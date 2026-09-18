# Atividade 4.7 — Explorando o Google Authenticator no Kali Linux

## Objetivo

Configurar o **Google Authenticator** no Kali Linux utilizando **TOTP (Time-based One-Time Password)**.

A atividade demonstra a geração de uma chave secreta, a associação dessa chave a um aplicativo autenticador por meio de QR Code e a geração de códigos temporários utilizados como segundo fator de autenticação.

O laboratório foi realizado em ambiente acadêmico controlado.

---

## Ambiente

* **Sistema:** Kali Linux
* **Usuário:** `root` durante a configuração do autenticador
* **Aplicativo utilizado:** Google Authenticator
* **Método:** TOTP
* **Período de validade do código:** aproximadamente 30 segundos
* **Dispositivo adicional:** smartphone

> As credenciais de acesso à VM, a chave secreta TOTP, os códigos temporários e os códigos de recuperação utilizados no laboratório não são publicados neste README.

---

## 1. Acesso administrativo

Inicialmente, foi aberto o terminal e obtido acesso de superusuário:

```bash
sudo -i
```

A senha utilizada pertence ao ambiente do laboratório e não é registrada neste documento.

---

## 2. Configuração do fuso horário

Antes de configurar o autenticador, o fuso horário da máquina foi definido para o horário de São Paulo:

```bash
timedatectl set-timezone America/Sao_Paulo
```

Em seguida, foi verificada a configuração:

```bash
timedatectl
```

Saída observada:

```text
Local time: sáb 2025-09-06 20:46:18 -03
Universal time: sáb 2025-09-06 23:46:18 UTC
RTC time: sáb 2025-09-06 23:46:18
Time zone: America/Sao_Paulo (-03, -0300)
System clock synchronized: yes
NTP service: active
RTC in local TZ: no
```

A sincronização correta do horário é importante para TOTP, pois os códigos são calculados com base no tempo atual.

---

## 3. Inicialização do Google Authenticator

O programa foi iniciado no Kali Linux com:

```bash
google-authenticator
```

Foi escolhida a opção para utilizar tokens baseados em tempo:

```text
Do you want authentication tokens to be time-based (y/n) y
```

O programa então apresentou um QR Code no terminal e gerou uma chave secreta associada à configuração.

Por segurança, a chave exibida durante o laboratório não é reproduzida neste README.

O fluxo gerado pelo programa foi equivalente a:

```text
Do you want authentication tokens to be time-based (y/n) y
Warning: pasting the following URL into your browser exposes the OTP secret to Google:
  [URL otpauth contendo segredo removida]

Your new secret key is: [SEGREDO TOTP REMOVIDO]
```

A chave secreta é o elemento utilizado para permitir que o aplicativo autenticador e o servidor produzam os mesmos códigos TOTP.

---

## 4. Associação com o Google Authenticator

Com o Google Authenticator instalado no smartphone, foi selecionada a opção para adicionar uma nova conta por meio da leitura de um QR Code.

O QR Code apresentado no terminal do Kali foi escaneado pelo aplicativo.

Após a associação, o Google Authenticator passou a gerar códigos TOTP para a conta configurada.

---

## 5. Validação do código TOTP

O código apresentado pelo aplicativo foi informado no terminal do Kali quando solicitado:

```text
Enter code from app (-1 to skip): [CÓDIGO TOTP REMOVIDO]
Code confirmed
```

O programa também apresentou códigos de recuperação.

Esses códigos não são reproduzidos neste README porque funcionam como credenciais alternativas para acesso à conta configurada.

O resultado:

```text
Code confirmed
```

confirmou que o código gerado pelo aplicativo correspondia ao código esperado pelo Google Authenticator no Kali Linux.

---

## 6. Configuração das opções de segurança

Após a confirmação do código, o programa solicitou algumas configurações adicionais.

No laboratório, foram aceitas as opções apresentadas pelo roteiro.

### Atualização do arquivo de configuração

