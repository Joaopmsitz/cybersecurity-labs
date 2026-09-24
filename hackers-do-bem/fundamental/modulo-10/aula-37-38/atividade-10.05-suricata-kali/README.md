# Atividade 10.5 — Suricata no Kali Linux

## Objetivo

Configurar e executar o **Suricata** no Kali Linux, utilizando regras de detecção para monitoramento do tráfego de rede e verificando os arquivos de log gerados pelo mecanismo.

---

## Ambiente

* **Sistema:** Kali GNU/Linux Rolling
* **Ferramenta:** Suricata
* **Versão:** 8.0.2
* **Interface de rede analisada:** `eth0`
* **Acesso:** RDP

> As credenciais utilizadas no laboratório não são registradas neste README.

---

## 1. Acesso ao terminal como root

Após acessar a máquina Kali Linux, foi aberto um terminal e executado:

```bash
sudo -i
```

O terminal passou a operar com privilégios administrativos.

---

## 2. Habilitando o serviço do Suricata

Foi habilitada a inicialização automática do serviço:

```bash
systemctl enable suricata.service
```

Saída:

```text
Created symlink '/etc/systemd/system/multi-user.target.wants/suricata.service' → '/usr/lib/systemd/system/suricata.service'.
```

O comando cria o vínculo necessário para que o serviço do Suricata seja iniciado automaticamente conforme a configuração do `systemd`.

---

## 3. Parando o serviço e obtendo as regras

Inicialmente, o serviço foi interrompido:

```bash
systemctl stop suricata.service
```

Em seguida, foi acessado o diretório de regras:

```bash
cd /var/lib/suricata/rules/
```

Foi realizado o download do arquivo de regras `emerging-exploit.rules`:

```bash
wget https://raw.githubusercontent.com/seanlinmt/suricata/master/files/rules/emerging-exploit.rules
```

Saída:

```text
--2025-12-05 21:49:23--  https://raw.githubusercontent.com/seanlinmt/suricata/master/files/rules/emerging-exploit.rules
Resolvendo raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.108.133, 185.199.111.133, 185.199.109.133, ...
Conectando-se a raw.githubusercontent.com (raw.githubusercontent.com)|185.199.108.133|:443... conectado.
A requisição HTTP foi enviada, aguardando resposta... 200 OK
Tamanho: 209126 (204K) [text/plain]
Salvando em: “emerging-exploit.rules.1”

emerging-exploit.rules.1   100%[=======================================>] 204,22K  --.-KB/s    em 0,003s  

2025-12-05 21:49:23 (66,0 MB/s) - “emerging-exploit.rules.1” salvo [209126/209126]
```

Após o download, foi retornado ao diretório inicial:

```bash
cd ~
```

---

## 4. Configurando o arquivo `suricata.yaml`

O arquivo principal de configuração do Suricata foi aberto:

```bash
nano /etc/suricata/suricata.yaml
```

Dentro do arquivo, foi localizada a configuração relacionada ao caminho das regras.

A configuração original utilizada no laboratório era:

```yaml
default-rule-path: /var/lib/suricata/rules

rule-files:
  - suricata.rules
```

Ela foi alterada para utilizar o arquivo de regras baixado:

```yaml
default-rule-path: /var/lib/suricata/rules

rule-files:
  - emerging-exploit.rules
```

Após a alteração, o arquivo foi salvo e o editor foi encerrado.

A configuração faz com que o Suricata procure as regras no diretório:

```text
/var/lib/suricata/rules
```

e utilize especificamente:

```text
emerging-exploit.rules
```

---

## 5. Identificando a interface de rede

Foi executado:

```bash
ifconfig
```

Saída:

```text
docker0: flags=4099<UP,BROADCAST,MULTICAST> mtu 1500
        inet 172.17.0.1 netmask 255.255.0.0 broadcast 172.17.255.255
        ether 02:42:e1:ed:78:4a txqueuelen 0 (Ethernet)
        RX packets 0 bytes 0 (0.0 B)
        RX errors 0 dropped 0 overruns 0 frame 0
        TX packets 0 bytes 0 (0.0 B)
        TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 9001
        inet 192.168.98.40 netmask 255.255.255.0 broadcast 192.168.98.255
        inet6 fe80::108d:b6ff:fe11:ff1d prefixlen 64 scopeid 0x20<link>
        ether 12:8d:b6:11:ff:1d txqueuelen 1000 (Ethernet)
        RX packets 249787 bytes 270983687 (258.4 MiB)
        RX errors 0 dropped 0 overruns 0 frame 0
        TX packets 101551 bytes 466777086 (445.1 MiB)
        TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING> mtu 65536
        inet 127.0.0.1 netmask 255.0.0.0
        inet6 ::1 prefixlen 128 scopeid 0x20<link>
        loop txqueuelen 1000 (Ethernet)
        RX packets 135 bytes 11357 (11.0 KiB)
        RX errors 0 dropped 0 overruns 0 frame 0
        TX packets 135 bytes 11357 (11.0 KiB)
        TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0
```

