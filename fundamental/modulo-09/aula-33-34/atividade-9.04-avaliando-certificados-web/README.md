# Atividade 9.4 — Avaliando Certificados Web no Windows Server 2022

## Objetivo

Analisar um certificado digital utilizado por um site web e observar suas principais informações de segurança e identificação.

Durante a atividade foi acessado o site `https://www.google.com/` pelo Microsoft Edge, analisado o certificado apresentado pela conexão HTTPS e, posteriormente, o certificado foi exportado e aberto no Notepad para visualizar sua estrutura em formato PEM.

Foram observadas informações como:

* entidade para a qual o certificado foi emitido;
* autoridade certificadora emissora;
* período de validade;
* fingerprints;
* hierarquia de certificação;
* campos do certificado;
* representação PEM.

---

## Ambiente

* **Sistema:** Windows Server 2022
* **Navegador:** Microsoft Edge
* **Protocolo analisado:** HTTPS
* **Site utilizado:** `https://www.google.com/`
* **Formato analisado após exportação:** PEM

---

## 1. Acesso ao site

Foi aberto o **Microsoft Edge** no Windows Server 2022.

No navegador, foi acessado:

```text
https://www.google.com/
```

O site foi carregado utilizando uma conexão HTTPS.

---

## 2. Verificação da conexão segura

Na barra de endereço do navegador, foi selecionado o ícone de segurança referente à conexão.

Foi apresentada a indicação:

```text
Connection is secure
```

Essa informação indica que o navegador estabeleceu uma conexão HTTPS e realizou as verificações correspondentes ao certificado apresentado pelo servidor.

---

## 3. Acesso ao certificado

A partir das informações da conexão segura, foi selecionado o ícone relacionado ao certificado.

Foi aberta a visualização das informações do certificado digital utilizado pelo site.

---

## 4. Análise das informações gerais

Na seção **General**, foram observadas informações relacionadas ao certificado, incluindo:

```text
Issued To
Issued By
Validity Period
Fingerprints
```

### Issued To

Identifica a entidade ou os nomes associados ao certificado.

### Issued By

Identifica a Autoridade Certificadora responsável pela emissão do certificado.

### Validity Period

Apresenta o período durante o qual o certificado é considerado válido.

### Fingerprints

São identificadores derivados do conteúdo do certificado por meio de funções de hash. Eles podem ser utilizados para comparar ou identificar um certificado específico.

---

## 5. Análise dos detalhes

Na seção de detalhes do certificado foram observados:

```text
Certificate Hierarchy
Certificate Fields
```

A **Certificate Hierarchy** apresenta a cadeia de confiança utilizada para validar o certificado.

Os **Certificate Fields** apresentam os campos que compõem a estrutura do certificado digital, incluindo informações relacionadas ao sujeito, emissor, validade, chave pública, assinatura e extensões.

---

## 6. Exportação do certificado

O certificado foi exportado para o computador utilizando a opção de exportação disponibilizada pelo navegador.

O arquivo foi salvo no diretório:

```text
Downloads
```

Essa etapa permitiu analisar posteriormente o conteúdo do certificado fora da interface gráfica do navegador.

---

## 7. Abertura do certificado no Notepad

Após a exportação, foi aberto o **Notepad**.

No menu:

```text
File → Open
```

foi acessada a pasta:

```text
Downloads
```

A visualização de arquivos foi alterada para:

```text
All files
```

Dessa forma, foi possível localizar e abrir o arquivo de certificado exportado.

---

## 8. Estrutura PEM

Ao abrir o certificado exportado no Notepad, foi possível visualizar sua representação em formato **PEM (Privacy-Enhanced Mail)**.

Um certificado PEM normalmente possui uma estrutura semelhante a:

```text
-----BEGIN CERTIFICATE-----
[conteúdo codificado em Base64]
-----END CERTIFICATE-----
```

O conteúdo entre os marcadores corresponde à representação Base64 do certificado.

A codificação Base64 não é uma forma de criptografia. Ela serve para representar dados binários em texto, facilitando seu armazenamento e transporte em ambientes que trabalham com conteúdo textual.

---

## Evidência — Passo 14

A evidência solicitada para a atividade corresponde ao **passo 14**, com o certificado exportado aberto no Notepad e sua estrutura PEM visível.

**Frase obrigatória antes do print:**

> **Print da atividade 9.4:** certificado digital web exportado e aberto no Notepad, apresentando sua estrutura em formato PEM com os marcadores `BEGIN CERTIFICATE` e `END CERTIFICATE`.

A tela deve permitir visualizar a estrutura do certificado exportado.

[**Evidências — Módulo 9 / Aulas 33 e 34**](../evidencias.pdf)

---

## Conceitos aplicados

### HTTPS

O **HTTPS** utiliza TLS para proteger a comunicação entre cliente e servidor. O certificado digital apresentado pelo servidor participa do processo de autenticação da identidade do servidor e estabelecimento da conexão segura.

### Certificado X.509

Os certificados utilizados em conexões TLS normalmente seguem o padrão X.509 e contêm informações sobre o sujeito, emissor, validade, chave pública, assinatura e extensões.

### Autoridade Certificadora

A Autoridade Certificadora assina certificados digitais para estabelecer uma cadeia de confiança.

O navegador utiliza as informações presentes no certificado e na cadeia de certificação para realizar as verificações necessárias.

### Fingerprint

O fingerprint é um resumo criptográfico do certificado. Ele pode ser utilizado para identificar e comparar certificados.

### PEM

O formato PEM representa dados criptográficos binários em texto utilizando Base64 e delimitadores.

Exemplo:

```text
-----BEGIN CERTIFICATE-----
...
-----END CERTIFICATE-----
```

e:

```text
-----END CERTIFICATE-----
```

O conteúdo Base64 pode posteriormente ser convertido novamente para sua representação binária original.

---

## Fluxo da atividade

```text
Microsoft Edge
      │
      ▼
https://www.google.com/
      │
      ▼
Conexão HTTPS
      │
      ▼
Certificado do servidor
      │
      ├── Issued To
      ├── Issued By
      ├── Validity Period
      ├── Fingerprints
      ├── Certificate Hierarchy
      └── Certificate Fields
              │
              ▼
        Exportação
              │
              ▼
          Downloads
              │
              ▼
           Notepad
              │
              ▼
        Estrutura PEM
```

---

## Resultado

Foi analisado um certificado digital utilizado em uma conexão HTTPS, permitindo observar suas informações gerais, autoridade emissora, validade, fingerprints, hierarquia e campos do certificado.

Após a exportação, o certificado foi aberto no Notepad e sua representação em **PEM**, contendo os delimitadores `BEGIN CERTIFICATE` e `END CERTIFICATE`, foi identificada.

A atividade demonstrou a relação entre os certificados digitais, a autenticação de servidores em conexões HTTPS e a estrutura utilizada para representar certificados em formato textual.
