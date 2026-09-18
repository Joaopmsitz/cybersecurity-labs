# Atividade 9.8 — Verificando Certificados Web com OCSP no Kali Linux

## Objetivo

Utilizar o OpenSSL no Kali Linux para analisar certificados digitais de servidores web e verificar informações relacionadas ao **OCSP (Online Certificate Status Protocol)** durante uma conexão TLS.

---

## Ambiente

* **Sistema:** Kali Linux
* **Ferramenta:** OpenSSL
* **Comando:** `openssl s_client`
* **Servidores analisados:** `www.grancursos.com.br` e `www.google.com`
* **Porta:** `443 (HTTPS)`

> As credenciais utilizadas para acesso ao laboratório não são registradas neste README.

---

## 1. Acesso ao terminal

Foi aberto um terminal no Kali Linux e obtido acesso administrativo com:

```bash
sudo -i
```

Em seguida, foi acessado o diretório utilizado nas atividades:

```bash
cd /home/aluno/Documentos/Arquivos
```

---

## 2. Verificação do certificado do servidor

Para estabelecer uma conexão TLS com o servidor do Gran Cursos e solicitar o status OCSP, foi executado:

```bash
openssl s_client -connect www.grancursos.com.br:443 -status
```

A opção `-connect` define o servidor e a porta utilizados na conexão, enquanto `-status` solicita ao servidor uma resposta de **OCSP stapling**, quando disponível.

Parte relevante da saída obtida:

```text
Connecting to 172.67.175.92
CONNECTED(00000003)
depth=2 C=US, O=Google Trust Services LLC, CN=GTS Root R4
verify return:1
depth=1 C=US, O=Google Trust Services, CN=WE1
verify return:1
depth=0 CN=grancursos.com.br
verify return:1
```

A cadeia de certificados foi validada durante a conexão.

---

## 3. Análise da resposta OCSP

Na saída do comando foi apresentada uma resposta OCSP:

```text
OCSP response:
======================================
OCSP Response Data:
    OCSP Response Status: successful (0x0)
    Response Type: Basic OCSP Response
    Version: 1 (0x0)
    Responder Id: 9077923567C4FFA8CCA9E67BD980797BCC93F938
    Produced At: Dec  2 17:35:25 2025 GMT
    Responses:
    Certificate ID:
      Hash Algorithm: sha1
      Issuer Name Hash: B9BED5F1A61E40B24196B0C29E7E1A9D8BFCB520
      Issuer Key Hash: 9077923567C4FFA8CCA9E67BD980797BCC93F938
      Serial Number: B57B7C7121C597FB1328D77A02E8828B
    Cert Status: good
    This Update: Dec  2 17:35:25 2025 GMT
    Next Update: Dec  9 16:35:24 2025 GMT

    Signature Algorithm: ecdsa-with-SHA256
```

O campo:

```text
Cert Status: good
```

indica que, de acordo com a resposta OCSP apresentada, o certificado consultado estava marcado como válido naquele momento.

Também foram observados os campos **This Update** e **Next Update**, que indicam o período de atualização associado à resposta.

---

## 4. Análise da cadeia e da conexão TLS

A saída também apresentou a cadeia de certificados:

```text
Certificate chain
 0 s:CN=grancursos.com.br
   i:C=US, O=Google Trust Services, CN=WE1
   a:PKEY: EC, (prime256v1); sigalg: ecdsa-with-SHA256
   v:NotBefore: Nov 27 15:16:12 2025 GMT; NotAfter: Feb 25 16:14:52 2026 GMT
 1 s:C=US, O=Google Trust Services, CN=WE1
   i:C=US, O=Google Trust Services LLC, CN=GTS Root R4
   a:PKEY: EC, (prime256v1); sigalg: ecdsa-with-SHA384
   v:NotBefore: Dec 13 09:00:00 2023 GMT; NotAfter: Feb 20 14:00:00 2029 GMT
 2 s:C=US, O=Google Trust Services LLC, CN=GTS Root R4
   i:C=BE, O=GlobalSign nv-sa, OU=Root CA, CN=GlobalSign Root CA
   a:PKEY: EC, (secp384r1); sigalg: sha256WithRSAEncryption
   v:NotBefore: Nov 15 03:43:21 2023 GMT; NotAfter: Jan 28 00:00:42 2028 GMT
```

Também foram identificados parâmetros da conexão TLS:

```text
subject=CN=grancursos.com.br
issuer=C=US, O=Google Trust Services, CN=WE1

Peer signing digest: SHA256
Peer signature type: ecdsa_secp256r1_sha256
Negotiated TLS1.3 group: X25519MLKEM768

Verification: OK

New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Protocol: TLSv1.3
Server public key is 256 bit

Verify return code: 0 (ok)
```

Essas informações permitem observar o certificado apresentado pelo servidor, sua autoridade emissora, a versão do TLS utilizada e o conjunto criptográfico negociado.

---

## 5. Verificação do OCSP no Google

Foi realizado um segundo teste utilizando o servidor do Google:

```bash
openssl s_client -connect www.google.com:443 -status
```

A saída relevante foi:

```text
Connecting to 192.178.155.106
CONNECTED(00000003)
depth=2 C=US, O=Google Trust Services LLC, CN=GTS Root R1
verify return:1
depth=1 C=US, O=Google Trust Services, CN=WR2
verify return:1
depth=0 CN=www.google.com
verify return:1
OCSP response: no response sent
```

Nesse caso, a mensagem:

```text
OCSP response: no response sent
```

indica que não foi enviada uma resposta OCSP stapled pelo servidor durante essa conexão.

---

## Evidência — Passo 5

**Frase obrigatória antes do print:**

> **Print da atividade 9.8:** resultado da conexão HTTPS com `www.google.com` utilizando `openssl s_client -status`, evidenciando a mensagem `OCSP response: no response sent`.

[**Evidências — Módulo 9 / Aulas 35 e 36**](../evidencias.pdf)

---

## Fluxo da atividade

| Etapa       | Resultado                             |
| ----------- | ------------------------------------- |
| Conexão TLS | `openssl s_client`                    |
| Consulta    | Opção `-status`                       |
| Gran Cursos | Resposta OCSP com `Cert Status: good` |
| Google      | `OCSP response: no response sent`     |

## Resultado

Foi realizada a análise de certificados HTTPS utilizando OpenSSL e `s_client`. A atividade permitiu observar tanto uma resposta OCSP com status `good` quanto uma conexão em que não foi enviada resposta OCSP stapled.
