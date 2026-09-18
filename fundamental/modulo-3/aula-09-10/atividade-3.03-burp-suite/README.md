# Atividade 3.3 — Interceptação de tráfego com Burp Suite

## Objetivo

Configurar o **Burp Suite** como proxy local para interceptar e analisar requisições HTTP/HTTPS realizadas por um navegador.

A atividade teve como foco compreender o funcionamento de um proxy de interceptação, observar requisições HTTP, analisar cabeçalhos e visualizar o tráfego gerado pelo navegador em um ambiente de laboratório controlado.

> **Escopo:** atividade realizada exclusivamente em ambiente autorizado para fins educacionais. A interceptação foi utilizada para análise do próprio tráfego gerado durante o laboratório.

## Ambiente

* Kali Linux
* Burp Suite Community Edition
* Mozilla Firefox
* Proxy local `127.0.0.1:8080`

---

## 1. Iniciando o Burp Suite

O Burp Suite foi iniciado pelo terminal:

```bash
burpsuite
```

Ao iniciar, foi apresentada a tela relacionada ao ambiente Java. Após aceitar o aviso, foi possível prosseguir para a configuração do projeto.

---

## 2. Criando um projeto temporário

Na tela inicial do Burp Suite foi selecionada a opção:

```text
Temporary Project
```

Esse modo mantém o projeto em memória durante a execução, sem criar um arquivo permanente de projeto.

Em seguida, foi selecionada a opção:

```text
Next
```

---

## 3. Utilizando as configurações padrão

Na etapa seguinte foi selecionada a opção para utilizar as configurações padrão do Burp Suite:

```text
Use Burp defaults
```

Depois foi iniciado o ambiente através de:

```text
Start Burp
```

Após o carregamento, a interface principal do Burp Suite foi disponibilizada.

---

## 4. Verificando o estado do Intercept

Na aba:

```text
Proxy → Intercept
```

foi verificado que a interceptação estava inicialmente desativada:

```text
Intercept is off
```

Esse estado permite que o navegador utilize o proxy sem que cada requisição fique pausada aguardando uma ação manual.

---

## 5. Verificando o listener do proxy

Em:

```text
Proxy → Proxy settings
```

foi verificada a configuração do listener utilizado pelo Burp Suite.

O listener estava configurado para:

```text
127.0.0.1:8080
```

Essa configuração significa que o Burp Suite aguardava conexões locais na porta `8080`.

### Conceito

O endereço `127.0.0.1` representa a própria máquina, também conhecido como **localhost**.

Dessa forma, o Firefox e o Burp Suite podem se comunicar localmente através da porta `8080`.

---

## 6. Testando a comunicação com o Burp

No Firefox foi acessado:

```text
http://burp
```

Inicialmente, a página não foi carregada porque o navegador ainda não estava configurado para utilizar o proxy do Burp Suite.

---

## 7. Acessando as configurações de proxy do Firefox

No Firefox foi acessado:

```text
Settings → Network Settings
```

Na configuração de conexão, foi selecionada a opção de configuração manual do proxy.

---

## 8. Configurando o endereço do proxy

No campo correspondente ao proxy HTTP foi configurado:

```text
HTTP Proxy: 127.0.0.1
```

---

## 9. Configurando a porta

A porta utilizada pelo Burp Suite foi definida como:

```text
Port: 8080
```

A configuração também foi aplicada às conexões HTTPS.

Assim, o fluxo passou a ser:

```text
Firefox
   ↓
127.0.0.1:8080
   ↓
Burp Suite
   ↓
Internet
```

---

## 10. Acessando novamente o endereço do Burp

Após configurar o proxy, o endereço abaixo foi acessado novamente:

```text
http://burp
```

A página do Burp Suite foi carregada no navegador.

Ela apresentou a interface:

```text
Burp Suite Community Edition
```

---

## 11. Obtendo o certificado da CA

Para permitir a análise de conexões HTTPS pelo proxy, foi acessado o endereço do Burp:

```text
http://burp
```

e selecionada a opção para obter o certificado da autoridade certificadora do Burp Suite.

O arquivo disponibilizado foi:

```text
cacert.der
```

Esse certificado é utilizado pelo Burp para estabelecer conexões HTTPS que possam ser analisadas localmente.

---

## 12. Abrindo o gerenciador de certificados do Firefox

No Firefox foi acessado:

```text
Settings → Privacy & Security
```

e posteriormente:

```text
View Certificates
```

Foi aberta a área responsável pelo gerenciamento das autoridades certificadoras confiáveis.

---

## 13. Importando o certificado

O arquivo:

```text
cacert.der
```

foi selecionado para importação.

Durante a importação, o Firefox apresentou as opções relacionadas à confiança da autoridade certificadora.

---

## 14. Concedendo confiança ao certificado

O certificado foi configurado para ser confiável nas finalidades necessárias para o laboratório, incluindo:

```text
Trust this CA to identify websites
```

e, conforme apresentado no ambiente:

```text
Trust this CA to identify email users
```

```text
Trust this CA to identify software developers
```

Após a confirmação, o certificado passou a ser reconhecido pelo Firefox.

### Conceito

Em conexões HTTPS, o certificado permite que o navegador valide a identidade do servidor.

