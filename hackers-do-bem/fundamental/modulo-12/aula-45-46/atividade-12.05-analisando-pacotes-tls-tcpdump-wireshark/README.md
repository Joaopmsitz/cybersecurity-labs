# Atividade 12.5 — Analisando Pacotes TLS com tcpdump e Wireshark

## Objetivo

Capturar e analisar tráfego HTTPS utilizando o **tcpdump** e o **Wireshark**, identificando uma conexão TLS e verificando a versão do protocolo utilizada na comunicação.

A atividade utiliza o endereço IPv4 obtido através de uma consulta DNS ao domínio `gov.br` para limitar a captura ao tráfego HTTPS destinado a esse endereço.

---

## Ambiente

* **Sistema operacional:** Kali Linux
* **Ferramentas:** `nslookup`, `tcpdump` e Wireshark
* **Interface de rede:** `eth0`
* **Domínio analisado:** `gov.br`
* **Porta:** `443`
* **Protocolo:** TLS

---

## 1. Acessando o Kali Linux

O Kali Linux foi iniciado e acessado através de RDP.

Após o acesso, foi aberto um terminal e obtido acesso administrativo com:

```bash id="r6v2mq"
sudo -i
```

---

## 2. Consultando o endereço IP de `gov.br`

Antes de iniciar a captura, foi realizada uma consulta DNS para identificar o endereço IP associado ao domínio:

```bash id="k8p3wc"
nslookup gov.br
```

Saída:

```text id="trg7na"
Server:         192.168.98.2
Address:        192.168.98.2#53

Non-authoritative answer:
Name:   gov.br
Address: 161.148.164.31
Name:   gov.br
Address: 2804:151:3:2:161:148:164:31
```

A consulta retornou:

```text id="z4m7xp"
IPv4: 161.148.164.31
IPv6: 2804:151:3:2:161:148:164:31
```

Para a captura realizada na atividade, foi utilizado o endereço IPv4:

```text id="n5c9vr"
161.148.164.31
```

---

## 3. Preparando o tcpdump

O comando utilizado para capturar o tráfego foi:

```bash id="p7x4km"
tcpdump -i eth0 -s 0 host 161.148.164.31 and port 443 -w capture.pcap
```

O comando foi preparado no terminal, mas a execução foi aguardada até o momento correto da atividade.

### Parâmetros utilizados

* `tcpdump`: ferramenta de captura e análise de pacotes.
* `-i eth0`: captura o tráfego da interface `eth0`.
* `-s 0`: utiliza o tamanho máximo do pacote, evitando truncamento do conteúdo capturado pelo snaplen.
* `host 161.148.164.31`: restringe a captura ao endereço IPv4 identificado para `gov.br`.
* `and port 443`: limita a captura ao tráfego associado à porta `443`.
* `-w capture.pcap`: salva os pacotes capturados no arquivo `capture.pcap`.

Dessa forma, a captura fica concentrada no tráfego HTTPS destinado ao endereço IPv4 identificado durante a consulta DNS.

---

## 4. Preparando o acesso ao site

Com o comando `tcpdump` preparado no terminal, o Firefox foi aberto.

No navegador, foi digitado:

```text id="h6q2vn"
gov.br
```

O endereço foi digitado, mas o acesso não foi iniciado imediatamente.

---

## 5. Iniciando a captura

O foco foi retornado para o terminal onde o comando `tcpdump` estava preparado.

O comando foi executado:

```bash id="d3w8qs"
tcpdump -i eth0 -s 0 host 161.148.164.31 and port 443 -w capture.pcap
```

O `tcpdump` iniciou a captura e apresentou:

```text id="5ks8zj"
┌──(root㉿kali)-[~]
└─# tcpdump -i eth0 -s 0 host 161.148.164.31 and port 443 -w capture.pcap
tcpdump: listening on eth0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
```

Nesse momento, o `tcpdump` permaneceu em execução aguardando os pacotes correspondentes ao filtro configurado.

---

## 6. Gerando o tráfego HTTPS

Após iniciar a captura, o foco foi retornado para o Firefox.

Foi pressionado **Enter** para acessar o domínio:

```text id="b9v5mx"
gov.br
```

O site foi carregado enquanto o `tcpdump` registrava os pacotes da comunicação HTTPS.

Após o carregamento da página, o navegador foi fechado.

---

## 7. Encerrando a captura

O foco foi retornado ao terminal e a captura foi interrompida com:

```text id="c4n7kp"
Ctrl+C
```

O resultado apresentado foi:

```text id="5ks8zj"
^C3935 packets captured
3935 packets received by filter
0 packets dropped by kernel
```

