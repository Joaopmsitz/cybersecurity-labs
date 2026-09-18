# Atividade 3.2 — Nmap

## Objetivo

Utilizar o **Nmap** para realizar descoberta de hosts, identificar dispositivos ativos na rede, analisar estados de portas, filtrar resultados e observar os pacotes utilizados durante a varredura.

A atividade foi realizada em um ambiente de laboratório controlado, utilizando a rede `192.168.98.0/24`.

---

## Ambiente

* **Sistema:** Kali Linux
* **Ferramenta:** Nmap 7.95
* **Interface de rede:** `eth0`
* **Rede do laboratório:** `192.168.98.0/24`
* **IP da máquina Kali:** `192.168.98.40/24`

---

## 1. Acesso como root

Inicialmente, foi aberto um terminal e obtido acesso administrativo:

```bash
sudo -i
```

---

## 2. Identificação das interfaces de rede

Foi utilizado o `ifconfig` para verificar as interfaces e os endereços IP disponíveis:

```bash
ifconfig
```

Saída observada:

```text
docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0
        ether 02:42:8e:9c:ad:13  txqueuelen 0  (Ethernet)

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
        inet 192.168.98.40  netmask 255.255.255.0
        inet6 fe80::a00:27ff:fe4e:66a1  prefixlen 64  scopeid 0x20<link>
        ether 0a:00:27:4e:66:a1  txqueuelen 1000  (Ethernet)

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
```

A interface utilizada para a rede do laboratório foi a `eth0`, com endereço `192.168.98.40/24`.

---

## 3. Descoberta de hosts com Nmap

Para descobrir quais hosts estavam ativos na rede, foi utilizado:

```bash
nmap -sn 192.168.98.0/24
```

O parâmetro `-sn` realiza uma descoberta de hosts sem executar a varredura convencional de portas.

Saída observada:

```text
Starting Nmap 7.95 ( https://nmap.org )
Nmap scan report for ip-192-168-98-1.ec2.internal (192.168.98.1)
Host is up.

Nmap scan report for ip-192-168-98-2.ec2.internal (192.168.98.2)
Host is up.

Nmap scan report for ip-192-168-98-20.ec2.internal (192.168.98.20)
Host is up.

Nmap scan report for ip-192-168-98-30.ec2.internal (192.168.98.30)
Host is up.

Nmap scan report for ip-192-168-98-201.ec2.internal (192.168.98.201)
Host is up.

Nmap scan report for ip-192-168-98-40.ec2.internal (192.168.98.40)
Host is up.

Nmap done: 256 IP addresses (6 hosts up) scanned in ...
```

Foram identificados **6 hosts ativos** na rede:

* `192.168.98.1`
* `192.168.98.2`
* `192.168.98.20`
* `192.168.98.30`
* `192.168.98.201`
* `192.168.98.40`

---

## 4. Filtrando os IPs encontrados

Foi criado um arquivo contendo os endereços encontrados utilizando um pipeline de comandos:

```bash
cd /home/aluno/Documentos/
```

Depois:

```bash
ls
```

Em seguida, o resultado do Nmap foi filtrado:

```bash
nmap -sn 192.168.98.0/24 | grep 192 | cut -d ' ' -f 5 > ips.txt
```

O comando utiliza:

* `nmap -sn` — descoberta dos hosts ativos;
* `grep 192` — filtra as linhas contendo os endereços da rede;
* `cut -d ' ' -f 5` — extrai o campo correspondente ao endereço;
* `>` — redireciona o resultado para um arquivo;
* `ips.txt` — arquivo criado para armazenar os resultados.

Foi verificada a criação do arquivo:

```bash
ls
```

E seu conteúdo:

```bash
cat ips.txt
```

Resultado:

```text
192.168.98.1
192.168.98.2
192.168.98.20
192.168.98.30
192.168.98.201
192.168.98.40
```

Essa etapa demonstra a utilização de **pipes (`|`) e redirecionamento (`>`)** para transformar a saída de uma ferramenta em entrada para outras ferramentas do sistema.

---

## 5. Varredura utilizando ACK Scan

Foi utilizada a opção `-sA`:

```bash
nmap -sA 192.168.98.0/24
```

O ACK Scan é utilizado principalmente para identificar se as portas estão sendo filtradas por firewall. Diferentemente de uma varredura SYN, ele não deve ser interpretado simplesmente como uma identificação de portas abertas.

