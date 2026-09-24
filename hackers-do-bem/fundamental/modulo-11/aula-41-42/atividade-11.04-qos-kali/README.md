# Atividade 11.4 — QoS no Kali Linux

## Objetivo

Explorar mecanismos de **Quality of Service (QoS)** no Linux utilizando o comando `tc` (*Traffic Control*), criando filas e filtros para controlar o tráfego da interface `eth0` e, posteriormente, aplicando um limite de taxa de transmissão.

---

## Ambiente

* **Sistema:** Kali GNU/Linux
* **Interface:** `eth0`
* **Ferramenta:** `tc` (*Traffic Control*)
* **Gateway:** `192.168.98.1`
* **Endereço da máquina:** `192.168.98.40`

---

## 1. Acessando o Kali Linux

A máquina Kali Linux foi acessada e o Terminal foi aberto.

Foi obtido acesso administrativo com:

```bash id="a4k7ps"
sudo -i
```

---

## 2. Verificando a interface de rede

As configurações das interfaces foram verificadas utilizando:

```bash id="m8q2vx"
ifconfig
```

A interface principal utilizada na atividade foi a `eth0`.

Entre as informações observadas, estavam:

```text id="c6w9rt"
eth0: ...
      inet 192.168.98.40
      netmask 255.255.255.0
      mtu 9001
```

A interface `eth0` possui o endereço `192.168.98.40` e está conectada à rede utilizada no laboratório.

---

## 3. Criando uma fila de prioridade

Foi adicionada uma disciplina de fila (*qdisc*) do tipo `prio` à interface `eth0`:

```bash id="evi9kk"
tc qdisc add dev eth0 root handle 1: prio
tc filter add dev eth0 parent 1: protocol ip prio 1 u32 match ip protocol 1 0xff flowid 1:1
```

O primeiro comando cria uma fila de prioridade:

```bash
tc qdisc add dev eth0 root handle 1: prio
```

### Parâmetros principais

* `tc`: ferramenta de controle de tráfego do Linux;
* `qdisc`: *queueing discipline*, responsável pelo gerenciamento das filas;
* `add`: adiciona uma nova configuração;
* `dev eth0`: aplica a configuração à interface `eth0`;
* `root`: define a fila como principal da interface;
* `handle 1:`: identifica a disciplina de fila;
* `prio`: utiliza uma fila baseada em prioridades.

O segundo comando adiciona um filtro:

```bash
tc filter add dev eth0 parent 1: protocol ip prio 1 u32 match ip protocol 1 0xff flowid 1:1
```

Nesse caso, o filtro utiliza o protocolo IP e identifica o protocolo `1`, correspondente ao **ICMP**, direcionando os pacotes para a classe `1:1`.

---

## 4. Removendo a QDisc anterior

Como o Linux permite apenas uma disciplina de fila raiz por interface, a configuração anterior foi removida:

```bash id="r5m9kx"
tc qdisc del dev eth0 root
```

Esse comando remove a QDisc raiz configurada anteriormente na interface `eth0`.

---

## 5. Testando a conectividade com o gateway

Antes de configurar uma nova política de QoS, foi realizado um teste de conectividade com o gateway:

```bash id="q80cbn"
ping 192.168.98.1
```

Resultado:

```text id="q80cbn"
PING 192.168.98.1 (192.168.98.1) 56(84) bytes of data.
64 bytes from 192.168.98.1: icmp_seq=1 ttl=255 time=0.325 ms
64 bytes from 192.168.98.1: icmp_seq=2 ttl=255 time=0.424 ms
64 bytes from 192.168.98.1: icmp_seq=3 ttl=255 time=0.450 ms
^C
--- 192.168.98.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2040ms
rtt min/avg/max/mdev = 0.325/0.399/0.450/0.053 ms
```

O teste apresentou:

* **3 pacotes transmitidos;**
* **3 pacotes recebidos;**
* **0% de perda;**
* tempo médio de resposta de aproximadamente **0,399 ms**.

---

## 6. Criando uma QDisc HTB

Foi configurada uma disciplina de fila do tipo **HTB (Hierarchical Token Bucket)**:

