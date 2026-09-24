# Atividade 3.5 — Ncat: Redirecionamento de Portas

## Objetivo

Utilizar o **Ncat**, ferramenta integrante do Nmap, para observar o encaminhamento de dados entre conexões TCP utilizando diferentes portas.

A atividade demonstra, em um ambiente de laboratório controlado, como o Ncat pode ser utilizado para criar listeners e estabelecer conexões entre eles.

> **Observação:** o procedimento realizado no laboratório utiliza uma conexão intermediária entre as portas `80` e `443`. Ele não representa, por si só, um mecanismo completo de NAT ou de port forwarding transparente. O objetivo aqui é observar o fluxo dos dados entre as conexões criadas pelo Ncat.

---

## Ambiente

* **Sistema:** Kali Linux
* **Ferramenta:** Ncat 7.95
* **Porta de entrada:** `80`
* **Porta intermediária:** `443`
* **Endereço utilizado nos testes:** `127.0.0.1`
* **Terminais utilizados:** três

---

## 1. Acesso como root

Inicialmente, foi obtido acesso administrativo:

```bash id="q8z3mf"
sudo -i
```

---

## 2. Criação do listener na porta 80

No primeiro terminal, foi executado:

```bash id="w7qk9p"
ncat -vl 80 -c 'ncat -l 443'
```

A saída apresentada foi:

```text id="uz499k"
Ncat: Version 7.95 ( https://nmap.org/ncat )
Ncat: Listening on [::]:80
Ncat: Listening on 0.0.0.0:80
```

O comando utiliza:

* `-v` — modo detalhado;
* `-l` — modo listener;
* `80` — porta utilizada pelo primeiro listener;
* `-c` — executa um comando quando uma conexão é recebida;
* `ncat -l 443` — cria um segundo listener na porta `443`.

Dessa forma, o primeiro processo permanece aguardando conexões na porta `80` e, quando uma conexão é recebida, executa o segundo comando Ncat.

---

## 3. Conexão com a porta 80

No segundo terminal, foi estabelecida uma conexão com o listener criado anteriormente:

```bash id="p2k0fr"
ncat -nv 127.0.0.1 80
```

A conexão foi estabelecida com o listener local.

No primeiro terminal, foi possível observar a conexão recebida:

```text id="z2h8xc"
Ncat: Connection from 127.0.0.1:59584.
```

Nesse momento, o primeiro Ncat recebeu a conexão proveniente do segundo terminal.

---

## 4. Conexão com a porta 443

No terceiro terminal, foi realizada uma conexão com a porta `443`:

```bash id="c0m3g7"
ncat -v 127.0.0.1 443
```

O Ncat confirmou a conexão com o listener:

```text id="m8d6qa"
Ncat: Connected to 127.0.0.1:443.
```

Assim, foram estabelecidas as conexões utilizadas no exercício:

```text
Terminal 2
   │
   │ conexão TCP
   ▼
porta 80
   │
   │ Ncat executa
   ▼
porta 443
   │
   ▼
Terminal 3
```

---

## 5. Teste de comunicação

Com as conexões estabelecidas, foi realizado um teste simples de transmissão de dados.

No terceiro terminal foi digitado:

```text id="6tq3aj"
Teste A
```

O texto foi recebido no segundo terminal:

```text id="k5h8vn"
Teste A
```

Em seguida, no segundo terminal foi digitado:

```text id="e6c4sp"
Teste B
```

O texto foi recebido no terceiro terminal:

```text id="n7f1wc"
Teste B
```

Esse comportamento demonstrou que os dados enviados em uma das extremidades puderam ser observados na outra através das conexões criadas pelo Ncat.

---

## 6. Interpretação do procedimento

O comando principal:

```bash id="l3w9yx"
ncat -vl 80 -c 'ncat -l 443'
```

cria um listener na porta `80`. Quando uma conexão é recebida, o parâmetro `-c` faz com que outro processo Ncat seja executado, nesse caso:

```bash id="m1d5pk"
ncat -l 443
```

Esse segundo Ncat cria um listener na porta `443`.

O exercício utiliza esses listeners para demonstrar o estabelecimento de conexões e o fluxo de dados entre os terminais.

É importante diferenciar esse comportamento de um **redirecionamento de portas transparente** realizado por mecanismos como NAT ou regras de firewall. Aqui, o fluxo depende dos processos Ncat criados pelo comando.

---

## Conceitos praticados

### Ncat

O **Ncat** é uma ferramenta de comunicação de rede integrante do projeto Nmap. Pode ser utilizada para criar listeners, estabelecer conexões TCP/UDP e testar comunicação entre hosts e portas.

### Listener

Um listener permanece aguardando conexões de entrada em uma determinada porta.

Neste laboratório foram utilizados listeners nas portas:

```text
80
443
```

### Loopback

O endereço:

```text
127.0.0.1
```

representa a própria máquina. Dessa forma, toda a comunicação realizada no exercício ocorreu localmente.

### Portas TCP

As portas `80` e `443` são tradicionalmente associadas, respectivamente, a HTTP e HTTPS. Neste exercício, entretanto, elas foram utilizadas apenas como portas TCP para demonstrar o funcionamento das conexões Ncat.

### `-l`

Coloca o Ncat em modo de escuta:

```bash id="j5r7av"
-l
```

### `-v`

Ativa a saída detalhada:

```bash id="b3x8ne"
-v
```

permitindo visualizar informações sobre as conexões.

### `-c`

Executa um comando quando uma conexão é recebida:

```bash id="r2u6kw"
-c
```

No laboratório, esse recurso foi utilizado para iniciar o segundo listener Ncat.

---

## Resultado

A atividade permitiu criar listeners utilizando o Ncat e estabelecer conexões TCP entre diferentes terminais da mesma máquina.

O procedimento demonstrou:

1. criação de um listener na porta `80`;
2. recebimento de uma conexão local;
3. execução de um segundo Ncat na porta `443`;
4. estabelecimento de outra conexão local;
5. transmissão de dados entre as extremidades;
6. observação dos dados enviados e recebidos nos terminais.

O teste com `Teste A` e `Teste B` confirmou o funcionamento da comunicação estabelecida durante o laboratório.

---

## Evidência

[**Evidências — Módulo 3 / Aulas 9 e 10**](../evidencias.pdf)

**Print registrado:** etapa 9 da atividade, conforme solicitado pelo roteiro.
