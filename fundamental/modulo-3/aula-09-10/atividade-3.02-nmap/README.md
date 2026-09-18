# Atividade 3.2 — Explorando varreduras com o Kali Linux

## Objetivo

Explorar o **Nmap** no Kali Linux para identificar hosts ativos em uma rede, analisar estados de portas, verificar possíveis filtragens por firewall, armazenar resultados em arquivo e observar os pacotes gerados durante uma varredura.

A atividade foi realizada em ambiente de laboratório controlado, exclusivamente para fins educacionais.

## Ambiente

* Kali Linux
* Terminal
* Nmap 7.95
* Rede de laboratório `192.168.98.0/24`

---

## 1. Acesso ao modo superusuário

O primeiro passo foi abrir o Terminal e utilizar o `sudo` para obter privilégios administrativos.

```bash
sudo -i
```

---

## 2. Identificando as interfaces de rede

O comando `ifconfig` foi utilizado para verificar as interfaces disponíveis e identificar a rede utilizada pela máquina.

```bash
ifconfig
```

Saída observada:

```text
docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        ether 02:42:df:26:13:80  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
        inet 192.168.98.40  netmask 255.255.255.0  broadcast 192.168.98.255
        inet6 fe80::1005:27ff:fe44:1631  prefixlen 64  scopeid 0x20<link>
        ether 12:05:27:44:16:31  txqueuelen 1000  (Ethernet)
        RX packets 1818194  bytes 2694820836 (2.5 GiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 61082  bytes 77348531 (73.7 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0  broadcast 255.255.255.255
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Ethernet)
        RX packets 23  bytes 1937 (1.8 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 23  bytes 1937 (1.8 KiB)
        RX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

A interface `eth0` apresentou o endereço `192.168.98.40/24`, indicando que a máquina estava conectada à rede de laboratório `192.168.98.0/24`.

---

## 3. Descobrindo hosts ativos com Nmap

Foi utilizado o modo `-sn` para realizar uma descoberta de hosts sem efetuar uma varredura convencional de portas.

```bash
nmap -sn 192.168.98.0/24
```

Saída observada:

```text
Starting Nmap 7.95 ( https://nmap.org ) at 2025-09-06 10:00 -03
Nmap scan report for ip-192-168-98-1.ec2.internal (192.168.98.1)
Host is up (0.00020s latency).
MAC Address: 12:BF:8B:B8:B0:87 (Unknown)
Nmap scan report for ip-192-168-98-2.ec2.internal (192.168.98.2)
Host is up (0.00019s latency).
MAC Address: 12:BF:8B:B8:B0:87 (Unknown)
Nmap scan report for ip-192-168-98-20.ec2.internal (192.168.98.20)
Host is up (0.00024s latency).
MAC Address: 12:89:91:6B:9F:03 (Unknown)
Nmap scan report for ip-192-168-98-30.ec2.internal (192.168.98.30)
Host is up (0.00034s latency).
MAC Address: 12:33:11:FB:DE:ED (Unknown)
Nmap scan report for ip-192-168-98-201.ec2.internal (192.168.98.201)
Host is up (0.00018s latency).
MAC Address: 12:CA:37:E3:5B:9B (Unknown)
Nmap scan report for ip-192-168-98-40.ec2.internal (192.168.98.40)
Host is up.
Nmap done: 256 IP addresses (6 hosts up) scanned in 1.95 seconds
```

Foram identificados **6 hosts ativos** na rede analisada.

### Conceito

O parâmetro `-sn` realiza uma descoberta de hosts, permitindo identificar quais endereços respondem na rede sem realizar a varredura tradicional das portas TCP.

---

## 4. Salvando os hosts encontrados em um arquivo

Foi criado um arquivo `ips.txt` contendo os resultados da descoberta.

```bash
cd /home/aluno/Documentos/
ls
nmap -sn 192.168.98.0/24 | grep 192 | cut -d ' ' -f 5 > ips.txt
ls
cat ips.txt
```

Saída:

```text
ips.txt

ip-192-168-98-1.ec2.internal
ip-192-168-98-2.ec2.internal
ip-192-168-98-20.ec2.internal
ip-192-168-98-30.ec2.internal
ip-192-168-98-201.ec2.internal
ip-192-168-98-40.ec2.internal
```

### Entendendo o comando

```text
nmap -sn 192.168.98.0/24
```

Realiza a descoberta dos hosts ativos na rede.

```text
|
```

O pipe encaminha a saída para o próximo comando.

```text
grep 192
```

Filtra as linhas que contêm `192`.

```text
cut -d ' ' -f 5
```

Extrai o campo correspondente ao endereço apresentado na saída.

```text
> ips.txt
```

Redireciona o resultado para o arquivo `ips.txt`.

---

## 5. Analisando filtragem de portas com TCP ACK Scan

Para observar o comportamento das portas e possíveis mecanismos de filtragem, foi utilizado o TCP ACK Scan:

```bash
nmap -sA 192.168.98.0/24
```

O parâmetro `-sA` realiza um **TCP ACK Scan**. Esse tipo de varredura pode ajudar a diferenciar portas filtradas de portas não filtradas, sendo útil na análise do comportamento de firewalls e filtros de pacotes.

---

## 6. Identificando portas abertas

A varredura seguinte foi realizada com o parâmetro `--open`, que limita a apresentação aos resultados considerados abertos.

```bash
nmap --open 192.168.98.0/24
```

Saída observada:

```text
Starting Nmap 7.95 ( https://nmap.org ) at 2025-09-06 10:02 -03
Nmap scan report for ip-192-168-98-1.ec2.internal (192.168.98.1)
Host is up (0.000064s latency).
All 1000 scanned ports on ip-192-168-98-1.ec2.internal (192.168.98.1) are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)
MAC Address: 12:BF:8B:B8:B0:87 (Unknown)

Nmap scan report for ip-192-168-98-2.ec2.internal (192.168.98.2)
Host is up (0.00013s latency).
Not shown: 999 filtered tcp ports (no-response)
PORT   STATE      SERVICE
53/tcp unfiltered domain
MAC Address: 12:BF:8B:B8:B0:87 (Unknown)

Nmap scan report for ip-192-168-98-20.ec2.internal (192.168.98.20)
Host is up (0.000062s latency).
All 1000 scanned ports on ip-192-168-98-20.ec2.internal (192.168.98.20) are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)
MAC Address: 12:89:91:6B:9F:03 (Unknown)

