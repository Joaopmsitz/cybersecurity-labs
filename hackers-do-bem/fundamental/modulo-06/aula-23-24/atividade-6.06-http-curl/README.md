# Activity 6.06 — Exploring HTTP Requests and Percent-Encoding on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 06  
> **Class:** 23–24  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

This activity explores HTTP requests using the `curl` command on Kali Linux, including retrieving web page content, downloading files, and using Percent-Encoding in URL parameters.

The exercise also demonstrates how an HTML page can be retrieved directly from the terminal and subsequently opened in a web browser.

## Environment

- **Operating system:** Kali Linux
- **Access method:** RDP
- **Machine IP address:** `192.168.98.40`
- **User:** `aluno`
- **Working directory:** `/home/aluno/Documentos`

The credentials used in the laboratory are not recorded in this README.

## Procedure

### 1. Open the Terminal

After accessing Kali Linux through RDP, the terminal was opened, and administrative access was obtained:

```bash
sudo -i
```

### 2. Make an HTTP Request Using `curl`

`curl` is a command-line tool used to make requests to servers and transfer data over various protocols, including HTTP and HTTPS.

The following command was executed:

```bash
curl https://www.example.com
```

The response returned the page's HTML content:

```html
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

This demonstrates that `curl` successfully made the HTTPS request and printed the content returned by the server directly in the terminal.

### 3. Download the Content to a File

First, the Documents directory was accessed:

```bash
cd /home/aluno/Documentos
```

The directory contents were then checked:

```bash
ls
```

The directory was initially empty.

The content from `example.com` was then saved to a file using:

```bash
curl -o output.html https://www.example.com
```

**Output:**

```text
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  1256  100  1256    0     0   1805      0 --:--:-- --:--:-- --:--:--  1820
```

After the download, the following command was executed:

```bash
ls
```

**Result:**

```text
output.html
```

The `-o` option specifies the filename to which the received content will be saved.

Therefore:

```bash
curl -o output.html https://www.example.com
```

sends the request and saves the response to `output.html`.

### 4. Open the HTML File

The `output.html` file was located using Thunar at:

```text
/home/aluno/Documentos
```

When the file was opened, its contents were rendered by the Firefox browser, allowing the HTML page previously retrieved using `curl` to be viewed.

After verification, Firefox and Thunar were closed.

### 5. Use Percent-Encoding in a URL

Next, a request was made to Google using an encoded search parameter:

```bash
curl "https://www.google.com/search?q=Ol%C3%A1%2C%20mundo%21"
```

In this URL, the parameter:

```text
q=Ol%C3%A1%2C%20mundo%21
```

represents the text:

```text
Olá, mundo!
```

This encoding method is known as **Percent-Encoding**.

Some examples from the URL are:

| Encoded value | Character |
|---|---|
| `%C3%A1` | `á` |
| `%2C` | `,` |
| `%20` | Space |
| `%21` | `!` |

The `á` character is represented by the UTF-8 byte sequence `%C3%A1`.

The response returned by Google was an HTML document, demonstrating that the encoded URL was accepted by the server.

### 6. Test the Encoded URL in the Browser

The same URL used with `curl` was opened in Firefox:

```text
https://www.google.com/search?q=Ol%C3%A1%2C%20mundo%21
```

The browser displayed results corresponding to the search text:

```text
Olá, mundo!
```

This is the step specified for the activity evidence.

The objective of this step is to visually demonstrate the use of Percent-Encoding in a URL and the resulting search in the browser.

## Concepts Practiced

### HTTP

HTTP is a protocol used for communication between web clients and servers.

In this exercise, `curl` acted as a client, sending requests to HTTP/HTTPS servers and receiving their responses.

### `curl`

`curl` allows requests to be made directly from the terminal.

In this laboratory, it was used to:

- Request a web page.
- View HTML content directly in the terminal.
- Download content.
- Save a response to a file.
- Submit a URL containing encoded parameters.

### Percent-Encoding

Percent-Encoding allows certain characters to be represented in a URL through sequences beginning with the `%` character.

For example:

```text
Space → %20
,     → %2C
!     → %21
```

Characters represented using multibyte UTF-8 sequences, such as `á`, can also appear as encoded byte sequences:

```text
á → %C3%A1
```

Percent-Encoding makes it possible to represent characters in URL components while preserving the intended parameter value.

## Results

The activity demonstrated how to use `curl` to:

- Make an HTTPS request.
- Display HTML returned by a server directly in the terminal.
- Download a page to `output.html`.
- Open the downloaded content in a browser.
- Construct a URL containing Percent-Encoding.
- Perform a search using the encoded URL.

The URL used in the final test was:

```text
https://www.google.com/search?q=Ol%C3%A1%2C%20mundo%21
```

It corresponds to a search for:

```text
Olá, mundo!
```

The exercise reinforced the relationship between HTTP requests, server responses, file downloads, and URL parameter encoding.

## Cleanup

After completing the activity, the created file was checked:

```bash
ls
```

**Output:**

```text
output.html
```

The file was then removed:

```bash
rm output.html
```

## Evidence

The evidence for this activity corresponds to Step 6, showing the Percent-Encoding URL in Firefox and the search results for `Olá, mundo!`.

[View Evidence — Classes 23–24](../evidencias.pdf)

---

[Back to Classes 23–24](../) · [Back to Module 06](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
