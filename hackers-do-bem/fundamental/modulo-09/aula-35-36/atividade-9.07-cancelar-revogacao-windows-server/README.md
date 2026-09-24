# Atividade 9.7 — Cancelar a Revogação de um Certificado no Windows Server 2022

## Objetivo

Cancelar a revogação de um certificado anteriormente revogado na Autoridade Certificadora do Windows Server 2022, retornando o certificado à lista de certificados emitidos.

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

```text id="b4h7xp"
Server Manager
```

Em seguida, o **Server Manager** foi aberto.

---

## 2. Acesso à Certification Authority

No Server Manager, foi acessado:

```text id="j7g5zs"
Tools → Certification Authority
```

A console de gerenciamento da Autoridade Certificadora foi aberta.

---

## 3. Acesso aos certificados revogados

Na coluna esquerda, foi expandida a autoridade:

```text id="e3m2xq"
aluno-DC01-CA
```

Em seguida, foi selecionada:

```text id="8p4wkt"
Revoked Certificates
```

Essa pasta apresenta os certificados que foram revogados pela Autoridade Certificadora.

---

## 4. Visualização do certificado

Na coluna da direita, foi localizado o certificado revogado na atividade anterior.

O certificado foi aberto com duplo clique para visualizar as abas:

```text id="7s6j2c"
General
Details
Path
```

Após a análise das informações, foi selecionado **OK**.

---

## 5. Visualização de atributos e extensões

Com o botão direito sobre o certificado, foram acessadas as opções:

```text id="1v8n5d"
All Tasks → View Attributes/Extensions...
```

Na janela aberta foram verificadas as abas:

```text id="9y0x4f"
Attributes
Extensions
```

Essas seções apresentam os atributos e extensões associados ao certificado.

Após a análise, foi selecionado **OK**.

---

## 6. Cancelamento da revogação

Com o certificado selecionado, foi utilizado o botão direito e acessado:

```text id="q2k6rv"
All Tasks → Unrevoke Certificate
```

A opção **Unrevoke Certificate** cancela a revogação registrada para o certificado.

---

## 7. Verificação em Revoked Certificates

Após a operação, foi verificada novamente a pasta:

```text id="w5m9ca"
Revoked Certificates
```

O certificado deixou de aparecer nessa lista.

---

## 8. Acesso aos certificados emitidos

Na coluna esquerda da console, foi selecionada:

```text id="4c8v2m"
Issued Certificates
```

---

## 9. Verificação do certificado

Na pasta **Issued Certificates**, foi localizado novamente o certificado cuja revogação havia sido cancelada.

Isso demonstra que o certificado retornou à lista de certificados emitidos após a operação de **Unrevoke Certificate**.

---

## Evidência — Passo 9

**Frase obrigatória antes do print:**

> **Print da atividade 9.7:** certificado com a revogação cancelada novamente presente na pasta `Issued Certificates` da Autoridade Certificadora.

[**Evidências — Módulo 9 / Aulas 35 e 36**](../evidencias.pdf)

---

## Fluxo da atividade

| Etapa           | Resultado                            |
| --------------- | ------------------------------------ |
| Certificado     | Localizado em `Revoked Certificates` |
| Ação            | `Unrevoke Certificate`               |
| Verificação     | Removido de `Revoked Certificates`   |
| Resultado final | Retornado para `Issued Certificates` |

## Resultado

A revogação do certificado foi cancelada com sucesso, fazendo com que ele voltasse a aparecer na pasta **Issued Certificates** da `aluno-DC01-CA`.