Nmap scan report for ip-192-168-98-30.ec2.internal (192.168.98.30)
Host is up (0.000039s latency).
All 1000 scanned ports on ip-192-168-98.30.ec2.internal (192.168.98.30) are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)
MAC Address: 12:33:11:FB:DE:ED (Unknown)

Nmap scan report for ip-192-168-98-201.ec2.internal (192.168.98.201)
Host is up (0.00031s latency).
All 1000 scanned ports on ip-192-168-98-201.ec2.internal (192.168.98.201) are in ignored states.
Not shown: 1000 unfiltered tcp ports (reset)
MAC Address: 12:CA:37:E3:5B:9B (Unknown)

Nmap scan report for ip-192-168-98-40.ec2.internal (192.168.98.40)
Host is up (0.000016s latency).
All 1000 scanned ports on ip-192-168-98-40.ec2.internal (192.168.98.40) are in ignored states.
Not shown: 1000 unfiltered tcp ports (reset)

Nmap done: 256 IP addresses (6 hosts up) scanned in 12.73 seconds
```

### Interpretação

Os resultados mostraram diferentes comportamentos entre os hosts:

* `192.168.98.1`: as 1000 portas analisadas estavam filtradas e sem resposta.
* `192.168.98.2`: a porta `53/tcp` apareceu como `unfiltered`, associada ao serviço DNS.
* `192.168.98.20`: portas filtradas, sem resposta.
* `192.168.98.30`: portas filtradas, sem resposta.
* `192.168.98.201`: portas classificadas como `unfiltered`, com respostas `RST`, indicando portas acessíveis, porém fechadas.
* `192.168.98.40`: portas `unfiltered` com respostas `RST`, indicando que o host estava respondendo, mas nenhuma das portas analisadas estava aberta nesse momento.

O estado `filtered` indica que o Nmap não conseguiu determinar se a porta está aberta porque algum mecanismo de filtragem impediu uma resposta conclusiva. Já `unfiltered` significa que a porta está acessível aos testes realizados, embora o resultado não determine necessariamente que exista um serviço escutando nela.

---

## 7. Observando os pacotes com `--packet-trace`

Para visualizar detalhes dos pacotes enviados e recebidos durante a varredura, foi utilizado:

```bash
nmap --packet-trace 192.168.98.0/24
```

Parte da saída observada:

```text
Starting Nmap 7.95 ( https://nmap.org ) at 2025-09-06 10:24 -03
SENT (0.0460s) ARP who-has 192.168.98.1 tell 192.168.98.40
SENT (0.0461s) ARP who-has 192.168.98.2 tell 192.168.98.40

...

RCVD (13.9826s) TCP 192.168.98.40:50849 > 192.168.98.40:18988 S ttl=39 id=48268 iplen=44  seq=2937192391 win=1024 <mss 1460>
RCVD (13.9826s) TCP 192.168.98.40:18988 > 192.168.98.40:50849 RA ttl=64 id=0 iplen=40  seq=0 win=0
Nmap scan report for ip-192-168-98-40.ec2.internal (192.168.98.40)
Host is up (0.000013s latency).
Not shown: 998 closed tcp ports (reset)
PORT     STATE SERVICE
22/tcp   open  ssh
3389/tcp open  ms-wbt-server

Nmap done: 256 IP addresses (6 hosts up) scanned in 14.03 seconds
```

O parâmetro `--packet-trace` permite observar os pacotes utilizados pelo Nmap durante o processo de descoberta e análise.

A saída também mostrou, nesse momento da atividade, as portas:

```text
22/tcp   open  ssh
3389/tcp open  ms-wbt-server
```

Isso demonstra como uma varredura pode revelar serviços expostos em um host dentro de um ambiente autorizado.

---

## 8. Removendo o arquivo temporário

Após concluir a análise, o arquivo criado durante o exercício foi removido:

```bash
ls
ips.txt

rm ips.txt
```

O arquivo `ips.txt` foi utilizado apenas como apoio durante a atividade.

---

## Conceitos praticados

* Nmap
* Descoberta de hosts
* TCP Ping Scan
* TCP ACK Scan
* Estados `open`, `filtered` e `unfiltered`
* Análise de portas
* Identificação de serviços
* Pipe (`|`)
* `grep`
* `cut`
* Redirecionamento de saída
* `--packet-trace`
* Reconhecimento de rede

## Resultado

A atividade permitiu praticar o uso do Nmap para realizar reconhecimento de uma rede de laboratório, identificando hosts ativos, analisando o comportamento das portas e observando os pacotes envolvidos durante uma varredura.

O exercício também mostrou como diferentes parâmetros do Nmap produzem informações diferentes sobre uma rede, desde a simples descoberta de hosts até a análise detalhada do tráfego gerado pelo scanner.

## Evidência

Os prints solicitados para o módulo foram reunidos no arquivo:

[**Evidências — Módulo 3 / Aulas 1 e 2**](../evidencias.pdf)
