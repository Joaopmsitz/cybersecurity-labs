# Atividade 6.6 — Explorando Solicitações HTTP e Codificação Percentual no Kali Linux

## Objetivo

Nesta atividade foram exploradas solicitações HTTP utilizando o comando `curl` no Kali Linux, incluindo a obtenção de conteúdo de páginas web, download de arquivos e utilização de **codificação percentual (Percent-Encoding)** em parâmetros de uma URL.

O exercício também demonstrou como uma página HTML pode ser obtida diretamente pelo terminal e posteriormente aberta no navegador.

---

## Ambiente

* **Sistema:** Kali Linux
* **Acesso:** RDP
* **IP da máquina:** `192.168.98.40`
* **Usuário:** `aluno`
* **Diretório de trabalho:** `/home/aluno/Documentos`

> As credenciais utilizadas no laboratório não são registradas neste documento.

---

## 1. Acessando o terminal

Após acessar o Kali Linux por RDP, foi aberto o terminal e obtido acesso administrativo:

```bash
sudo -i
```

---

## 2. Realizando uma solicitação HTTP com `curl`

O `curl` é uma ferramenta de linha de comando utilizada para realizar solicitações a servidores e transferir dados através de diversos protocolos, incluindo HTTP e HTTPS.

Foi executado:

```bash
curl https://www.example.com
```

A resposta retornou o conteúdo HTML da página:

```text
<!doctype html>
<html>
<head>
    <title>Example Domain</title>

    <meta charset="utf-8" />
    <meta http-equiv="Content-type" content="text/html; charset=utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <style type="text/css">
    body {
        background-color: #f0f0f2;
        margin: 0;
        padding: 0;
        font-family: -apple-system, system-ui, BlinkMacSystemFont, "Segoe UI", "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
        
    }
    div {
        width: 600px;
        margin: 5em auto;
        padding: 2em;
        background-color: #fdfdff;
        border-radius: 0.5em;
        box-shadow: 2px 3px 7px 2px rgba(0,0,0,0.02);
    }
    a:link, a:visited {
        color: #38488f;
        text-decoration: none;
    }
    @media (max-width: 700px) {
        div {
            margin: 0 auto;
            width: auto;
        }
    }
    </style>    
</head>

<body>
<div>
    <h1>Example Domain</h1>
    <p>This domain is for use in illustrative examples in documents. You may use this
    domain in literature without prior coordination or asking for permission.</p>
    <p><a href="https://www.iana.org/domains/example">More information...</a></p>
</div>
</body>
</html>
```

Isso demonstra que o `curl` conseguiu realizar a solicitação HTTPS e imprimir no terminal o conteúdo retornado pelo servidor.

---

## 3. Baixando o conteúdo para um arquivo

Primeiramente, foi acessado o diretório `Documentos`:

```bash
cd /home/aluno/Documentos
```

Em seguida, foi verificado o conteúdo:

```bash
ls
```

O diretório estava inicialmente vazio.

O conteúdo de `example.com` foi então salvo em um arquivo utilizando:

```bash
curl -o output.html https://www.example.com
```

Saída:

```text
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  1256  100  1256    0     0   1805      0 --:--:-- --:--:-- --:--:--  1820
```

Após o download:

```bash
ls
```

Resultado:

```text
output.html
```

A opção `-o` define o nome do arquivo no qual o conteúdo recebido será salvo.

Portanto:

```bash
curl -o output.html https://www.example.com
```

realiza a requisição e grava a resposta em `output.html`.

---

## 4. Abrindo o arquivo HTML

O arquivo `output.html` foi localizado através do Thunar em:

```text
/home/aluno/Documentos
```

Ao abrir o arquivo, seu conteúdo foi interpretado pelo navegador Firefox, permitindo visualizar a página HTML obtida anteriormente através do `curl`.

Após a verificação, o Firefox e o Thunar foram fechados.

---

## 5. Utilizando codificação percentual em uma URL

Em seguida, foi realizada uma solicitação ao Google utilizando um parâmetro de pesquisa codificado:

```bash
curl "https://www.google.com/search?q=Ol%C3%A1%2C%20mundo%21"
```

Nesse endereço, o parâmetro:

```text
q=Ol%C3%A1%2C%20mundo%21
```

representa o texto:

```text
Olá, mundo!
```

A codificação utilizada é conhecida como **Percent-Encoding** ou codificação percentual.

Alguns exemplos presentes na URL:

| Código   | Caractere |
| -------- | --------- |
| `%C3%A1` | `á`       |
| `%2C`    | `,`       |
| `%20`    | espaço    |
| `%21`    | `!`       |

A resposta retornada pelo Google foi um documento HTML, demonstrando que a URL codificada foi aceita pelo servidor.

---

## 6. Testando a URL codificada no navegador

A mesma URL utilizada no `curl` foi aberta no Firefox:

```text
https://www.google.com/search?q=Ol%C3%A1%2C%20mundo%21
```

O navegador apresentou o resultado correspondente à pesquisa pelo texto:

```text
Olá, mundo!
```

**Este é o passo solicitado para a evidência da atividade.**

O objetivo desse passo é demonstrar visualmente a utilização da codificação percentual em uma URL e o resultado obtido pelo navegador.

---

## Conceitos envolvidos

### HTTP

HTTP é um protocolo utilizado para comunicação entre clientes e servidores web.

No exercício, o `curl` atuou como cliente, enviando solicitações para servidores HTTP/HTTPS e recebendo suas respostas.

### `curl`

O `curl` permite realizar requisições diretamente pelo terminal.

No laboratório foi utilizado para:

```text
Solicitar uma página web
Baixar conteúdo
Salvar uma resposta em arquivo
Enviar uma URL com parâmetros codificados
```

### Codificação percentual

A codificação percentual permite representar determinados caracteres dentro de uma URL através de sequências iniciadas pelo caractere `%`.

Por exemplo:

```text
espaço → %20
,      → %2C
!      → %21
```

Caracteres que possuem representação específica em UTF-8, como `á`, também podem aparecer como uma sequência de bytes codificados:

```text
á → %C3%A1
```

---

## Resultado

A atividade permitiu utilizar o `curl` para:

1. realizar uma requisição HTTPS;
2. visualizar diretamente o HTML retornado por um servidor;
3. baixar uma página para `output.html`;
4. abrir o conteúdo baixado no navegador;
5. construir uma URL contendo parâmetros em Percent-Encoding;
6. realizar uma pesquisa utilizando a URL codificada.

A URL utilizada no teste final foi:

```text
https://www.google.com/search?q=Ol%C3%A1%2C%20mundo%21
```

e corresponde à pesquisa por:

```text
Olá, mundo!
```

---

## Limpeza

Após a conclusão da atividade, o arquivo criado foi removido:

```bash
ls
```

Saída:

```text
output.html
```

Em seguida:

```bash
rm output.html
```

---

## Evidência

A evidência desta atividade corresponde ao **passo 6**, mostrando no Firefox a URL com codificação percentual e o resultado da pesquisa por `Olá, mundo!`.

[**Evidências — Módulo 6 / Aulas 3 e 4**](../evidencias.pdf)
