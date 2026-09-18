# Atividade 9.3 — Conhecendo o Certificado Digital Obtido no Windows Server 2022

## Objetivo

Acessar e analisar um certificado digital emitido pela Autoridade Certificadora configurada nas atividades anteriores.

A atividade foi realizada em um Windows Server 2022 utilizado como cliente, verificando inicialmente a comunicação com o servidor da CA e, posteriormente, analisando o certificado `aluno-DC01-CA` instalado nas **Trusted Root Certification Authorities**.

Foram observadas informações como:

* versão do certificado;
* algoritmo de assinatura;
* algoritmo de hash da assinatura;
* período de validade;
* chave pública;
* utilização da chave;
* caminho de certificação;
* finalidades do certificado;
* informações relacionadas ao OCSP.

---

## Ambiente

* **Sistema:** Windows Server 2022
* **Cliente:** Windows Server 2022
* **Autoridade Certificadora:** `aluno-DC01-CA`
* **Domínio:** `aluno.hacker.com`
* **Repositório do certificado:** Trusted Root Certification Authorities
* **Certificado analisado:** `aluno-DC01-CA`

> As credenciais utilizadas para acesso ao ambiente de laboratório não são registradas neste README.

---

## 1. Teste de conectividade com o servidor

Inicialmente, foi aberto o **Command Prompt** no Windows Server 2022 cliente.

Foi realizado um teste de conectividade com o servidor da Autoridade Certificadora utilizando:

```cmd id="7s9q1m"
ping 192.168.98.20
```

O retorno apresentado foi:

```text id="v6v0bd"
C:\Users\nome1>ping 192.168.98.20

Pinging 192.168.98.20 with 32 bytes of data:
Reply from 192.168.98.20: bytes=32 time<1ms TTL=128
Reply from 192.168.98.20: bytes=32 time=1ms TTL=128
```

As respostas demonstram que o cliente conseguiu estabelecer comunicação com o servidor.

---

## 2. Acesso ao gerenciamento de certificados

Após o teste de conectividade, o **Command Prompt** foi fechado.

No campo de pesquisa do Windows foi digitado:

```text id="2w8t3u"
Manage user certificates
```

Foi então aberto o console de gerenciamento de certificados do usuário:

```text id="q0v5r4"
certmgr
```

---

## 3. Localização do certificado da CA

No console de certificados, foi acessado:

```text id="8z5g1p"
Trusted Root Certification Authorities
└── Certificates
```

Nessa seção foi localizado o certificado:

```text id="1m8x4v"
aluno-DC01-CA
```

O certificado apresentava como emissor a própria Autoridade Certificadora:

```text id="7f1p3k"
Issued By: aluno-DC01-CA
```

Isso é esperado para uma **Root CA**, pois o certificado raiz é autoassinado.

---

## 4. Abertura do certificado

O certificado `aluno-DC01-CA` foi aberto para visualizar suas propriedades.

A janela de propriedades apresenta diferentes abas que permitem analisar as informações e extensões presentes no certificado.

---

## 5. Análise da aba General

Na aba **General**, foram observadas as informações gerais do certificado.

Essa seção permite verificar, entre outros elementos:

* para quem o certificado foi emitido;
* quem o emitiu;
* período de validade;
* situação de confiança do certificado;
* finalidade de utilização da chave.

A análise dessa aba permite identificar a relação entre o certificado instalado no cliente e a Autoridade Certificadora responsável por sua emissão.

---

## 6. Acesso aos detalhes do certificado

Em seguida, foi selecionada a aba:

```text id="r3k7w2"
Details
```

Essa seção apresenta os campos individuais do certificado digital.

Entre as informações disponíveis estão:

```text id="d8p2n1"
Version
Signature algorithm
Signature hash algorithm
Valid to
Public Key
Key Usage
```

Esses campos permitem analisar tecnicamente a estrutura e as características criptográficas do certificado.

---

## 7. Principais campos observados

### Version

Indica a versão do padrão de certificado utilizado.

Certificados digitais baseados em X.509 utilizam esse campo para identificar a versão da estrutura do certificado.

### Signature algorithm

Identifica o algoritmo utilizado para gerar a assinatura digital do certificado.

A assinatura permite verificar se o conteúdo do certificado foi assinado pela autoridade responsável.