```text
Do you want me to update your "/root/.google_authenticator" file? (y/n) y
```

O arquivo `.google_authenticator` é utilizado para armazenar as informações necessárias à configuração do autenticador para o usuário.

### Restrição de reutilização do token

Foi habilitada a opção para impedir o uso múltiplo do mesmo token:

```text
Do you want to disallow multiple uses of the same authentication
token? ... (y/n) y
```

Essa configuração ajuda a evitar a reutilização do mesmo código durante sua janela de validade.

### Janela de tolerância de tempo

Também foi habilitada a opção relacionada à compensação de possíveis diferenças de horário entre cliente e servidor:

```text
Do you want to do so? (y/n) y
```

O objetivo dessa configuração é permitir uma margem para diferenças de sincronização temporal.

### Rate limiting

Por fim, foi habilitado o controle de taxa para tentativas de autenticação:

```text
If the computer that you are logging into isn't hardened against brute-force
login attempts, you can enable rate-limiting for the authentication module.

Do you want to enable rate-limiting? (y/n) y
```

Essa opção limita a quantidade de tentativas permitidas dentro de determinado intervalo de tempo, dificultando tentativas automatizadas de força bruta.

---

## 7. Funcionamento do TOTP

O **TOTP (Time-based One-Time Password)** gera códigos temporários com base em uma chave secreta compartilhada e no horário atual.

O processo observado no laboratório pode ser representado da seguinte forma:

```text
Chave secreta
      │
      ├───────────────┐
      │               │
      ▼               ▼
Kali Linux       Google Authenticator
      │               │
      │   mesmo tempo │
      └───────┬───────┘
              ▼
        Código TOTP
       temporário
```

O servidor e o aplicativo não precisam trocar o código pela rede para gerar o valor. Ambos utilizam a mesma chave secreta e uma referência temporal para calcular o código esperado.

---

## Conceitos praticados

### TOTP

O **Time-based One-Time Password** é um mecanismo de autenticação baseado em códigos temporários calculados a partir de uma chave secreta e do tempo.

### Segundo fator de autenticação

O TOTP pode ser utilizado como um segundo fator além da senha tradicional.

Nesse cenário, mesmo que uma senha seja conhecida, o acesso pode exigir também o código temporário gerado pelo autenticador.

### Chave secreta

A chave secreta é utilizada pelos dois lados para gerar os mesmos códigos TOTP.

Ela deve ser protegida como uma credencial.

### QR Code

O QR Code apresentado pelo `google-authenticator` fornece uma maneira prática de transferir a configuração do token para o aplicativo autenticador.

### Sincronização de horário

Como o TOTP depende do tempo, diferenças significativas entre o relógio do servidor e o dispositivo autenticador podem causar falhas na validação.

Por isso, a atividade começou configurando e verificando o fuso horário da máquina.

### Rate limiting

O controle de taxa reduz a quantidade de tentativas de autenticação permitidas em determinado período, ajudando contra tentativas automatizadas de força bruta.

---

## Resultado

A atividade permitiu configurar o Google Authenticator no Kali Linux e associá-lo a um smartphone utilizando TOTP.

Foi possível:

* configurar o fuso horário do Kali Linux;
* iniciar o `google-authenticator`;
* habilitar tokens baseados em tempo;
* gerar uma configuração TOTP;
* apresentar o QR Code no terminal;
* cadastrar o token no aplicativo Google Authenticator;
* gerar um código temporário;
* validar o código no Kali Linux;
* configurar proteção contra reutilização de tokens;
* configurar tolerância para diferenças de horário;
* habilitar rate limiting;
* concluir a configuração do segundo fator.

A atividade demonstrou na prática como um autenticador TOTP pode complementar a autenticação baseada em senha.

---

## Evidência

[**Evidências — Módulo 4 / Aulas 3 e 4**](../evidencias.pdf)

**Print registrado:** etapa 9 da atividade, conforme solicitado pelo roteiro geral de evidências do Módulo 4.