```bash id="00aqal"
tc qdisc add dev eth0 root handle 1: htb
tc class add dev eth0 parent 1: classid 1:1 htb rate 10mbit
tc filter add dev eth0 parent 1: protocol ip prio 1 u32 match ip src 192.168.98.1 flowid 1:1
```

A primeira linha cria a QDisc HTB:

```bash
tc qdisc add dev eth0 root handle 1: htb
```

A segunda cria uma classe com limite de taxa:

```bash
tc class add dev eth0 parent 1: classid 1:1 htb rate 10mbit
```

Nesse caso, a classe `1:1` foi configurada com uma taxa de:

```text
10 Mbit/s
```

Por fim, foi criado um filtro que identifica tráfego cujo endereço IP de origem é `192.168.98.1`:

```bash
tc filter add dev eth0 parent 1: protocol ip prio 1 u32 match ip src 192.168.98.1 flowid 1:1
```

Assim, o tráfego correspondente é direcionado para a classe `1:1`.

---

## 7. Removendo a configuração HTB

Antes de realizar o teste final, a QDisc existente foi removida novamente:

```bash id="r5m9kx"
tc qdisc del dev eth0 root
```

Isso permitiu aplicar uma nova configuração de controle de tráfego à interface.

---

## 8. Limitando a interface a 1 Mbit/s

Para demonstrar o controle direto da taxa de transmissão, foi configurada uma QDisc **TBF (Token Bucket Filter)**:

```bash id="pfif6d"
tc qdisc add dev eth0 root tbf rate 1mbit burst 10kb latency 50ms
```

A configuração utiliza:

* `tbf`: *Token Bucket Filter*;
* `rate 1mbit`: limita a taxa a **1 Mbit/s**;
* `burst 10kb`: define o tamanho do burst permitido;
* `latency 50ms`: define a latência máxima utilizada no gerenciamento da fila.

Com essa configuração, o tráfego da interface passa a ser submetido ao limite definido pela QDisc.

### Evidência — Passo 8

**Frase obrigatória antes do print:**

> **Print da atividade 11.4:** configuração da QDisc TBF na interface `eth0`, utilizando `rate 1mbit`, `burst 10kb` e `latency 50ms` para limitar a taxa de transmissão da interface.

[**Evidências — Módulo 11 / Aulas 41 e 42**](../evidencias.pdf)

---

## 9. Removendo o limite de velocidade

Após o registro da evidência, a configuração de QoS foi removida:

```bash id="r5m9kx"
tc qdisc del dev eth0 root
```

Dessa forma, o limite de `1 Mbit/s` aplicado à interface foi removido.

---

## 10. Encerrando a atividade

Após remover a configuração de QoS, o Terminal foi fechado.

---

## Conceitos

* **QoS (Quality of Service):** conjunto de mecanismos utilizados para controlar e organizar o tráfego de rede.
* **`tc`:** ferramenta do Linux para controle de tráfego e gerenciamento de filas.
* **QDisc:** disciplina responsável pelo tratamento dos pacotes em uma interface.
* **PRIO:** QDisc baseada em prioridades.
* **HTB:** mecanismo hierárquico para controle de taxas e classes de tráfego.
* **TBF:** mecanismo baseado em *Token Bucket* utilizado para limitar a taxa de transmissão.
* **ICMP:** protocolo utilizado pelo `ping` para testes de conectividade.

## Fluxo da atividade

```text id="n7w4cs"
Verificar interface
       ↓
Criar QDisc PRIO
       ↓
Adicionar filtro ICMP
       ↓
Remover QDisc
       ↓
Testar gateway
       ↓
Criar QDisc HTB
       ↓
Classificar tráfego
       ↓
Remover QDisc
       ↓
Aplicar TBF de 1 Mbit/s
       ↓
Remover configuração
```

## Resultado

Foram exploradas diferentes formas de controle de tráfego com `tc`, incluindo **PRIO**, **HTB** e **TBF**. No teste final, a interface `eth0` foi configurada com uma taxa máxima de **1 Mbit/s**, demonstrando na prática o uso de QoS para controle de banda.
