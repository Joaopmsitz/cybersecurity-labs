# Atividade 9.6 — Revogando um Certificado no Windows Server 2022

## Objetivo

Revogar um certificado digital previamente emitido pela Autoridade Certificadora do Windows Server 2022, utilizando a console **Certification Authority**.

Como pré-requisito, foram consideradas as atividades anteriores de criação da CA e emissão do certificado.

---

## Ambiente

* **Sistema:** Windows Server 2022
* **Serviço:** Active Directory Certificate Services (AD CS)
* **Autoridade Certificadora:** `aluno-DC01-CA`
* **Console:** Certification Authority

> As credenciais utilizadas para acesso ao laboratório não são registradas neste README.

---

## 1. Acesso ao Server Manager

Foi aberto o campo de pesquisa do Windows e pesquisado:

```text
Server Manager
```

Em seguida, o **Server Manager** foi aberto.

---

## 2. Acesso à Certification Authority

No Server Manager, foi acessado:

```text
Tools → Certification Authority
```

A console de gerenciamento da Autoridade Certificadora foi aberta.

---

## 3. Visualização dos certificados emitidos

Na coluna esquerda da janela, foi expandida a autoridade:

```text
aluno-DC01-CA
```

Em seguida, foi selecionada a pasta:

```text
Issued Certificates
```

Essa seção apresenta os certificados que foram emitidos pela Autoridade Certificadora.

---

## 4. Seleção do certificado

Na coluna da direita, foi selecionado o primeiro certificado da lista.

Com o botão direito sobre o certificado, foram acessadas as opções:

```text
All Tasks → Revoke Certificate
```

---

## 5. Escolha do motivo da revogação

Na janela de revogação foi selecionado o motivo:

```text
Certificate Hold
```

Essa opção representa a suspensão temporária do certificado.

A operação foi confirmada utilizando:

```text
Yes
```

Com isso, o certificado foi revogado pela Autoridade Certificadora.

---

## 6. Verificação após a revogação

Após a operação, a pasta:

```text
Issued Certificates
```

foi novamente selecionada.

O certificado revogado deixou de aparecer nessa lista, demonstrando que a revogação foi processada pela Autoridade Certificadora.

---

## Evidência — Passo 6

**Frase obrigatória antes do print:**

> **Print da atividade 9.6:** pasta `Issued Certificates` após a revogação do certificado, demonstrando a alteração na lista de certificados emitidos.

[**Evidências — Módulo 9 / Aulas 35 e 36**](../evidencias.pdf)

---

## Fluxo da atividade

| Etapa       | Resultado             |
| ----------- | --------------------- |
| Localização | `Issued Certificates` |
| Ação        | `Revoke Certificate`  |
| Motivo      | `Certificate Hold`    |
| Resultado   | Certificado revogado  |

## Resultado

O certificado previamente emitido pela `aluno-DC01-CA` foi revogado utilizando a console **Certification Authority**.
