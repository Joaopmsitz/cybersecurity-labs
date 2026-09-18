# Atividade 3.6 — Explorando ferramentas de detecção de rede no Kali Linux

## Objetivo

Utilizar comandos disponíveis no **Kali Linux** para diagnosticar o estado da rede, identificar interfaces, testar conectividade, observar rotas, consultar estatísticas de protocolos e verificar conexões e serviços de rede em execução.

A atividade foi realizada em ambiente de laboratório e os comandos foram utilizados exclusivamente para fins acadêmicos.

---

## Ambiente

* **Sistema:** Kali Linux
* **Interface principal:** `eth0`
* **IP da máquina:** `192.168.98.40/24`
* **Rede:** `192.168.98.0/24`

---

## 1. Acesso como superusuário

Foi aberto o Terminal e executado:

```bash
sudo -i
```

Após informar a senha do ambiente de laboratório, o terminal passou a operar como `root`.

---

## 2. Identificação das interfaces de rede

Foi utilizado o comando:

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
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Loopback Local)
        RX packets 23  bytes 1937 (1.8 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 23  bytes 1937 (1.8 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

Foram identificadas três interfaces:

* `docker0` — interface virtual utilizada pelo Docker;
* `eth0` — interface principal conectada à rede do laboratório;
* `lo` — interface de loopback.

A interface `eth0` possuía o endereço `192.168.98.40/24`.

---

## 3. Teste de conectividade com `ping`

Para testar a conectividade e verificar a resolução do nome de domínio, foi utilizado:

```bash
ping www.google.com
```

Saída observada:

```text
PING www.google.com (172.253.63.106) 56(84) bytes of data.
64 bytes from bi-in-f106.1e100.net (172.253.63.106): icmp_seq=1 ttl=109 time=1.42 ms
64 bytes from bi-in-f106.1e100.net (172.253.63.106): icmp_seq=2 ttl=109 time=1.41 ms
```

A execução foi interrompida utilizando:

```text
Ctrl + C
```

O resultado demonstra que `www.google.com` foi resolvido para o endereço `172.253.63.106` no momento da execução e que houve respostas aos pacotes ICMP enviados.

Os principais campos observados foram:

* `icmp_seq` — número sequencial do pacote;
* `ttl` — valor de Time To Live observado na resposta;
* `time` — tempo de ida e volta (RTT) da comunicação.

---

## 4. Rastreamento da rota com `traceroute`

Em seguida, foi utilizado:

```bash
traceroute -I grancursos.com.br
```

O parâmetro `-I` faz o `traceroute` utilizar sondas ICMP.

Saída apresentada no roteiro:

```text
traceroute to grancursos.com.br (172.67.175.92), 30 hops max, 60 byte packets
 1  244.5.7.59 (244.5.7.59)  2.953 ms  2.920 ms *
 2  240.4.116.42 (240.4.116.42)  0.305 ms  0.299 ms  0.318 ms
 3  242.12.75.131 (242.12.75.131)  1.596 ms  1.589 ms  1.584 ms
 4  240.3.180.12 (240.3.180.12)  1.048 ms  1.332 ms  1.557 ms
 5  240.3.180.29 (240.3.180.29)  0.636 ms  0.961 ms  0.955 ms
 6  99.83.116.94 (99.83.116.94)  0.949 ms  1.081 ms  1.101 ms
 7  * * *
 8  173.245.63.137 (173.245.63.137)  1.421 ms  1.404 ms  1.359 ms
 9  172.67.175.92 (172.67.175.92)  0.901 ms  0.889 ms  0.870 ms
```

O `traceroute` permite observar os saltos utilizados pelos pacotes entre a origem e o destino.

Os `*` representam sondas que não receberam resposta dentro do tempo esperado. Isso não significa necessariamente que exista uma falha de conectividade: roteadores e dispositivos intermediários podem não responder a determinados tipos de sondas ICMP.

A saída também demonstra que o caminho pode passar por diferentes redes e infraestruturas antes de chegar ao destino.

> **Observação:** resultados de `traceroute` podem variar conforme o momento da execução, roteamento, balanceamento de carga e políticas de filtragem.

---

## 5. Estatísticas das interfaces com `netstat -i`

Foi utilizado:

```bash
netstat -i
```

Saída observada:

```text
Tabela de Interfaces do Kernel
Iface             MTU    RX-OK RX-ERR RX-DRP RX-OVR    TX-OK TX-ERR TX-DRP TX-OVR Flg
docker0          1500        0      0      0 0             0      0      0      0 BMU
eth0             9001     8055      0      0 0          9143      0      0      0 BMRU
lo              65536       23      0      0 0            23      0      0      0 LRU
```

O comando apresenta estatísticas relacionadas às interfaces de rede.

Campos importantes:

* **Iface** — nome da interface;
* **MTU** — Maximum Transmission Unit;
* **RX-OK** — pacotes recebidos sem erro;
* **RX-ERR** — erros de recepção;
* **RX-DRP** — pacotes recebidos descartados;
* **RX-OVR** — ocorrências de overflow na recepção;
* **TX-OK** — pacotes transmitidos com sucesso;
* **TX-ERR** — erros de transmissão;
* **TX-DRP** — pacotes descartados durante transmissão;
* **TX-OVR** — ocorrências de overflow na transmissão;
* **Flg** — flags associadas à interface.

---

## 6. Consulta da tabela de roteamento

Foi executado:

```bash
netstat -rn
```

Saída observada:

```text
Tabela de Roteamento IP do Kernel
Destino         Roteador        MáscaraGen.    Opções   MSS Janela  irtt Iface
0.0.0.0         192.168.98.1    0.0.0.0         UG        0 0          0 eth0
172.17.0.0      0.0.0.0         255.255.0.0     U         0 0          0 docker0
192.168.98.0    0.0.0.0         255.255.255.0   U         0 0          0 eth0
```

A tabela mostra as rotas conhecidas pelo sistema.

A entrada:

```text
0.0.0.0         192.168.98.1    0.0.0.0         UG
```

representa a rota padrão, utilizando `192.168.98.1` como gateway através da interface `eth0`.

A rede:

```text
192.168.98.0/24
```

está diretamente associada à interface `eth0`.

Já:

```text
172.17.0.0/16
```

está associada à interface virtual `docker0`.

---

## 7. Estatísticas dos protocolos de rede

Foi utilizado:

```bash
netstat -s
```

Saída observada:

```text
Ip:
    Forwarding: 1
    9136 total packets received
    4 with invalid addresses
    0 forwarded
    0 incoming packets discarded
    9132 incoming packets delivered
    10381 requests sent out
Icmp:
    29 ICMP messages received
    0 input ICMP message failed
    Histograma de entrada ICMP:
        destination unreachable: 3
        timeout in transit: 15
        echo replies: 11
    56 ICMP messages sent
    0 ICMP messages failed
    Histograma de saída ICMP
        destination unreachable: 3
        echo requests: 53
IcmpMsg:
        InType0: 11
        InType3: 3
        InType11: 15
        OutType3: 3
        OutType8: 53
Tcp:
    68 active connection openings
    3 passive connection openings
    0 failed connection attempts
    1 connection resets received
    1 connections established
    9068 segments received
    16104 segments sent out
    0 segments retransmitted
    0 bad segments received
    0 resets sent
Udp:
    43 packets received
    3 packets to unknown port received
    0 packet receive errors
    48 packets sent
    0 receive buffer errors
    0 send buffer errors
UdpLite:
TcpExt:
    67 TCP sockets finished time wait in fast timer
    204 delayed acks sent
    2 packet headers predicted
    1628 acknowledgments not containing data payload received
    6007 predicted acknowledgments
    TCPBacklogCoalesce: 2
    TCPRcvCoalesce: 11
    TCPAutoCorking: 43
    TCPOrigDataSent: 14843
    TCPHystartTrainDetect: 1
    TCPHystartTrainCwnd: 16
    TCPDelivered: 14910
IpExt:
    OutMcastPkts: 10
    InOctets: 535228
    OutOctets: 70865774
    OutMcastOctets: 1590
    InNoECTPkts: 9172
    InECT0Pkts: 2
MPTcpExt:
```

O resultado apresenta estatísticas agrupadas por protocolo e extensão.

### IP

Apresenta informações gerais sobre o tráfego IP, incluindo pacotes recebidos, descartados e enviados.

### ICMP

Apresenta estatísticas de mensagens ICMP, incluindo:

* `echo requests`;
* `echo replies`;
* `destination unreachable`;
* `timeout in transit`.

### TCP

Apresenta estatísticas relacionadas às conexões TCP, incluindo aberturas de conexão, segmentos recebidos e enviados, retransmissões e resets.

### UDP

Apresenta estatísticas de datagramas UDP recebidos e enviados.

### TcpExt / IpExt

Apresentam informações adicionais relacionadas aos protocolos TCP e IP.

---

## 8. Verificação de conexões e serviços

A etapa final e principal ponto de evidência da atividade utilizou:

```bash
netstat -anptu
```

O comando combina diferentes opções:

* `-a` — mostra todas as conexões e sockets em escuta;
* `-n` — exibe endereços e portas numericamente;
* `-p` — mostra o PID e o programa associado;
* `-t` — inclui conexões TCP;
* `-u` — inclui conexões UDP.

Saída observada:

```text
Conexões Internet Ativas (servidores e estabelecidas)
Proto Recv-Q Send-Q Endereço Local          Endereço Remoto         Estado      PID/Program name
tcp        0      0 127.0.0.1:36367         0.0.0.0:*               OUÇA       576/containerd
tcp        0      0 0.0.0.0:22              0.0.0.0:*               OUÇA       618/sshd: /usr/sbin
tcp6       0      0 :::22                   :::*                    OUÇA       618/sshd: /usr/sbin
tcp6       0      0 :::3389                 :::*                    OUÇA       641/xrdp
tcp6       0      0 ::1:3350                :::*                    OUÇA       581/xrdp-sesman
tcp6       0      0 192.168.98.40:3389      192.168.98.201:49732    ESTABELECIDA 2206/xrdp
udp        0      0 0.0.0.0:68              0.0.0.0:*                           441/dhclient
udp6       0      0 fe80::1005:27ff:fe4:546 :::*                                494/dhclient
```

Essa saída permite relacionar **portas de rede, estados de conexão e processos em execução**.

Por exemplo:

```text
tcp  0  0  0.0.0.0:22  0.0.0.0:*  OUÇA  618/sshd
```

indica que o serviço `sshd` estava escutando na porta TCP `22`.

Também foi observada uma conexão RDP:

```text
tcp6  0  0  192.168.98.40:3389  192.168.98.201:49732  ESTABELECIDA  2206/xrdp
```

Nesse caso, a porta `3389` estava associada ao serviço `xrdp`, e havia uma conexão estabelecida com outro endereço do ambiente de laboratório.

A saída também mostrou o `dhclient` associado à porta UDP `68`, utilizada pelo DHCP.

---

## 9. Encerramento

Após finalizar as consultas, o Terminal foi fechado.

---

## Conceitos praticados

Durante a atividade foram utilizados diferentes recursos de diagnóstico de rede:

* `ifconfig` — identificação de interfaces e endereços;
* `ping` — teste de conectividade utilizando ICMP;
* `traceroute` — observação dos saltos entre origem e destino;
* `netstat -i` — estatísticas das interfaces;
* `netstat -rn` — tabela de roteamento;
* `netstat -s` — estatísticas dos protocolos;
* `netstat -anptu` — conexões, portas, estados e processos associados.

O conjunto desses comandos permite obter uma visão prática do estado da rede de um sistema Linux.

---

## Resultado

A atividade permitiu analisar diferentes camadas do funcionamento da rede no Kali Linux, desde a configuração das interfaces até as conexões e serviços que estavam ativos.

Foi possível identificar:

1. interfaces e endereços IP;
2. conectividade através de ICMP;
3. saltos de uma rota de rede;
4. estatísticas de transmissão e recepção;
5. rotas configuradas;
6. estatísticas dos protocolos IP, ICMP, TCP e UDP;
7. portas em estado de escuta;
8. conexões estabelecidas;
9. processos associados aos sockets.

A etapa final com `netstat -anptu` foi utilizada como evidência da atividade, conforme especificado no roteiro.

---

## Evidência

[**Evidências — Módulo 3 / Aulas 11 e 12**](../evidencias.pdf)