A interface utilizada para executar o Suricata foi a:

```text
eth0
```

Ela apresentava o endereço IPv4:

```text
192.168.98.40
```

---

## 6. Executando o Suricata

Com a configuração realizada e a interface identificada, o Suricata foi iniciado diretamente no terminal:

```bash
suricata -c /etc/suricata/suricata.yaml -i eth0
```

Saída:

```text
i: suricata: This is Suricata version 8.0.2 RELEASE running in SYSTEM mode
W: detect-flowbits: flowbit 'ET.pdf.in.http' is checked but not set. Checked in 2017790 and 0 other sigs
i: mpm-hs: Rule group caching - loaded: 0 newly cached: 13 total cacheable: 13
i: threads: Threads created -> W: 2 FM: 1 FR: 1   Engine started.
```

A saída confirma que o Suricata foi iniciado na versão **8.0.2** e entrou em execução na interface `eth0`.

Também foi apresentada uma mensagem de aviso relacionada a um `flowbit` utilizado por uma regra:

```text
W: detect-flowbits: flowbit 'ET.pdf.in.http' is checked but not set.
```

Apesar do aviso, o mecanismo continuou sua inicialização normalmente, conforme indicado por:

```text
Engine started.
```

---

## 7. Verificando os arquivos de log

Com o Suricata em execução, foi utilizado um segundo terminal para verificar os arquivos de log.

Foi acessado o diretório:

```bash
cd /var/log/suricata
```

Em seguida:

```bash
ls
```

Saída:

```text
eve.json fast.log stats.log suricata.log
```

Os arquivos presentes no diretório incluem:

* `eve.json` — eventos estruturados gerados pelo Suricata.
* `fast.log` — registro simplificado de alertas.
* `stats.log` — estatísticas de execução.
* `suricata.log` — registros relacionados à execução do mecanismo.

---

## Evidência — Passo 9

**Frase obrigatória antes do print:**

> **Print da atividade 10.5:** diretório `/var/log/suricata` exibindo os arquivos de log gerados pelo Suricata durante sua execução.

[**Evidências — Módulo 10 / Aulas 37 e 38**](../evidencias.pdf)

---

## 8. Encerrando o Suricata

Após a verificação dos arquivos de log, o processo do Suricata foi interrompido no primeiro terminal utilizando:

```text
Ctrl+C
```

Saída:

```text
i: suricata: Signal Received. Stopping engine.
i: device: eth0: packets: 8624, drops: 0 (0.00%), invalid chksum: 0
```

O Suricata recebeu o sinal de interrupção e encerrou o mecanismo.

Durante a execução foram contabilizados:

```text
packets: 8624
drops: 0 (0.00%)
invalid chksum: 0
```

Isso indica que, nessa execução, foram processados **8624 pacotes**, sem pacotes descartados pelo mecanismo e sem registros de checksum inválido.

---

## Conceitos

* **Suricata:** mecanismo de detecção e prevenção de intrusões e monitoramento de tráfego de rede.
* **Rules:** regras utilizadas para identificar padrões e comportamentos específicos no tráfego.
* **`eve.json`:** principal arquivo estruturado de eventos.
* **`fast.log`:** registro simplificado de alertas.
* **`stats.log`:** estatísticas da execução.
* **`suricata.log`:** registros operacionais do mecanismo.

## Fluxo da atividade

```text
Habilitar serviço
      ↓
Baixar regras
      ↓
Configurar suricata.yaml
      ↓
Identificar interface eth0
      ↓
Executar Suricata
      ↓
Verificar logs
      ↓
Encerrar execução
```

## Resultado

O Suricata foi configurado para utilizar as regras `emerging-exploit.rules` e executado na interface `eth0`.

A execução foi iniciada corretamente e os arquivos de log foram gerados em `/var/log/suricata`. Ao final, foram registrados **8624 pacotes**, com **0 drops** e **0 checksums inválidos**.
