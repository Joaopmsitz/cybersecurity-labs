# Atividade 4.10 — OTPClient

## Objetivo

Utilizar o **OTPClient** para armazenar um segredo TOTP em um banco de dados protegido e gerar códigos temporários de autenticação.

A atividade demonstra o cadastro manual de um token TOTP e a visualização do código gerado pelo aplicativo.

> **Segurança:** o segredo TOTP, senha do banco, QR Code, códigos temporários e arquivos de backup não são registrados neste README.

---

## Ambiente

* Kali Linux
* OTPClient
* Google Authenticator
* TOTP (Time-based One-Time Password)
* Banco de dados criptografado

---

## 1. Abrindo o OTPClient

O aplicativo foi iniciado pelo terminal:

```bash id="8wmdec"
otpclient
```

Durante a inicialização foi apresentada a seguinte mensagem:

```text
[WARNING] your OS's memlock limit may be too low for you (current value: 8388608 bytes).
This may cause issues when importing third parties databases or dealing with tens of tokens.
For information on how to increase the memlock value, please have a look at https://github.com/paolostivanin/OTPClient/wiki/Secure-Memory-Limitations
```

### Interpretação

O aviso informa que o limite de memória bloqueada (`memlock`) do sistema pode ser baixo.

O `memlock` está relacionado à capacidade de manter determinadas áreas de memória fora do processo de swap. O OTPClient utiliza mecanismos de proteção de memória para reduzir a exposição de informações sensíveis.

O aviso não impediu a execução do aplicativo no laboratório.

---

## 2. Criando o banco de dados

No OTPClient, foi criada uma nova base de dados:

```text
NewDatabase.enc
```

O arquivo foi salvo no diretório:

```text
/home/aluno/Documentos
```

Foi definida uma senha para proteger o banco de dados.

> A senha utilizada no laboratório não é publicada neste documento.

Após a criação, o banco foi desbloqueado para permitir o cadastro do token.

---

## 3. Gerando um novo segredo TOTP

Em outro terminal, foi executado:

```bash id="9c7j4a"
google-authenticator
```

Foi escolhida a utilização de tokens baseados em tempo:

```text
Do you want authentication tokens to be time-based (y/n) y
```

O Google Authenticator gerou um novo segredo TOTP.

O segredo real foi utilizado somente durante a configuração do laboratório e foi **omitido deste README**.

---

## 4. Adicionando o token ao OTPClient

No OTPClient, foi selecionada a opção:

```text
+
```

Em seguida, foi escolhida a configuração manual do token.

Foram preenchidos os campos relacionados à conta, emissor e segredo TOTP.

O segredo gerado pelo `google-authenticator` foi inserido no campo correspondente:

```text
Secret
```

O valor real não é reproduzido neste documento.

---

## 5. Visualizando o código TOTP

Após salvar o token, o registro foi exibido no OTPClient.

Ao selecionar o token, foram apresentadas informações como:

```text
Type
Account
Issuer
OTP Value
Validity
```

O campo **OTP Value** apresenta o código temporário atualmente gerado pelo OTPClient.

A validade indica o período restante antes da renovação do código.

O código TOTP é calculado a partir do segredo cadastrado e do horário atual:

```text
Segredo TOTP + Horário
          ↓
       TOTP
          ↓
Código temporário
```

---

## Conceitos

### OTP

**One-Time Password (OTP)** é uma senha destinada a ser utilizada uma única vez ou durante um período limitado.

No caso desta atividade, foi utilizado o **TOTP**, no qual o código é calculado com base no tempo.

### TOTP

O **Time-based One-Time Password** utiliza um segredo compartilhado e o horário atual para produzir códigos temporários.

Por isso, o segredo precisa ser protegido. Quem obtiver o segredo pode potencialmente gerar os mesmos códigos TOTP.

### OTPClient

O OTPClient permite armazenar tokens OTP em um banco de dados protegido e utilizar esses tokens para gerar códigos de autenticação.

Neste laboratório, o segredo foi cadastrado manualmente e o código foi gerado pelo aplicativo.

### Banco `NewDatabase.enc`

O arquivo criado pelo laboratório funciona como o armazenamento protegido dos tokens cadastrados no OTPClient.

Além do banco principal, foi criado um arquivo de backup durante a atividade.

Esses arquivos não devem ser publicados em repositórios públicos, pois podem conter informações necessárias para recuperar os tokens cadastrados.

---

## 6. Limpeza do laboratório

Após finalizar a atividade, foram verificados os arquivos criados no diretório:

```bash id="r2r8mn"
sudo -i
cd /home/aluno/Documentos
ls
```

Saída observada:

```text
NewDatabase.enc  NewDatabase.enc.bak  QRcode.png
```

Os arquivos gerados exclusivamente para o laboratório foram removidos:

```bash
rm *
```

O sistema solicitou confirmação:

```text
zsh: sure you want to delete all 3 files in /home/aluno/Documentos [yn]? y
```

> **Observação:** `rm *` é um comando destrutivo e foi utilizado aqui somente durante a limpeza do ambiente do laboratório, após verificar que os arquivos presentes eram os artefatos gerados pela atividade. Em um ambiente real, é mais seguro remover arquivos específicos pelo nome.

---

## Resultado

Foi criado um banco protegido no OTPClient e cadastrado manualmente um token TOTP gerado pelo `google-authenticator`.

O OTPClient conseguiu gerar e exibir o código temporário juntamente com suas informações de conta, emissor, tipo e validade.

A atividade demonstrou na prática o fluxo:

```text
Google Authenticator
        ↓
Segredo TOTP
        ↓
OTPClient
        ↓
Banco protegido
        ↓
Código TOTP temporário
```

---

## Evidências

[**Evidências — Módulo 4 / Aulas 3 e 4**](../evidencias.pdf)

**Evidência registrada:** passo 11 — visualização do token TOTP e do código temporário no OTPClient.
