# Atividade 5.10 — Rotação de Senha no Kali Linux

## Objetivo

Nesta atividade foi realizada uma configuração de **política de rotação de senhas** no Kali Linux.

O exercício utiliza o comando `passwd -S` para consultar informações relacionadas à senha dos usuários e, posteriormente, modifica o arquivo `/etc/login.defs` para estabelecer parâmetros de validade, intervalo mínimo entre alterações e período de aviso antes da expiração.

A prática permite observar como políticas de senha podem ser configuradas diretamente no sistema Linux.

---

## Ambiente

* **Sistema:** Kali Linux
* **Acesso:** RDP
* **IP da máquina:** `192.168.98.40`
* **Usuário:** `aluno`

> As credenciais utilizadas no laboratório não são registradas neste documento.

---

## 1. Acessando o terminal

Após acessar a máquina Kali Linux por RDP, foi aberto o terminal e obtido acesso administrativo:

```bash id="c7m2v8"
sudo -i
```

O acesso administrativo é necessário porque a atividade envolve a consulta e alteração de configurações do sistema.

---

## 2. Consultando a política da senha do usuário root

Com privilégios administrativos, foi utilizado:

```bash id="r4n8k1"
passwd -S
```

Saída observada:

```text id="9jtq3a"
┌──(root㉿kali)-[~]
└─# passwd -S   
root P 2024-07-02 0 99999 7 -1
```

O comando `passwd -S` exibe informações resumidas sobre o status da senha do usuário.

A saída:

```text id="x6p3q9"
root P 2024-07-02 0 99999 7 -1
```

pode ser interpretada como:

| Campo            | Valor        | Significado                                   |
| ---------------- | ------------ | --------------------------------------------- |
| Usuário          | `root`       | Conta consultada                              |
| Status           | `P`          | Senha definida                                |
| Última alteração | `2024-07-02` | Data da última alteração da senha             |
| Mínimo           | `0`          | Dias mínimos antes de permitir nova alteração |
| Máximo           | `99999`      | Número máximo de dias de validade             |
| Aviso            | `7`          | Dias de antecedência para aviso de expiração  |
| Inatividade      | `-1`         | Configuração de inatividade após expiração    |

Esses valores representam a política existente para a conta no momento da consulta.

---

## 3. Consultando a política da senha do usuário aluno

Após a consulta da conta `root`, foi encerrada a sessão administrativa:

```bash id="q5v9r2"
exit
```

Em seguida, foi executado novamente:

```bash id="h8k3w6"
passwd -S
```

Saída observada:

```text id="35gooa"
┌──(aluno㉿kali)-[~]
└─$ passwd -S
aluno P 2025-09-06 0 99999 7 -1
```

A saída apresenta a mesma estrutura de informações, desta vez referente ao usuário `aluno`:

```text id="u2m7x4"
aluno P 2025-09-06 0 99999 7 -1
```

Os principais valores observados são:

* usuário: `aluno`;
* status da senha: `P`;
* última alteração registrada: `2025-09-06`;
* período mínimo: `0` dias;
* período máximo: `99999` dias;
* aviso de expiração: `7` dias;
* inatividade após expiração: `-1`.

> A data exibida corresponde à saída observada no material do laboratório e pode variar conforme a máquina utilizada.

---

## 4. Editando o arquivo de configuração

Para configurar os parâmetros da política de senha, foi utilizado o editor `nano` com privilégios administrativos:

```bash id="m9x4q7"
sudo nano /etc/login.defs
```

O arquivo `/etc/login.defs` contém configurações utilizadas por ferramentas relacionadas ao gerenciamento de contas e senhas em sistemas Linux.

No arquivo, foram localizados os seguintes parâmetros:

```text id="y590cv"
PASS_MAX_DAYS   99999
PASS_MIN_DAYS   0
PASS_WARN_AGE   7
```

Esses valores representam a configuração anterior observada no laboratório.

---

## 5. Configurando a rotação de senha

Os parâmetros foram alterados para:

```text id="ei8ksn"
PASS_MAX_DAYS   270
PASS_MIN_DAYS   90
PASS_WARN_AGE   10
```

Esses valores estabelecem:

### PASS_MAX_DAYS

```text id="j8q3v6"
PASS_MAX_DAYS   270
```

Define o número máximo de dias durante os quais uma senha pode permanecer válida antes de exigir alteração.

Neste laboratório, a validade máxima configurada foi de **270 dias**.

### PASS_MIN_DAYS

```text id="p6r2w9"
PASS_MIN_DAYS   90
```

Define a quantidade mínima de dias que deve passar antes que o usuário possa alterar novamente sua senha.

Neste laboratório, foi configurado um intervalo mínimo de **90 dias**.

### PASS_WARN_AGE

```text id="z4m7k2"
PASS_WARN_AGE   10
```

Define com quantos dias de antecedência o sistema deve avisar o usuário sobre a proximidade da expiração da senha.

Neste laboratório, o aviso foi configurado para ocorrer **10 dias antes da expiração**.

---

## 6. Salvando a configuração

Após realizar as alterações no arquivo `/etc/login.defs`, o arquivo foi salvo pelo `nano` utilizando:

```text id="s5x8n3"
Ctrl + X
S
Enter
```

Depois disso, o terminal foi fechado.

---

## Conceitos envolvidos

### Rotação de senhas

A rotação de senhas consiste em estabelecer regras que determinam quando uma senha deve ser alterada.

Em ambientes corporativos, políticas desse tipo podem fazer parte dos controles de gerenciamento de identidade e acesso, ajudando a estabelecer requisitos administrativos para as credenciais.

### `/etc/login.defs`

O arquivo:

```text id="a7k2m5"
/etc/login.defs
```

é utilizado para armazenar diversos parâmetros relacionados ao gerenciamento de contas no Linux.

Nesta atividade, foram utilizados especificamente:

```text id="v9p4x1"
PASS_MAX_DAYS
PASS_MIN_DAYS
PASS_WARN_AGE
```

### Política configurada

A configuração final utilizada no laboratório foi:

```text id="n3w8q6"
PASS_MAX_DAYS   270
PASS_MIN_DAYS   90
PASS_WARN_AGE   10
```

Representando:

```text id="c6r1t8"
Senha
 │
 ├── Validade máxima: 270 dias
 │
 ├── Intervalo mínimo para alteração: 90 dias
 │
 └── Aviso antes da expiração: 10 dias
```

---

## Resultado

A atividade permitiu consultar os parâmetros de validade das senhas utilizando `passwd -S` e configurar novos valores no arquivo `/etc/login.defs`.

A configuração anterior observada era:

```text id="f2k7m4"
PASS_MAX_DAYS   99999
PASS_MIN_DAYS   0
PASS_WARN_AGE   7
```

Após a alteração, os parâmetros definidos no laboratório foram:

```text id="ei8ksn"
PASS_MAX_DAYS   270
PASS_MIN_DAYS   90
PASS_WARN_AGE   10
```

Com isso, foi estabelecida uma política de rotação de senha com validade máxima de 270 dias, intervalo mínimo de 90 dias entre alterações e aviso de expiração com 10 dias de antecedência.

---

## Evidência

A evidência desta atividade corresponde ao **passo 5**, mostrando a configuração dos parâmetros no arquivo `/etc/login.defs`:

```text
PASS_MAX_DAYS   270
PASS_MIN_DAYS   90
PASS_WARN_AGE   10
```

[**Evidências — Módulo 5 / Aulas 3 e 4**](../evidencias.pdf)