Nesse tipo de varredura, o Nmap pode apresentar estados como:

* **filtered** — há indícios de filtragem por firewall ou outro mecanismo;
* **unfiltered** — a porta pode ser alcançada, mas o ACK Scan não determina que ela esteja aberta.

---

## 6. Exibindo somente portas abertas

Foi realizada uma nova varredura utilizando:

```bash
nmap --open 192.168.98.0/24
```

Saída observada:

```text
Nmap scan report for ip-192-168-98-1.ec2.internal (192.168.98.1)
All 1000 scanned ports on 192.168.98.1 are filtered

Nmap scan report for ip-192-168-98-2.ec2.internal (192.168.98.2)
PORT   STATE       SERVICE
53/tcp unfiltered  domain
999/tcp filtered   ...

Nmap scan report for ip-192-168-98.20.ec2.internal (192.168.98.20)
All 1000 scanned ports on 192.168.98.20 are filtered

Nmap scan report for ip-192-168-98.30.ec2.internal (192.168.98.30)
All 1000 scanned ports on 192.168.98.30 are filtered

Nmap scan report for ip-192-168-98-201.ec2.internal (192.168.98.201)
All 1000 scanned ports on 192.168.98.201 are unfiltered

Nmap scan report for ip-192-168-98-40.ec2.internal (192.168.98.40)
All 1000 scanned ports on 192.168.98.40 are unfiltered

Nmap done: 256 IP addresses (6 hosts up) scanned in 12.73 seconds
```

Um ponto importante observado durante a atividade é que **`unfiltered` não significa necessariamente `open`**. O resultado depende do tipo de varredura utilizada. O ACK Scan é principalmente utilizado para estudar filtragem de pacotes.

---

## 7. Observando os pacotes com `--packet-trace`

Por fim, foi utilizada a opção `--packet-trace` para visualizar informações dos pacotes envolvidos durante a varredura:

```bash
nmap --packet-trace 192.168.98.0/24
```

Entre as informações observadas estavam requisições ARP para descoberta dos hosts, por exemplo:

```text
ARP who-has 192.168.98.x tell 192.168.98.40
```

Também foram identificadas portas abertas no próprio host do laboratório:

```text
22/tcp open  ssh
3389/tcp open  ms-wbt-server
```

O parâmetro `--packet-trace` permite observar uma camada mais baixa do processo de varredura, tornando possível relacionar o resultado apresentado pelo Nmap com os pacotes efetivamente utilizados para realizar a descoberta e análise.

---

## 8. Remoção do arquivo temporário

Após finalizar a atividade, o arquivo utilizado para armazenar os IPs foi removido:

```bash
rm ips.txt
```

---

## Conceitos praticados

### Nmap

Ferramenta utilizada para descoberta de hosts, análise de portas e identificação de características de uma rede.

### Host Discovery

Processo utilizado para identificar quais endereços IP estão ativos em determinado segmento de rede.

### TCP ACK Scan

A opção `-sA` envia pacotes TCP ACK e é utilizada principalmente para analisar regras de filtragem e comportamento de firewalls.

### Estados de portas

Durante a atividade foram observados estados como `filtered` e `unfiltered`. A interpretação desses estados depende do tipo de scan utilizado.

### `--open`

Permite reduzir a quantidade de informações exibidas, concentrando a saída em portas identificadas como abertas quando o tipo de varredura consegue determinar esse estado.

### `--packet-trace`

Exibe informações sobre os pacotes utilizados durante a execução do Nmap, permitindo observar o funcionamento da varredura.

### Pipes e redirecionamento

A atividade também utilizou recursos básicos do shell:

```text
|
```

para encadear comandos, e:

```text
>
```

para redirecionar a saída para um arquivo.

---

## Resultado

A atividade permitiu utilizar o Nmap de forma prática em uma rede de laboratório, passando por diferentes etapas:

1. identificação da interface e do endereço IP da máquina;
2. descoberta de hosts ativos;
3. extração dos IPs encontrados utilizando comandos do Linux;
4. análise de filtragem com ACK Scan;
5. análise de portas;
6. observação dos pacotes utilizados durante a varredura.

O exercício reforçou a relação entre **descoberta de hosts, análise de portas, filtragem de rede, firewall e tráfego TCP/IP**.

---

## Evidência

[**Evidências — Módulo 3 / Aulas 9 e 10**](../evidencias.pdf)

**Print registrado:** etapa 6 da atividade, conforme solicitado pelo roteiro.
