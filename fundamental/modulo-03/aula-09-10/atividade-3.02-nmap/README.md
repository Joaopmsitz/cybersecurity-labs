# Atividade 3.3 — Burp Suite

## Objetivo

Configurar o **Burp Suite** como proxy local para interceptar e analisar requisições HTTP/HTTPS realizadas pelo navegador em um ambiente de laboratório controlado.

A atividade demonstra como o tráfego do navegador pode passar por um proxy local, permitindo visualizar requisições, cabeçalhos e outros elementos da comunicação HTTP.

---

## Ambiente

* **Sistema:** Kali Linux
* **Ferramenta:** Burp Suite Community Edition
* **Navegador:** Mozilla Firefox
* **Proxy:** `127.0.0.1:8080`
* **Ambiente:** laboratório controlado

---

## 1. Inicialização do Burp Suite

No terminal, foi executado:

```bash id="1r2y6v"
burpsuite
```

Na tela inicial do Burp Suite foi selecionada a opção:

**Temporary Project**

Em seguida:

**Next → Use Burp defaults → Start Burp**

O Burp Suite foi então iniciado com as configurações padrão.

---

## 2. Verificação do Proxy

Após iniciar o programa, foi acessada a área:

**Proxy → Intercept**

Inicialmente, a interceptação estava desativada:

**Intercept is off**

A configuração foi mantida dessa forma durante a preparação do navegador.

---

## 3. Verificação do listener

Em:

**Proxy → Proxy settings**

foi verificado o listener utilizado pelo Burp Suite.

A configuração utilizada foi:

```text
127.0.0.1:8080
```

Esse listener permite que aplicações locais, como o Firefox, encaminhem suas requisições HTTP para o Burp Suite.

---

## 4. Teste inicial no navegador

No Firefox, foi acessado:

```text
http://burp
```

Nesse momento, o navegador ainda não estava configurado para utilizar o Burp Suite como proxy, portanto a página não foi carregada como esperado.

Isso confirmou que ainda era necessário configurar o proxy manualmente no Firefox.

---

## 5. Configuração do proxy no Firefox

No Firefox foi acessado:

**Settings → Network Settings → Settings**

Foi selecionada a opção:

**Manual proxy configuration**

Os valores configurados foram:

```text
HTTP Proxy: 127.0.0.1
Port: 8080
```

Também foi habilitada a opção para utilizar essa configuração para conexões HTTPS.

A configuração permitiu que o tráfego do navegador fosse encaminhado para o listener local do Burp Suite.

---

## 6. Teste de comunicação com o Burp

Após configurar o proxy, foi acessado novamente:

```text
http://burp
```

Dessa vez, a página do Burp Suite foi disponibilizada pelo proxy local.

Foi possível visualizar a página:

```text
Burp Suite Community Edition
```

Isso confirmou que o Firefox estava se comunicando com o Burp Suite através de:

```text
127.0.0.1:8080
```

---

## 7. Download do certificado CA

Para permitir a análise de conexões HTTPS, foi acessado novamente:

```text
http://burp
```

Na página do Burp Suite foi realizado o download do certificado:

```text
cacert.der
```

Esse certificado é utilizado pelo Burp Suite para atuar como uma autoridade certificadora local durante a inspeção HTTPS no ambiente de laboratório.

---

## 8. Importação do certificado no Firefox

No Firefox foi acessado:

**Settings → Privacy & Security → Certificates → View Certificates**

Na janela de certificados, foi utilizada a opção:

**Import**

e selecionado o arquivo:

```text
cacert.der
```

Durante a importação, foi habilitada a confiança necessária para que o certificado pudesse ser utilizado para identificar sites durante a análise de conexões HTTPS.

---

## 9. Ativação da interceptação

Após a configuração do certificado, foi retornado ao Burp Suite:

**Proxy → Intercept**

A opção foi alterada para:

**Intercept is on**

Com isso, as requisições realizadas pelo Firefox passaram a ser interceptadas pelo Burp Suite antes de serem encaminhadas ao servidor.

---

## 10. Acesso ao site de teste

Com o proxy configurado e a interceptação ativada, foi acessado pelo Firefox:

```text
https://casasbahia.com.br/
```

A requisição foi interceptada pelo Burp Suite.