Em um laboratório de interceptação, o Burp atua como intermediário e utiliza sua própria CA para gerar certificados locais para os domínios acessados. Por isso, a CA do Burp precisa ser explicitamente confiada pelo navegador de laboratório.

---

## 15. Retornando ao Burp Suite

Após concluir a configuração do certificado, foi retornada a janela principal do Burp Suite.

O proxy já estava configurado para receber as requisições provenientes do Firefox.

---

## 16. Ativando a interceptação

Na área:

```text
Proxy → Intercept
```

a interceptação foi ativada:

```text
Intercept is on
```

A partir desse momento, as requisições feitas pelo Firefox poderiam ser pausadas pelo Burp antes de serem encaminhadas ao destino.

---

## 17. Acessando um site através do proxy

Com a interceptação ativada, o Firefox foi utilizado para acessar:

```text
https://casasbahia.com.br/
```

A requisição passou pelo proxy local configurado anteriormente.

---

## 18. Observando a requisição interceptada

O Burp Suite interceptou a comunicação e a requisição ficou aguardando encaminhamento.

Como consequência, o carregamento da página no Firefox ficou interrompido enquanto a requisição permanecia em estado de interceptação.

Esse comportamento demonstra uma das principais funções do Burp Suite: permitir que o analista visualize uma requisição antes que ela continue para o servidor.

---

## 19. Analisando os cabeçalhos HTTP

Na requisição interceptada foram observadas informações como:

```text
Host
Cookie
User-Agent
```

Esses campos fazem parte dos cabeçalhos HTTP enviados pelo navegador.

### Host

Indica o servidor/domínio para o qual a requisição está sendo direcionada.

### Cookie

Pode conter informações utilizadas pelo site para manter estado de sessão, preferências ou outras informações associadas ao navegador.

> Durante uma análise real, cookies podem conter informações sensíveis e tokens de sessão. Por isso, não devem ser compartilhados ou registrados fora de um ambiente autorizado.

### User-Agent

Identifica características do cliente utilizado para realizar a requisição, como navegador e sistema operacional.

---

## 20. Consultando o HTTP History

O Burp Suite mantém um histórico das requisições que passaram pelo proxy.

Foi acessado:

```text
Proxy → HTTP history
```

O histórico apresentou as requisições realizadas pelo navegador, permitindo analisar individualmente informações como:

* método HTTP;
* URL;
* domínio;
* caminho;
* status HTTP;
* parâmetros;
* cabeçalhos;
* conteúdo das requisições e respostas.

Essa funcionalidade é particularmente útil para compreender como uma aplicação web se comunica com seus servidores.

---

## 21. Evidência — HTTP History

A evidência da atividade foi registrada mostrando o **HTTP History** do Burp Suite com as requisições interceptadas durante o laboratório.

O print deve mostrar a interface completa e legível, conforme as regras de evidência do módulo.

---

## 22. Encaminhando as requisições

Com a requisição interceptada, foi utilizada a opção:

```text
Forward
```

para encaminhá-la ao destino.

Dependendo da quantidade de requisições geradas pelo navegador, foi necessário utilizar o botão `Forward` diversas vezes para permitir a continuidade do carregamento.

Esse processo demonstra o funcionamento do modo de interceptação:

```text
Firefox
   ↓
Burp Suite
   ↓
[Intercept]
   ↓
Forward
   ↓
Servidor
```

---

## 23. Verificando o carregamento da página

Após encaminhar as requisições necessárias, a página acessada no Firefox pôde continuar seu carregamento normalmente.

Isso confirmou que o navegador estava efetivamente passando pelo proxy configurado no Burp Suite.

---

## 24. Desativando o proxy

Ao finalizar o exercício, a configuração de proxy do Firefox foi restaurada para:

```text
No Proxy
```

Essa etapa é importante para evitar que o navegador continue utilizando o proxy local do laboratório após a atividade.

O Burp Suite e o Firefox foram então encerrados.

---

## Conceitos praticados

* Burp Suite
* Proxy de interceptação
* HTTP/HTTPS
* Proxy local
* `127.0.0.1`
* Porta `8080`
* HTTP History
* Intercept
* Forward
* HTTP Headers
* `Host`
* `Cookie`
* `User-Agent`
* Certificado digital
* Certificate Authority (CA)
* Inspeção de tráfego web

## Fluxo observado

O laboratório permitiu visualizar na prática o caminho percorrido por uma requisição web:

```text
Firefox
   │
   │ Requisição HTTP/HTTPS
   ▼
Burp Suite
   │
   │ Intercept
   ▼
Análise da requisição
   │
   │ Forward
   ▼
Servidor web
   │
   │ Resposta
   ▼
Burp Suite
   │
   ▼
Firefox
```

## Resultado

A atividade permitiu configurar o Burp Suite como proxy local do Firefox, instalar a CA do laboratório, interceptar requisições HTTP/HTTPS e analisar informações presentes nos cabeçalhos e no histórico HTTP.

O exercício também demonstrou a diferença entre simplesmente navegar por uma aplicação web e observar tecnicamente as requisições que o navegador realiza durante essa navegação.

## Evidência

[**Evidências — Módulo 3 / Aulas 9 e 10**](../evidencias.pdf)
