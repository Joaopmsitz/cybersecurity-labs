# Atividade 4.8 — Google Authenticator no Firefox

## Objetivo

Configurar um autenticador TOTP no Firefox utilizando a extensão **Authenticator by mymindstorm**, a partir de um segredo gerado pelo Google Authenticator no Kali Linux.

A atividade demonstra como um mesmo segredo TOTP pode ser utilizado por diferentes clientes autenticadores para gerar códigos temporários de autenticação.

> **Segurança:** o segredo TOTP, QR Code, códigos de autenticação e códigos de recuperação não são registrados neste README.

---

## Ambiente

* Kali Linux — máquina virtual do laboratório
* Firefox — computador pessoal
* Extensão **Authenticator by mymindstorm**
* Google Authenticator
* TOTP (Time-based One-Time Password)

---

## 1. Instalação da extensão no Firefox

No Firefox do computador pessoal, foi acessado o catálogo de extensões da Mozilla e pesquisada a extensão:

```text
Authenticator by mymindstorm
```

Após a instalação, a extensão foi adicionada à barra de ferramentas utilizando a opção de fixação.

---

## 2. Gerando o segredo TOTP no Kali Linux

No Kali Linux:

```bash
sudo -i
```

Em seguida, foi executado:

```bash
google-authenticator
```

Foi selecionada a opção de autenticação baseada em tempo:

```text
Do you want authentication tokens to be time-based (y/n) y
```

O Google Authenticator gerou um novo segredo TOTP e as informações necessárias para associá-lo a um aplicativo autenticador.

O segredo gerado foi **omitido deste documento**, pois ele funciona como uma credencial para geração dos códigos TOTP.

---

## 3. Transferência do segredo para o computador pessoal

O segredo TOTP gerado no Kali foi copiado por meio do recurso de área de transferência da máquina virtual para o computador pessoal.

Essa etapa permite configurar a extensão do Firefox manualmente, sem registrar o segredo em texto no repositório.

---

## 4. Configurando o Authenticator no Firefox

No Firefox, foi aberta a extensão **Authenticator by mymindstorm**.

Foi utilizada a opção de edição e, em seguida, a opção:

```text
+
```

A configuração foi inserida manualmente.

### Emissor

Foi utilizado:

```text
Kali Linux
```

### Secret

Foi inserido o segredo TOTP gerado anteriormente pelo:

```bash
google-authenticator
```

O valor real do segredo não é reproduzido neste README.

Após salvar a configuração, a extensão passou a apresentar a conta cadastrada e o código TOTP atual.

---

## 5. Visualização do código TOTP

Ao abrir a extensão **Authenticator** no Firefox, foi possível visualizar o código temporário gerado a partir do segredo cadastrado.

O código muda periodicamente conforme o intervalo definido pelo mecanismo TOTP.

A evidência desta etapa mostra o código sendo gerado diretamente pela extensão do navegador.

> O código apresentado na evidência é temporário e não deve ser reutilizado como credencial permanente.

---

## Conceitos

### TOTP

**Time-based One-Time Password** é um mecanismo de autenticação que gera senhas temporárias com base em um segredo compartilhado e no horário atual.

De forma simplificada:

```text
Segredo compartilhado + Hora atual
              ↓
        Algoritmo TOTP
              ↓
       Código temporário
```

O cliente autenticador e o sistema que valida o código precisam possuir o mesmo segredo e estar com o horário suficientemente sincronizado.

### Segredo TOTP

É a informação utilizada pelo autenticador para gerar os códigos. Quem possui esse segredo pode, em determinadas condições, gerar os mesmos códigos temporários.

Por isso, o segredo deve ser tratado como uma credencial e não deve ser publicado no GitHub.

### Authenticator no Firefox

A extensão funciona como um cliente autenticador capaz de armazenar o segredo e calcular os códigos TOTP diretamente no navegador.

Neste laboratório, o mesmo segredo criado no Kali foi utilizado para configurar a extensão no Firefox.

---

## Resultado

A extensão **Authenticator by mymindstorm** foi configurada manualmente no Firefox utilizando o segredo TOTP gerado no Kali Linux.

Ao abrir a extensão, foi possível visualizar o código TOTP atual e acompanhar sua renovação periódica.

A atividade demonstrou na prática a relação entre:

```text
Google Authenticator
        ↓
Segredo TOTP
        ↓
Authenticator no Firefox
        ↓
Código temporário
```

---

## Evidências

[**Evidências — Módulo 4 / Aulas 3 e 4**](../evidencias.pdf)

**Evidência registrada:** passo 14 — visualização do código TOTP no Authenticator do Firefox.