A captura registrou:

* **3935 pacotes capturados**
* **3935 pacotes recebidos pelo filtro**
* **0 pacotes descartados pelo kernel**

O arquivo da captura foi salvo como:

```text id="m2x8rz"
capture.pcap
```

---

## 8. Verificando o arquivo de captura

Para verificar se o arquivo havia sido criado, foi executado:

```bash id="q9v4cs"
ls
```

Saída:

```text id="4s8qo0"
┌──(root㉿kali)-[~]
└─# ls
capture.pcap  Desktop    Downloads          Music     Public     Templates          Videos
curso        Documents   inicializacao.log  Pictures  Ransomware thinclient_drives
```

A presença de:

```text id="w6k3px"
capture.pcap
```

confirma que a captura foi armazenada no diretório atual.

---

## 9. Abrindo a captura no Wireshark

O aplicativo **Wireshark** foi aberto.

No menu superior, foi selecionado:

```text id="x3r8mv"
File → Open
```

Em seguida, foi localizado e aberto o arquivo:

```text id="a7p5cn"
capture.pcap
```

O Wireshark carregou os pacotes registrados pelo `tcpdump`.

---

## 10. Filtrando os pacotes TLS

Na barra de filtro do Wireshark, foi utilizado:

```text id="j4m8qx"
tls
```

O filtro restringe a visualização aos pacotes que o Wireshark identifica como pertencentes ao protocolo TLS.

---

## 11. Analisando as conexões TLS

Após a aplicação do filtro, foram observadas conexões TLS presentes na captura.

Nos pacotes analisados, o Wireshark pode identificar informações relacionadas à negociação TLS, incluindo versões como:

```text id="c8v2mr"
TLS 1.2
TLS 1.3
```

A identificação da versão permite verificar qual versão do protocolo TLS está presente nos pacotes capturados.

Além da versão do protocolo, o Wireshark pode apresentar outras informações da sessão, como endereços IP, portas, mensagens do handshake e parâmetros relacionados à negociação criptográfica.

A captura foi realizada especificamente para o endereço IPv4 `161.148.164.31` na porta `443`, conforme o filtro utilizado no `tcpdump`.

---

## 12. Evidência

O print obrigatório corresponde ao **passo 12**, mostrando o arquivo `capture.pcap` aberto no Wireshark com o filtro:

```text id="q6x3vb"
tls
```

A tela deve apresentar os pacotes TLS identificados na captura e as respectivas informações disponíveis, incluindo a versão do protocolo quando exibida pelo Wireshark.

**Frase obrigatória antes do print:**

> **Print da atividade 12.5:** captura `capture.pcap` aberta no Wireshark com o filtro `tls`, exibindo conexões que utilizam TLS e suas versões, como TLS 1.2 e/ou TLS 1.3.

[**Evidências — Módulo 12 / Aulas 45 e 46**](../evidencias.pdf)

---

## 13. Removendo a captura

Após concluir a análise, o Wireshark foi fechado.

O arquivo temporário da captura foi removido com:

```bash id="v8m4kc"
rm capture.pcap
```

A remoção evita manter desnecessariamente o arquivo de captura no ambiente utilizado no laboratório.

---

## Conceitos

* **tcpdump:** ferramenta de captura de pacotes em interfaces de rede.
* **PCAP:** formato utilizado para armazenar capturas de tráfego.
* **TLS:** protocolo criptográfico utilizado para proteger comunicações como HTTPS.
* **Porta 443:** porta normalmente utilizada para HTTPS.
* **Wireshark:** ferramenta gráfica para análise detalhada de pacotes.
* **Filtro `tls`:** utilizado para concentrar a visualização nos pacotes identificados como TLS.

## Fluxo

```text id="r5c9vx"
nslookup gov.br
        ↓
161.148.164.31
        ↓
tcpdump na eth0
        ↓
host 161.148.164.31 + port 443
        ↓
Acesso ao gov.br
        ↓
capture.pcap
        ↓
Wireshark
        ↓
Filtro: tls
        ↓
Análise das conexões TLS
```

## Resultado

Foi realizada uma captura de tráfego HTTPS destinada ao endereço IPv4 `161.148.164.31`, obtido através de `nslookup gov.br`.

O `tcpdump` registrou **3935 pacotes**, sem perdas reportadas pelo kernel, e armazenou os dados em `capture.pcap`. O arquivo foi posteriormente aberto no Wireshark e analisado com o filtro `tls`, permitindo observar as conexões TLS presentes na captura e suas versões identificadas.
