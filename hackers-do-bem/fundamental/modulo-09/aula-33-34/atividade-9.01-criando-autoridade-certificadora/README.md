# Atividade 9.1 — Criando uma Autoridade Certificadora no Windows Server 2022

## Objetivo

Implementar uma **Autoridade Certificadora (CA)** utilizando o Windows Server 2022 e o serviço **Active Directory Certificate Services (AD CS)**.

Durante a atividade foi configurada uma CA corporativa do tipo **Enterprise Root CA**, utilizando:

* RSA de 2048 bits;
* SHA-256;
* chave privada nova;
* validade dos certificados de 10 anos;
* base de dados padrão do serviço de certificados.

Ao final, a autoridade certificadora foi disponibilizada no servidor com o nome `aluno-DC01-CA`.

---

## Ambiente

* **Sistema:** Windows Server 2022
* **Serviço:** Active Directory Certificate Services (AD CS)
* **Função:** Certification Authority
* **Tipo de CA:** Enterprise CA
* **Hierarquia:** Root CA
* **Criptografia:** RSA 2048 bits
* **Hash:** SHA-256
* **Validade configurada:** 10 anos
* **Base de dados:** `C:\Windows\system32\CertLog`

> As credenciais utilizadas para acesso ao ambiente de laboratório não são registradas neste README.

---

## 1. Acesso ao Server Manager

Após inicializar o Windows Server 2022, foi aberto o **Server Manager** por meio do campo de pesquisa do Windows.

Na interface do Server Manager, foi acessado:

```text
Manage → Add Roles and Features
```

---

## 2. Início da instalação da função

No assistente **Add Roles and Features Wizard**, foram mantidas as opções padrão e avançadas as etapas iniciais utilizando **Next**.

Na seção **Server Roles**, foi localizada a função:

```text
Active Directory Certificate Services
```

A função foi selecionada e, quando solicitado, foi utilizada a opção **Add Features**.

Depois disso, o assistente foi avançado até a configuração dos serviços da função.

---

## 3. Seleção do serviço Certification Authority

Na seção **Role Services**, foi verificado que o serviço:

```text
Certification Authority
```

estava selecionado.

A instalação foi iniciada utilizando **Install**.

Durante o processo, o Server Manager apresentou a mensagem:

```text
Installation started on DC01.aluno.hacker.com
```

A instalação foi aguardada até sua conclusão.

---

## 4. Configuração do Active Directory Certificate Services

Após a instalação da função, foi selecionada a opção:

```text
Configure Active Directory Certificate Services on the Destination server
```

Na janela **AD CS Configuration**, foi avançada a primeira etapa e selecionado o serviço:

```text
Certification Authority
```

---

## 5. Seleção do tipo de CA

No tipo de instalação, foi selecionada:

```text
Enterprise CA
```

Essa opção permite integrar a Autoridade Certificadora ao ambiente do Active Directory.

Em seguida, foi selecionada a opção:

```text
Root CA
```

Dessa forma, a autoridade configurada atua como uma CA raiz dentro da hierarquia de certificação do laboratório.

---

## 6. Criação da chave privada

Na configuração da chave privada, foi selecionada:

```text
Create a new private key
```

Foi mantido o provedor criptográfico padrão apresentado pelo laboratório:

```text
RSA 2048 bits
SHA-256
```

A chave privada gerada é utilizada pela Autoridade Certificadora para assinar os certificados emitidos por ela.

---

## 7. Configuração do nome da CA

Foi mantido o nome comum sugerido pelo ambiente:

```text
aluno-DC01-CA
```

Os demais campos foram mantidos conforme as opções padrão apresentadas pelo assistente.

Esse nome identifica a Autoridade Certificadora que posteriormente será utilizada para emissão e gerenciamento de certificados.

---

## 8. Definição da validade

A validade padrão apresentada pelo assistente era de 5 anos.

Esse período foi alterado para:

```text
10 anos
```

A configuração define o período de validade da autoridade certificadora.

---

## 9. Localização da base de dados

Foi mantida a localização padrão da base de dados da CA:

```text
C:\Windows\system32\CertLog
```

Esse diretório é utilizado pelo serviço de certificados para armazenar informações relacionadas à Autoridade Certificadora.

---

## 10. Aplicação da configuração

Após revisar o resumo das configurações, foi selecionada a opção:

```text
Configure
```

Ao término do processo, a configuração foi concluída com sucesso e o assistente apresentou o indicador de sucesso:

```text
Configuration succeeded
```

As janelas do assistente foram então fechadas.

---

## 11. Acesso à Certification Authority

No menu do Windows, foi expandida a pasta:

```text
Windows Administrative Tools
```

e selecionado:

```text
Certification Authority
```

Foi aberta a console de gerenciamento da Autoridade Certificadora.

---

## 12. Verificação da Autoridade Certificadora

Na console **Certification Authority (Local)**, foi verificada a existência da CA:

```text
aluno-DC01-CA
```

A presença dessa autoridade confirma que a função **Certification Authority** foi instalada e configurada no Windows Server 2022.

---

## Evidência — Passo 16

A evidência solicitada para a atividade corresponde ao **passo 16**, no qual deve ser apresentada a console **Certification Authority (Local)** contendo a autoridade:

```text
aluno-DC01-CA
```

**Frase obrigatória antes do print:**

> **Print da atividade 9.1:** console Certification Authority (Local) exibindo a Autoridade Certificadora `aluno-DC01-CA` configurada no Windows Server 2022.

[**Evidências — Módulo 9 / Aulas 33 e 34**](../evidencias.pdf)

---

## Conceitos aplicados

### Autoridade Certificadora

Uma **Autoridade Certificadora (CA)** é responsável por emitir e assinar certificados digitais, estabelecendo uma relação de confiança entre a identidade representada pelo certificado e sua chave pública.

### Active Directory Certificate Services

O **AD CS** é o conjunto de serviços do Windows Server utilizado para implementar uma infraestrutura de chave pública (**PKI**) no ambiente Windows.

### Enterprise CA

Uma **Enterprise CA** é integrada ao Active Directory, permitindo utilizar recursos do domínio para emissão, gerenciamento e distribuição de certificados.

### Root CA

A **Root CA** ocupa o topo de uma hierarquia de certificação. Sua chave é utilizada para assinar seu próprio certificado e, em estruturas hierárquicas, pode ser utilizada para estabelecer confiança em CAs subordinadas.

### Chave privada

A chave privada da CA é um dos componentes mais sensíveis da infraestrutura. Ela é utilizada para assinar certificados emitidos pela autoridade e deve ser protegida contra acesso não autorizado.

---

## Resultado

Foi instalada e configurada uma **Autoridade Certificadora Enterprise Root CA** no Windows Server 2022 por meio do **Active Directory Certificate Services**.

A configuração utilizou:

```text
CA:       aluno-DC01-CA
Tipo:     Enterprise CA
Hierarquia: Root CA
Chave:    RSA 2048 bits
Hash:     SHA-256
Validade: 10 anos
```

A console **Certification Authority (Local)** confirmou a presença da CA `aluno-DC01-CA`, concluindo a implementação da autoridade certificadora do laboratório.