### Signature hash algorithm

Indica o algoritmo de hash utilizado como parte do processo de assinatura.

O hash transforma os dados do certificado em um resumo de tamanho definido, que é posteriormente utilizado no processo de assinatura.

### Valid to

Indica o limite final do período de validade do certificado.

Um certificado possui um período de validade definido e, após esse período, não deve ser considerado válido para os usos correspondentes.

### Public Key

Apresenta a chave pública associada ao certificado.

A chave pública pode ser distribuída e utilizada por terceiros para operações criptográficas ou para validação de assinaturas, dependendo da finalidade do certificado.

### Key Usage

Define as utilizações criptográficas permitidas para a chave de acordo com as extensões presentes no certificado.

---

## 8. Caminho de certificação

Após a análise da aba **Details**, foi acessada a seção:

```text id="0p5h9q"
Certification Path
```

Essa seção apresenta a hierarquia de confiança relacionada ao certificado.

Como o certificado analisado pertence à CA raiz do laboratório, ele aparece associado à autoridade:

```text id="h3c6y1"
aluno-DC01-CA
```

O caminho de certificação é importante para entender como o sistema estabelece confiança entre certificados e autoridades certificadoras.

---

## 9. Propriedades e finalidades do certificado

O certificado foi acessado com o botão direito e selecionada a opção:

```text id="u8k2r6"
Properties
```

Na aba **General**, foi observada a seção:

```text id="q4n7s0"
Certificate purposes
```

Essa área permite identificar as finalidades para as quais o certificado pode ser utilizado.

Também foi observada a aba:

```text id="e6p1w5"
OCSP
```

O **OCSP (Online Certificate Status Protocol)** é utilizado em infraestruturas de certificados para consultar informações relacionadas ao status de certificados, como sua situação de revogação.

---

## Evidência — Passo 10

A evidência solicitada para esta atividade corresponde ao **passo 10 da sequência geral**, com a aba **Details** do certificado aberta.

**Frase obrigatória antes do print:**

> **Print da atividade 9.3:** aba Details do certificado `aluno-DC01-CA`, apresentando os campos de versão, algoritmo de assinatura, algoritmo de hash, validade, chave pública e utilização da chave.

Os principais campos esperados na tela são:

```text id="7w4m2c"
Version
Signature algorithm
Signature hash algorithm
Valid to
Public Key
Key Usage
```

[**Evidências — Módulo 9 / Aulas 33 e 34**](../evidencias.pdf)

---

## Conceitos aplicados

### Certificado digital

Um certificado digital associa uma identidade a uma chave pública e contém informações que permitem sua utilização dentro de uma infraestrutura de confiança.

### X.509

O certificado analisado segue a estrutura utilizada pelo padrão **X.509**, que define campos como emissor, sujeito, validade, chave pública, assinatura e extensões.

### Chave pública

A chave pública é armazenada no certificado e pode ser disponibilizada para outras entidades. Seu uso depende da finalidade definida no certificado.

### Assinatura digital

A assinatura da CA permite verificar a integridade do certificado e sua relação com a autoridade que o assinou.

### Certification Path

O caminho de certificação representa a cadeia de confiança entre o certificado analisado e uma autoridade certificadora confiável.

### OCSP

O **OCSP** é um protocolo utilizado para consultar o status de certificados digitais, especialmente para verificar informações relacionadas à revogação.

---

## Fluxo da análise

```text id="z1k5m8"
Windows Server 2022 Cliente
            │
            ▼
      Teste de conectividade
            │
            ▼
       Manage user certificates
            │
            ▼
Trusted Root Certification Authorities
            │
            ▼
       aluno-DC01-CA
            │
            ├── General
            │
            ├── Details
            │
            ├── Certification Path
            │
            └── Certificate purposes / OCSP
```

---

## Resultado

Foi localizado no Windows Server 2022 cliente o certificado da Autoridade Certificadora:

```text id="a6s9c2"
aluno-DC01-CA
```

A análise permitiu identificar os principais componentes de um certificado digital X.509, incluindo informações de assinatura, hash, validade, chave pública e utilização da chave.

Também foi analisado o **caminho de certificação** e observada a seção de **Certificate purposes**, além da referência ao **OCSP** nas propriedades do certificado.
