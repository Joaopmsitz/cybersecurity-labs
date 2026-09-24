# Atividade 11.1 — Explorando a Tabela ARP no Kali Linux

## Objetivo

Explorar a **tabela ARP** do Kali Linux, observando os endereços IP e MAC associados às máquinas da rede, limpar as entradas existentes e verificar como novas entradas são aprendidas novamente após uma conexão de rede.

---

## Ambiente

* **Sistema:** Kali GNU/Linux
* **Acesso:** RDP
* **Interface de rede:** `eth0`
* **Ferramentas:** Terminal, `arp` e `ip`
* **Navegador:** Mozilla Firefox

---

## 1. Acessando o Kali Linux

A máquina Kali Linux foi inicializada e acessada via RDP.

Após o acesso, foi aberto o Terminal e obtido acesso administrativo com:

```bash id="h3v9pq"
sudo -i
```

O sistema solicitou a senha do usuário para elevar os privilégios:

```text id="a7k2mz"
┌──(aluno㉿kali)-[~]
└─$ sudo -i
[sudo] senha para aluno:
```

---

## 2. Visualizando a tabela ARP

Para visualizar as entradas atuais da tabela ARP, foi utilizado:

```bash id="b8n4wx"
arp -a
```

A saída apresentada foi:

```text id="w1c6rd"
┌──(root㉿kali)-[~]
└─# arp -a
ip-192-168-98-201.ec2.internal (192.168.98.201) em 12:5c:9d:d7:39:31 [ether] em eth0
ip-192-168-98-1.ec2.internal (192.168.98.1) em 12:82:f4:28:c9:8d [ether] em eth0
ip-192-168-98-2.ec2.internal (192.168.98.2) em 12:82:f4:28:c9:8d [ether] em eth0
```

A tabela apresenta a associação entre endereços IP e endereços MAC conhecidos pelo sistema.

### Elementos observados

* **192.168.98.201:** endereço IP associado ao MAC `12:5c:9d:d7:39:31`;
* **192.168.98.1:** endereço IP associado ao MAC `12:82:f4:28:c9:8d`;
* **192.168.98.2:** endereço IP associado ao MAC `12:82:f4:28:c9:8d`;
* **`[ether]`:** indica Ethernet como tecnologia de camada de enlace;
* **`eth0`:** interface de rede pela qual a associação é conhecida.

A tabela ARP permite que o sistema associe endereços IPv4 aos respectivos endereços MAC dentro da rede local.

---

## 3. Limpando a tabela ARP

Para remover as entradas existentes da tabela de vizinhança, foi executado:

```bash id="x2f7ka"
ip -s -s neigh flush all
```

A saída apresentada foi:

```text id="q5r8nt"
192.168.98.201 dev eth0 lladdr 12:5c:9d:d7:39:31  ref 1 used 66/0/66probes 1 REACHABLE
192.168.98.1 dev eth0 lladdr 12:82:f4:28:c9:8d  used 419/419/376probes 1 STALE
192.168.98.2 dev eth0 lladdr 12:82:f4:28:c9:8d  used 37/37/13probes 1 STALE

*** Round 1, deleting 3 entries ***
*** Flush is complete after 1 round ***
```

O comando removeu as entradas aprendidas da tabela de vizinhança.

Os estados apresentados antes da remoção também mostram informações sobre o estado das associações, como:

* `REACHABLE`: vizinhança considerada alcançável;
* `STALE`: entrada existente, mas que precisa ser validada novamente quando utilizada.

---

## 4. Verificando novamente a tabela ARP

Após a limpeza, o comando foi executado novamente:

```bash id="m4v7zc"
arp -a
```

A saída foi:

```text id="j9q2sx"
┌──(root㉿kali)-[~]
└─# arp -a
ip-192-168-98-201.ec2.internal (192.168.98.201) em 12:5c:9d:d7:39:31 [ether] em eth0
ip-192-168-98-2.ec2.internal (192.168.98.2) em 12:82:f4:28:c9:8d [ether] em eth0
```

Foi possível observar que a entrada referente ao endereço `192.168.98.1` não estava mais presente naquele momento.

A ausência dessa entrada demonstra o efeito da limpeza da tabela. Outras entradas podem reaparecer caso o sistema volte a se comunicar com os respectivos destinos.

---

## 5. Acessando o Google

Foi aberto o **Mozilla Firefox** através de:

```text id="c6k1qp"
Aplicativos → Navegador Web
```

No navegador, foi acessado:

```text id="s7m3vd"
https://www.google.com
```

Essa conexão gera tráfego de rede que pode fazer com que o sistema precise descobrir novamente informações de camada de enlace para alcançar o destino por meio da rede local.

---

## 6. Verificando novamente a tabela ARP

Após acessar o Google, o comando foi executado novamente:

```bash id="r5n8yt"
arp -a
```

A saída apresentada foi:

```text id="e2p6jk"
┌──(root㉿kali)-[~]
└─# arp -a
ip-192-168-98-1.ec2.internal (192.168.98.1) em 12:82:f4:28:c9:8d [ether] em eth0
ip-192-168-98-201.ec2.internal (192.168.98.201) em 12:5c:9d:d7:39:31 [ether] em eth0
ip-192-98-2.ec2.internal (192.168.98.2) em 12:82:f4:28:c9:8d [ether] em eth0
```

A entrada referente ao gateway `192.168.98.1` voltou a aparecer na tabela ARP.

### Evidência — Passo 6

**Frase obrigatória antes do print:**

> **Print da atividade 11.1:** tabela ARP do Kali Linux após o acesso ao Google, mostrando novamente a entrada do endereço `192.168.98.1` associada ao endereço MAC correspondente na interface `eth0`.

[**Evidências — Módulo 11 / Aulas 41 e 42**](../evidencias.pdf)

> **Observação:** o endereço `192.168.98.1` funciona como gateway da rede nesse ambiente. Para alcançar destinos externos, o tráfego precisa ser encaminhado por esse gateway, fazendo com que sua associação de camada 2 esteja novamente disponível.

---

## 7. Encerrando a atividade

Após registrar a evidência, o Mozilla Firefox e o Terminal foram fechados.

---

## Conceitos

* **ARP (Address Resolution Protocol):** protocolo utilizado para descobrir o endereço MAC associado a um endereço IPv4 na rede local.
* **Tabela ARP:** mantém associações entre endereços IP e MAC conhecidas pelo sistema.
* **MAC:** endereço utilizado na comunicação da camada de enlace.
* **Gateway:** dispositivo utilizado para encaminhar tráfego destinado a outras redes.
* **`arp -a`:** exibe associações ARP disponíveis.
* **`ip neigh`:** permite consultar e manipular a tabela de vizinhança do Linux.

## Fluxo da atividade

```text id="u4k9ps"
Visualizar tabela ARP
        ↓
Limpar entradas
        ↓
Verificar tabela novamente
        ↓
Acessar Google
        ↓
Executar arp -a
        ↓
Observar nova associação
```

## Resultado

A tabela ARP foi visualizada e posteriormente limpa. Após uma nova comunicação de rede, a associação do gateway `192.168.98.1` voltou a aparecer, demonstrando que as informações de vizinhança podem ser aprendidas novamente conforme o tráfego da rede.
