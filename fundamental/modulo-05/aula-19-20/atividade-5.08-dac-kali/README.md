# Atividade 5.8 — DAC no Kali Linux

## Objetivo

Nesta atividade foi realizada uma prática de **Controle de Acesso Discricionário (DAC — Discretionary Access Control)** no Kali Linux, utilizando as permissões tradicionais de arquivos do Linux.

O objetivo é observar as permissões inicialmente atribuídas a um arquivo e, em seguida, modificá-las utilizando o comando `chmod`, concedendo ao proprietário do arquivo permissões de leitura, escrita e execução.

---

## Ambiente

* **Sistema:** Kali Linux
* **Acesso:** RDP
* **IP da máquina:** `192.168.98.40`
* **Usuário:** `aluno`
* **Diretório utilizado:** `/home/aluno/Documentos/`

> As credenciais utilizadas no laboratório não são registradas neste documento.

---

## 1. Acessando o terminal

Após acessar a máquina Kali Linux por RDP, foi aberto o terminal e obtido acesso administrativo com:

```bash
sudo -i
```

Em seguida, foi acessado o diretório `Documentos` do usuário:

```bash
cd /home/aluno/Documentos/
```

---

## 2. Criando o arquivo

Foi utilizado o editor `nano` para criar o arquivo `texto.txt`:

```bash
nano texto.txt
```

O conteúdo inserido no arquivo foi:

```text
Teste1
```

O arquivo foi salvo utilizando:

```text
Ctrl + X
S
Enter
```

---

## 3. Verificando o arquivo

Após salvar o arquivo, foi utilizado o comando `ls` para confirmar sua existência:

```bash
ls
```

Saída observada:

```text
┌──(root㉿kali)-[/home/aluno/Documentos]
└─# ls            
texto.txt
```

O resultado confirma que o arquivo `texto.txt` foi criado no diretório `/home/aluno/Documentos/`.

---

## 4. Verificando as permissões atuais

Para visualizar as permissões detalhadas do arquivo, foi executado:

```bash
ls -l
```

Saída observada:

```text
┌──(root㉿kali)-[/home/aluno/Documentos]
└─# ls -l         
total 4
-rw-r--r-- 1 root root 7 fev 10 18:10 texto.txt
```

A saída pode ser interpretada da seguinte forma:

```text
-rw-r--r-- 1 root root 7 fev 10 18:10 texto.txt
│││││││││
││││││││└── arquivo
│││││││└─── permissões de outros usuários
││││││└──── permissões do grupo
│││││└───── permissões do proprietário
```

A sequência:

```text
-rw-r--r--
```

representa:

* `-` → arquivo regular;
* `rw-` → o proprietário possui leitura e escrita;
* `r--` → o grupo possui apenas leitura;
* `r--` → outros usuários possuem apenas leitura.

Também é possível observar que:

* o proprietário é `root`;
* o grupo associado é `root`;
* o arquivo possui 7 bytes;
* o nome do arquivo é `texto.txt`.

---

## 5. Modificando as permissões com chmod

Para demonstrar o controle de acesso discricionário, foi utilizado o comando:

```bash
chmod u+rwx texto.txt
```

O comando `chmod` permite modificar as permissões de acesso de arquivos e diretórios.

Neste caso:

* `u` → **user**, ou seja, o proprietário do arquivo;
* `+` → adiciona permissões;
* `r` → leitura (**read**);
* `w` → escrita (**write**);
* `x` → execução (**execute**);
* `texto.txt` → arquivo que terá suas permissões modificadas.

Assim, o comando adiciona as permissões de **leitura, escrita e execução ao proprietário** do arquivo.

---

## 6. Verificando a nova permissão

Após executar o `chmod`, foi utilizado novamente:

```bash
ls -l
```

Saída observada:

```text
┌──(root㉿kali)-[/home/aluno/Documentos]
└─# ls -l
total 4
-rwxr--r-- 1 root root 7 fev 10 18:10 texto.txt
```

A alteração pode ser observada na primeira parte da permissão:

Antes:

```text
-rw-r--r--
```

Depois:

```text
-rwxr--r--
```

A permissão `x` foi adicionada ao proprietário. Dessa forma, o proprietário `root` passou a possuir:

```text
rwx
```

ou seja:

* leitura;
* escrita;
* execução.

Enquanto as permissões do grupo e dos demais usuários permaneceram:

```text
r--
```

---

## Conceitos envolvidos

### DAC — Discretionary Access Control

O **DAC (Discretionary Access Control)** é um modelo de controle de acesso no qual o proprietário de um recurso possui autoridade para definir ou modificar as permissões de acesso.

No Linux, esse modelo é representado principalmente pelas permissões associadas a:

* proprietário (**user/owner**);
* grupo (**group**);
* outros usuários (**others**).

### Permissões Linux

As três permissões básicas utilizadas são:

| Permissão | Símbolo | Significado       |
| --------- | ------- | ----------------- |
| Read      | `r`     | Permite leitura   |
| Write     | `w`     | Permite alteração |
| Execute   | `x`     | Permite execução  |

Essas permissões são organizadas em três grupos:

```text
rwx rwx rwx
│   │   │
│   │   └── others
│   └────── group
└────────── owner
```

### chmod

O comando `chmod` é utilizado para alterar as permissões de arquivos e diretórios.

Nesta atividade foi utilizado:

```bash
chmod u+rwx texto.txt
```

O comando modificou somente as permissões do proprietário, sem alterar as permissões atribuídas ao grupo ou aos demais usuários.

---

## Resultado

A atividade demonstrou, na prática, como o **DAC funciona no Linux** por meio das permissões tradicionais de arquivos.

O arquivo inicialmente possuía:

```text
-rw-r--r--
```

Após a execução de:

```bash
chmod u+rwx texto.txt
```

passou a possuir:

```text
-rwxr--r--
```

A alteração mostra que o proprietário do arquivo recebeu a permissão de execução, mantendo as permissões de leitura e escrita que já possuía.

---

## Evidência

A evidência desta atividade corresponde ao **passo 7**, após a execução do `chmod` e a verificação das novas permissões com `ls -l`.

[**Evidências — Módulo 5 / Aulas 3 e 4**](../evidencias.pdf)
