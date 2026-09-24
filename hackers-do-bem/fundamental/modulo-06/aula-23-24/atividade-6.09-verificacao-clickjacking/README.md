# Atividade 6.9 — Verificando Sites com Vulnerabilidade ao Clickjacking

## Objetivo

Nesta atividade foi utilizado o serviço **Clickjacker** para verificar as proteções contra Clickjacking configuradas em diferentes sites.

Foram analisados principalmente os cabeçalhos HTTP:

* `X-Frame-Options`;
* `Content-Security-Policy`, especificamente a diretiva `frame-ancestors`.

O objetivo foi comparar as configurações apresentadas pelo serviço e identificar se os sites possuíam mecanismos de proteção contra incorporação em `iframe`.

---

## Ambiente

* **Sistema:** computador local
* **Navegador:** navegador web
* **Serviço utilizado:** Clickjacker
* **URL:** `https://clickjacker.io/`

> Nesta atividade foi utilizado o computador local, e não a máquina virtual da AWS.

---

## 1. Acessando o Clickjacker

O navegador foi aberto e acessado o endereço:

```text
https://clickjacker.io/
```

A página disponibiliza um campo para informar o site que será analisado e apresenta informações relacionadas às proteções contra Clickjacking.

Entre os dados apresentados estão:

* **IP Address:** endereço IP associado ao site analisado;
* **Time:** horário em que o teste foi realizado;
* **X-Frame-Options:** cabeçalho HTTP utilizado para controlar a possibilidade de uma página ser carregada em `frame` ou `iframe`;
* **CSP Header (Frame-Ancestors):** configuração da diretiva `frame-ancestors` da Content Security Policy.

---

## 2. Entendendo os mecanismos de proteção

### X-Frame-Options

O cabeçalho `X-Frame-Options` controla se uma página pode ser incorporada em um `frame` ou `iframe`.

Entre os valores relevantes estão:

```text
DENY
```

Impede que a página seja incorporada em frames.

```text
SAMEORIGIN
```

Permite a incorporação somente quando a origem do conteúdo incorporado corresponde à origem permitida.

A ausência desse cabeçalho não significa, isoladamente, que um site seja vulnerável, pois outras políticas, principalmente CSP, também podem fornecer proteção.

### CSP — frame-ancestors

A diretiva:

```text
frame-ancestors
```

faz parte da **Content Security Policy (CSP)** e permite definir quais origens podem incorporar uma página em `frame` ou `iframe`.

Essa política pode fornecer uma camada adicional de proteção contra Clickjacking.

---

## 3. Testando o site esr.rnp.br

No campo **Test for Clickjacking now**, foi informado:

```text
esr.rnp.br
```

O teste apresentou:

```text
Test Results:
Site:
https://esr.rnp.br
IP Address:	177.136.78.45
Time:	Tue Sep 30 2025 00:35:08 GMT+0000 (Coordinated Universal Time)
X-Frame-Options: SAMEORIGIN
CSP Header (Frame-Ancestors)	Missing anti-framing policy
```

O resultado mostra que o site apresentava:

```text
X-Frame-Options: SAMEORIGIN
```

Isso restringe a incorporação da página a uma determinada relação de origem.

Embora o resultado do campo CSP informe:

```text
Missing anti-framing policy
```

a presença de `X-Frame-Options: SAMEORIGIN` já representa um mecanismo de proteção contra incorporação indevida em frames.

Portanto, a ausência da diretiva `frame-ancestors` não deve ser interpretada isoladamente como comprovação de vulnerabilidade.

---

## 4. Testando o site [www.hackthissite.org](http://www.hackthissite.org)

Em seguida, foi realizado o teste com:

```text
www.hackthissite.org
```

O resultado apresentado pelo Clickjacker foi:

```text
Test Results:
Site:	
https://www.hackthissite.org
IP Address:	137.74.187.100
Time:	Tue Sep 30 2025 00:37:18 GMT+0000 (Coordinated Universal Time)
X-Frame-Options:	Missing header
CSP Header (Frame-Ancestors)	Missing anti-framing policy
Total scans so far: 3,548,984
```

Nesse resultado, o serviço informou:

```text
X-Frame-Options: Missing header
```

e:

```text
CSP Header (Frame-Ancestors): Missing anti-framing policy
```

Ou seja, o teste não identificou um `X-Frame-Options` nem uma política `frame-ancestors` utilizada para restringir a incorporação da página.

De acordo com a interpretação apresentada pelo laboratório, essa configuração caracteriza o site como vulnerável ao Clickjacking.

É importante diferenciar a ausência desses mecanismos de uma exploração efetivamente realizada: o teste verifica as políticas de proteção apresentadas pelo site, não executa um ataque contra usuários.

**Este é o passo solicitado para a evidência da atividade.**

---

## Comparação dos resultados

| Site                   | X-Frame-Options | CSP `frame-ancestors` | Resultado observado                                       |
| ---------------------- | --------------- | --------------------- | --------------------------------------------------------- |
| `esr.rnp.br`           | `SAMEORIGIN`    | Ausente               | Possui proteção por `X-Frame-Options`                     |
| `www.hackthissite.org` | Ausente         | Ausente               | Sem essas políticas anti-framing identificadas pelo teste |

A comparação demonstra a importância de analisar os mecanismos de proteção em conjunto.

No primeiro caso, mesmo sem uma política `frame-ancestors`, havia uma política `X-Frame-Options: SAMEORIGIN`.

No segundo caso, o serviço não identificou nenhum dos dois mecanismos.

---

## Conceitos envolvidos

### Clickjacking

Clickjacking é uma técnica que pode utilizar elementos sobrepostos ou conteúdo incorporado para induzir o usuário a realizar uma ação diferente daquela que acredita estar executando.

Uma das formas de mitigação é impedir que páginas sejam incorporadas em frames de origens não autorizadas.

### X-Frame-Options

É um cabeçalho HTTP utilizado para controlar a possibilidade de uma página ser carregada dentro de `frame` ou `iframe`.

No laboratório foram observados dois cenários:

```text
SAMEORIGIN
```

e:

```text
Missing header
```

### Content Security Policy

A CSP permite estabelecer políticas de segurança para diferentes tipos de conteúdo.

A diretiva:

```text
frame-ancestors
```

especifica quais origens podem incorporar a página em frames.

### Anti-framing

Uma política anti-framing restringe a possibilidade de uma página ser incorporada por outras páginas.

Essas políticas são importantes para reduzir o risco de ataques baseados em Clickjacking.

---

## Resultado

Foram analisados dois sites utilizando o Clickjacker.

No primeiro:

```text
esr.rnp.br
```

foi identificado:

```text
X-Frame-Options: SAMEORIGIN
```

No segundo:

```text
www.hackthissite.org
```

o serviço informou ausência de:

```text
X-Frame-Options
```

e:

```text
CSP Header (Frame-Ancestors)
```

A atividade permitiu compreender como cabeçalhos HTTP e políticas CSP podem ser utilizados para identificar e mitigar riscos relacionados à incorporação de páginas em `iframe`.

---

## Evidência

A evidência desta atividade corresponde ao **passo 4**, no qual foi realizado o teste de `www.hackthissite.org` e apresentados os resultados de `X-Frame-Options` e `CSP Header (Frame-Ancestors)`.

[**Evidências — Módulo 6 / Aulas 3 e 4**](../evidencias.pdf)