Nesse momento, o navegador permaneceu aguardando enquanto a requisição estava sendo analisada no proxy.

---

## 11. Análise da requisição interceptada

Na tela de interceptação foi possível visualizar informações da requisição HTTP, incluindo cabeçalhos como:

```text
Host:
Cookie:
User-Agent:
```

Esses campos permitem identificar diferentes informações relacionadas à comunicação entre o navegador e o servidor.

### Host

Indica o domínio para o qual a requisição está sendo direcionada.

### Cookie

Pode transportar informações armazenadas pelo navegador e associadas à sessão ou ao funcionamento do site.

### User-Agent

Identifica características do cliente que está realizando a requisição, como navegador e sistema operacional.

---

## 12. HTTP History

Além da interceptação em tempo real, foi acessada a seção:

**Proxy → HTTP history**

Essa área apresenta o histórico das requisições observadas pelo Burp Suite.

Foi possível visualizar as requisições realizadas pelo navegador, seus métodos HTTP, URLs, códigos de resposta e outras informações relacionadas ao tráfego.

---

## 13. Evidência da atividade

A evidência solicitada pelo roteiro corresponde ao **passo 21**, mostrando o histórico HTTP no Burp Suite com as requisições interceptadas.

A captura foi realizada com a janela do Burp Suite em tela cheia, conforme as orientações do laboratório.

---

## 14. Encaminhamento das requisições

Após analisar as requisições, foi utilizada a opção:

**Forward**

para encaminhá-las ao destino.

Como algumas páginas realizam diversas requisições, foi necessário utilizar o **Forward** várias vezes para permitir que o carregamento continuasse.

Depois que as requisições foram encaminhadas, a página conseguiu continuar seu carregamento normalmente.

---

## 15. Restauração da configuração do Firefox

Após finalizar a análise, o proxy manual configurado no Firefox foi removido.

A configuração de rede foi restaurada para:

**No Proxy**

Essa etapa é importante para que o navegador não continue dependendo do Burp Suite para realizar conexões depois do término do laboratório.

---

## Conceitos praticados

### Proxy

Um proxy atua como intermediário entre o cliente e o servidor. Neste laboratório, o Burp Suite foi utilizado como proxy local para permitir a inspeção do tráfego gerado pelo navegador.

### Loopback

O endereço:

```text
127.0.0.1
```

representa a própria máquina. O Burp Suite utilizou esse endereço para disponibilizar seu listener local.

### Porta 8080

A porta:

```text
8080
```

foi utilizada pelo listener HTTP do Burp Suite.

### Intercept

A função **Intercept** permite pausar uma requisição antes que ela seja encaminhada ao destino, possibilitando sua análise.

### Forward

A função **Forward** libera uma requisição interceptada para que ela continue seu caminho até o servidor.

### HTTP History

O **HTTP History** registra as requisições observadas pelo Burp Suite, permitindo analisar posteriormente o tráfego gerado pelo navegador.

### HTTPS e certificado CA

O HTTPS utiliza TLS para proteger a comunicação. Para que o Burp pudesse realizar a inspeção HTTPS no ambiente de laboratório, seu certificado CA foi instalado e confiado pelo Firefox.

### Headers HTTP

Os cabeçalhos fazem parte das requisições e respostas HTTP e transportam informações utilizadas pelo cliente e pelo servidor durante a comunicação.

---

## Resultado

A atividade permitiu configurar o Burp Suite como um proxy local e acompanhar, de forma prática, o fluxo de uma requisição realizada pelo navegador.

Durante o exercício foi possível:

1. iniciar o Burp Suite;
2. verificar o listener local;
3. configurar o Firefox para utilizar `127.0.0.1:8080`;
4. instalar o certificado CA do Burp;
5. interceptar uma requisição HTTPS;
6. analisar cabeçalhos HTTP;
7. consultar o HTTP History;
8. encaminhar as requisições com **Forward**;
9. restaurar a configuração original do navegador.

O laboratório demonstrou na prática como um proxy de interceptação pode ser utilizado para **análise de tráfego HTTP/HTTPS em um ambiente controlado**.

---

## Evidência

[**Evidências — Módulo 3 / Aulas 9 e 10**](../evidencias.pdf)

**Print registrado:** etapa 21 da atividade, conforme solicitado pelo roteiro.
