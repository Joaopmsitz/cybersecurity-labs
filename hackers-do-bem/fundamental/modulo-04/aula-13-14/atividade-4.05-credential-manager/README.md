# Atividade 4.5 — Windows Credential Manager

## Objetivo

Explorar o **Credential Manager (Gerenciador de Credenciais)** do Windows Server 2022, identificando os diferentes tipos de credenciais armazenadas e realizando o procedimento de backup das credenciais em um ambiente de laboratório.

A atividade também demonstra a importância de proteger arquivos de backup de credenciais, pois eles podem conter informações sensíveis relacionadas à autenticação do sistema.

---

## Ambiente

* **Sistema:** Windows Server 2022
* **Recurso utilizado:** Credential Manager
* **Tipos de credenciais observados:**

  * Web Credentials
  * Windows Credentials
  * Certificate-based Credentials
  * Generic Credentials
* **Arquivo de backup:** `backup.cdr`

> As credenciais utilizadas para acesso ao ambiente do curso não são reproduzidas neste README.

---

## 1. Acesso ao Credential Manager

Após acessar o Windows Server 2022 no ambiente de laboratório, foi realizada uma pesquisa pelo recurso:

```text
Credential Manager
```

O **Credential Manager** foi então aberto.

Essa ferramenta permite visualizar e gerenciar determinados tipos de informações de autenticação armazenadas pelo Windows.

---

## 2. Web Credentials

Na seção **Web Credentials**, foram verificadas as credenciais disponíveis.

No ambiente utilizado pelo laboratório, essa seção podia estar vazia.

Essa área está relacionada a credenciais utilizadas por determinados componentes e aplicações do Windows para autenticação em recursos web.

---

## 3. Windows Credentials

Em seguida, foi acessada a seção **Windows Credentials**.

Foram observadas as categorias apresentadas pelo sistema:

```text
Windows Credentials
Certificate-based Credentials
Generic Credentials
```

### Windows Credentials

Relacionadas a credenciais utilizadas para autenticação em determinados recursos e serviços do Windows.

### Certificate-based Credentials

Relacionadas a mecanismos de autenticação baseados em certificados.

### Generic Credentials

Utilizadas por aplicações para armazenar determinados tipos de informações de autenticação que não se enquadram necessariamente nas credenciais específicas do Windows.

---

## 4. Início do backup das credenciais

Na janela do Credential Manager, foi selecionada a opção:

```text
Back up Credentials
```

O assistente de backup foi iniciado.

Em seguida, foi utilizada a opção para selecionar o local onde o arquivo seria salvo.

---

## 5. Definição do arquivo de backup

No assistente, foi selecionada a área de trabalho (**Desktop**) como local de armazenamento temporário.

O nome definido para o arquivo foi:

```text
backup
```

O Windows adicionou a extensão correspondente ao arquivo de backup.

O arquivo resultante foi:

```text
backup.cdr
```

> O arquivo de backup não faz parte deste repositório. Ele pode conter informações relacionadas às credenciais e deve ser tratado como material sensível.

---

## 6. Autenticação para criação do backup

Durante o processo, o Windows solicitou uma autenticação adicional.

No ambiente virtualizado, foi enviado o comando equivalente a:

```text
Ctrl + Alt + Delete
```

utilizando a barra de controle da máquina virtual.

A credencial da conta utilizada no laboratório foi então informada para confirmar a operação.

As credenciais de acesso do ambiente não são registradas neste README.

---

## 7. Confirmação do backup

Após a autenticação, o assistente prosseguiu com a criação do backup.

Ao finalizar, o Windows apresentou a confirmação:

```text
The backup was successful
```

Isso indica que o procedimento de criação do arquivo de backup foi concluído.

---

## 8. Verificação do arquivo

O arquivo criado foi localizado na área de trabalho:

```text
backup.cdr
```

Essa verificação demonstra que o backup foi efetivamente criado no local selecionado.

Por conter material relacionado às credenciais, o arquivo não deve ser enviado para um repositório GitHub ou compartilhado publicamente.

---

## 9. Limpeza do ambiente

Após a conclusão da atividade, o arquivo de backup foi removido do ambiente de laboratório.

A remoção é importante porque um backup de credenciais não deve permanecer armazenado sem necessidade.

O arquivo utilizado na atividade não foi incluído neste repositório.

---

## Conceitos praticados

### Credential Manager

O **Windows Credential Manager** é um componente do Windows utilizado para gerenciar diferentes tipos de credenciais utilizadas pelo sistema e por aplicações.

### Windows Credentials

Categoria destinada a credenciais utilizadas para determinados recursos e serviços do Windows.

### Generic Credentials

Categoria utilizada para credenciais genéricas armazenadas por aplicações e outros componentes.

### Certificate-based Credentials

Categoria relacionada a mecanismos de autenticação baseados em certificados.

### Backup de credenciais

O Windows permite realizar backup de determinadas informações de credenciais por meio do Credential Manager.

Esse recurso deve ser tratado com cuidado, pois o arquivo gerado possui informações relacionadas à autenticação.

---

## Cuidados de segurança

O arquivo de backup criado durante a atividade **não deve ser versionado no GitHub**.

Em um ambiente real, um arquivo desse tipo deve ser:

* protegido contra acesso não autorizado;
* armazenado somente quando necessário;
* protegido durante transferência;
* removido de locais temporários após o uso;
* nunca publicado em repositórios públicos.

No laboratório, o arquivo foi removido após a conclusão do exercício.

---

## Resultado

A atividade permitiu explorar o Credential Manager do Windows Server 2022 e compreender as principais categorias de credenciais apresentadas pela ferramenta.

Foi possível:

* localizar o Credential Manager;
* consultar Web Credentials;
* consultar Windows Credentials;
* identificar Certificate-based Credentials;
* identificar Generic Credentials;
* iniciar o assistente de backup;
* criar um arquivo de backup temporário;
* autenticar a operação;
* confirmar a criação do backup;
* remover o arquivo após a conclusão do laboratório.

O exercício demonstrou que mecanismos de gerenciamento e backup de credenciais devem ser tratados como componentes sensíveis da segurança do sistema.

---

## Evidência

[**Evidências — Módulo 4 / Aulas 1 e 2**](../evidencias.pdf)

**Print registrado:** etapa 11 da atividade, conforme definido na lista geral de evidências do Módulo 4.
