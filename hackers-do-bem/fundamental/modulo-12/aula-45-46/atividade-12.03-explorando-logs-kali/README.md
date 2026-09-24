# Atividade 12.3 — Explorando os Logs no Kali Linux

## Objetivo

Explorar os principais arquivos e ferramentas de registro de eventos disponíveis no **Kali Linux**, utilizando o diretório `/var/log`, o arquivo `syslog`, o `journalctl` e o aplicativo gráfico **Logs** do GNOME.

A atividade também demonstra como realizar uma busca por ocorrências contendo a palavra `error` nos registros do sistema.

---

## Ambiente

* **Sistema operacional:** Kali Linux
* **Acesso:** RDP
* **Diretório de logs:** `/var/log`
* **Ferramentas:** `cat`, `journalctl`, `grep` e Logs do GNOME

---

## 1. Acessando o Kali Linux

O Kali Linux foi iniciado e acessado através de RDP.

Após o acesso, foi aberto um terminal e obtido acesso administrativo com:

```bash id="v8m2qp"
sudo -i
```

---

## 2. Explorando o diretório `/var/log`

O diretório `/var/log` concentra diversos arquivos e diretórios utilizados pelo sistema para armazenar registros de eventos.

Para visualizar seu conteúdo, foi executado:

```bash id="n4x7cz"
ls -l /var/log
```

Saída:

```text id="tna7n1"
total 7652
-rw-r--r--  1 root              root                  0 dez  2 23:00 alternatives.log
-rw-r--r--  1 root              root              73040 nov 27 21:16 alternatives.log.1
-rw-r--r--  1 root              root               6014 jul 10  2024 alternatives.log.2.gz
drwxr-x---  2 root              adm                4096 jul  4  2024 apache2
drwxr-xr-x  2 root              root               4096 dez  2 23:00 apt
drwxr-x---  2 root              adm                4096 jun 11  2024 audit
-rw-r-----  1 root              adm               66442 dez  6 10:47 auth.log
-rw-r-----  1 root              adm               37391 dez  2 23:00 auth.log.1
-rw-r-----  1 root              adm                1395 nov 24 16:30 auth.log.2.gz
-rw-r-----  1 root              adm                1873 out 14  2024 auth.log.3.gz
-rw-r-----  1 root              adm              694409 jul 10  2024 auth.log.4.gz
-rw-------  1 root              root               2590 dez  6 10:45 boot.log
-rw-------  1 root              root             106163 dez  6 10:45 boot.log.1
-rw-------  1 root              root              40417 dez  5 17:40 boot.log.2
-rw-------  1 root              root              44216 dez  3 00:19 boot.log.3
-rw-------  1 root              root              66461 dez  2 23:00 boot.log.4
-rw-------  1 root              root              22404 nov 27 20:41 boot.log.5
-rw-------  1 root              root              25803 nov 24 16:30 boot.log.6
-rw-------  1 root              root              46369 out 14  2024 boot.log.7
-rw-rw----  1 root              utmp                  0 dez  2 23:00 btmp
-rw-rw----  1 root              utmp                  0 nov 24 16:30 btmp.1
drwxr-xr-x  2 clamav            clamav             4096 dez  2 23:00 clamav
-rw-r-----  1 root              adm               27347 dez  6 10:45 cloud-init.log
-rw-r-----  1 root              adm              102475 dez  2 23:00 cloud-init.log.1.gz
-rw-r-----  1 root              adm              105384 dez  2 23:35 cloud-init.log.2.gz
-rw-r-----  1 root              adm              114037 out 14  2024 cloud-init.log.3.gz
-rw-r-----  1 root              adm               97731 dez  6 10:45 cloud-init-output.log
-rw-r-----  1 root              adm               18152 dez  6 10:45 cron.log
-rw-r-----  1 root              adm                7868 dez  2 23:00 cron.log.1
-rw-r-----  1 root              adm                 441 nov 24 16:30 cron.log.2.gz
-rw-r-----  1 root              adm                 621 out 14  2024 cron.log.3.gz
-rw-r--r--  1 root              root                  0 dez  2 23:00 dpkg.log
-rw-r--r--  1 root              root            1398585 nov 27 23:08 dpkg.log.1
-rw-r--r--  1 root              root                764 out 14  2024 dpkg.log.2.gz
-rw-r--r--  1 root              root              94566 jul 10  2024 dpkg.log.3.gz
drwxr-s---  2 Debian-exim       adm                4096 dez  6 10:45 exim4
-rw-r--r--  1 root              root                  0 mai 27  2024 faillog
-rw-r--r--  1 root              root               6216 nov 27 21:08 fontconfig.log
drwxr-xr-x  2 freerad           adm                4096 jul  4  2024 freeradius
drwxr-sr-x+ 3 root              systemd-journal    4096 jul  2  2024 journal
-rw-r-----  1 root              adm              457577 dez  6 10:45 kern.log
-rw-r-----  1 root              adm              208922 dez  2 23:00 kern.log.1
-rw-r-----  1 root              adm               10528 nov 24 16:30 kern.log.2.gz
-rw-r-----  1 root              adm               20605 out 14  2024 kern.log.3.gz
-rw-r-----  1 root              adm               81932 jul 10  2024 kern.log.4.gz
-rw-rw-r--  1 root              utmp             292584 dez  5 22:47 lastlog
drwx--x--x  2 root              root               4096 dez  6 10:45 lightdm
-rw-r-xr-x  2 root              root               4096 mar  2  2024 openvpn
-rw-rwxr-x  2 root              root               4096 dez  2 23:00 postgresql
-rw-------  2 root              root               4096 mai 27  2024 private
lrwxrwxrwx  1 root              root                 39 mai 27  2024 README -> ../../usr/share/doc/systemd/README.logs
drwxr-xr-x  5 root              root               4096 nov 27 20:56 runit
drwx------  2 root              root               4096 mar 13  2024 speech-dispatcher
drwxr-xr-x  2 root              root               4096 jul  1  2024 squid
drwxr-xr-x  2 root              root               4096 dez  5 21:54 suricata
-rw-r-----  1 root              adm             2020220 dez  6 10:47 syslog
-rw-r-----  1 root              adm              976302 dez  2 23:00 syslog.1
-rw-r-----  1 root              adm               32682 nov 24 16:30 syslog.2.gz
-rw-r-----  1 root              adm               70309 out 14  2024 syslog.3.gz
-rw-r-----  1 root              adm              280466 jul 10  2024 syslog.4.gz
drwxr-xr-x  2 root              root               4096 jan 15  2024 sysstat
drwxr-s---  2 debian-tor        adm                4096 jul  4  2024 tor
drwxr-x---  2 root              adm               4096 dez  5 21:54 unattended-upgrades
-rw-r-----  1 root              adm                4400 dez  6 10:45 user.log
-rw-r-----  1 root              adm               15587 dez  2 23:00 user.log.1
-rw-r-----  1 root              adm                 992 nov 24 16:30 user.log.2.gz
-rw-r-----  1 root              root                265 jul  4  2024 vbox-install.log
-rw-r--r--  1 root              root                 37 dez  6 10:45 vbox-setup.log
-rw-r--r--  1 root              root                 37 dez  5 23:08 vbox-setup.log.1
-rw-r--r--  1 root              root                 37 dez  5 22:49 vbox-setup.log.2
-rw-r--r--  1 root              root                 37 dez  5 22:37 vbox-setup.log.3
-rw-r--r--  1 root              root                 37 dez  5 21:46 vbox-setup.log.4
-rw-rw-r--  1 root              utmp             47616 dez  5 22:47 wtmp
-rw-r--r--  1 root              root               8192 dez  5 22:47 wtmp.db
-rw-r-----  1 xrdp              adm               37771 dez  6 10:46 xrdp.log
-rw-r-----  1 xrdp              adm                1778 dez  2 23:00 xrdp.log.1.gz
-rw-r-----  1 xrdp              adm                 1166 nov 24 16:30 xrdp.log.2.gz
-rw-r-----  1 xrdp              adm                 1894 out 14  2024 xrdp.log.3.gz
-rw-r-----  1 xrdp              adm                 1347 jul  4  2024 xrdp.log.4.gz
```

Entre os arquivos e diretórios observados estão registros relacionados a autenticação, inicialização, kernel, serviços, rede, Docker, Suricata, OpenVPN, sessões de usuário e outros componentes do sistema.

---

## 3. Explorando o `syslog`

O arquivo `syslog` contém registros gerais de diversos componentes e serviços do sistema.

Para visualizar seu conteúdo, foi executado:

```bash id="q6v3bn"
cat /var/log/syslog
```

Parte da saída apresentada:

```text id="srz0th"
2025-12-02T23:00:27.696849-03:00 ip-192-168-98-40 systemd[1]: rsyslog.service: Sent signal SIGHUP to main process 746 (rsyslogd) on client request.
2025-12-02T23:00:27.697808-03:00 ip-192-168-98-40 rsyslogd: [origin software="rsyslogd" swVersion="8.2510.0" x-pid="746" x-info="https://www.rsyslog.com"] rsyslogd was HUPed
2025-12-02T23:00:27.790481-03:00 ip-192-168-98-40 systemd[1]: logrotate.service: Deactivated successfully.
2025-12-02T23:00:27.790791-03:00 ip-192-168-98-40 systemd[1]: Finished logrotate.service - Rotate log files.
2025-12-02T23:00:27.801578-03:00 ip-192-168-98-40 cloud-init[509]: Cloud-init v. 25.3 running 'modules:config' at Wed, 03 Dec 2025 02:00:27 +0000. Up 14.28 seconds.
2025-12-02T23:00:27.869909-03:00 ip-192-168-98-40 sh[1097]: Completed socket interaction for boot stage config

...
```

A saída demonstra que diferentes componentes podem escrever informações no mesmo arquivo de log. No exemplo, aparecem eventos relacionados ao `systemd`, `rsyslogd`, `logrotate` e `cloud-init`.

---

## 4. Consultando o journal do sistema

Além dos arquivos tradicionais em `/var/log`, o Kali Linux utiliza o **systemd journal**, que pode ser consultado através do comando `journalctl`.

Para visualizar os registros referentes à inicialização atual, foi executado:

```bash id="y5r8ck"
journalctl -b
```

Parte da saída:

```text id="q75pkl"
dez 06 10:45:41 kali kernel: Linux version 6.16.8+kali-cloud-amd64 (devel@kali.org) (x86_64-linux-gnu-gcc->
dez 06 10:45:41 kali kernel: Command line: BOOT_IMAGE=/boot/vmlinuz-6.16.8+kali-cloud-amd64 root=UUID=03b8>
dez 06 10:45:41 kali kernel: BIOS-provided physical RAM map:
dez 06 10:45:41 kali kernel: BIOS-e820: [mem 0x0000000000000000-0x000000000009fbff] usable
dez 06 10:45:41 kali kernel: BIOS-e820: [mem 0x000000000009fc00-0x000000000009ffff] reserved
dez 06 10:45:41 kali kernel: BIOS-e820: [mem 0x00000000000f0000-0x00000000000fffff] reserved
dez 06 10:45:41 kali kernel: BIOS-e820: [mem 0x0000000000100000-0x00000000bffe8fff] usable
dez 06 10:45:41 kali kernel: BIOS-e820: [mem 0x00000000bffe9000-0x00000000bfffffff] reserved
dez 06 10:45:41 kali kernel: BIOS-e820: [mem 0x00000000e0000000-0x00000000e03fffff] reserved
dez 06 10:45:41 kali kernel: BIOS-e820: [mem 0x00000000fffc0000-0x00000000ffffffff] reserved
dez 06 10:45:41 kali kernel: BIOS-e820: [mem 0x0000000100000000-0x000000013cffffff] usable
dez 06 10:45:41 kali kernel: BIOS-e820: [mem 0x000000013d000000-0x000000013fffffff] reserved
dez 06 10:45:41 kali kernel: printk: legacy bootconsole [earlyser0] enabled
dez 06 10:45:41 kali kernel: NX (Execute Disable) protection: active
dez 06 10:45:41 kali kernel: APIC: Static calls initialized
dez 06 10:45:41 kali kernel: SMBIOS 2.7 present.
dez 06 10:45:41 kali kernel: DMI: Amazon EC2 t3a.medium/, BIOS 1.0 10/16/2017
dez 06 10:45:41 kali kernel: DMI: Memory slots populated: 1/1
dez 06 10:45:41 kali kernel: Hypervisor detected: KVM

...
```

Os registros mostram informações do processo de inicialização do sistema, incluindo a versão do kernel, parâmetros de boot, memória disponível, informações de BIOS e a detecção do hypervisor KVM.

---

## 5. Pesquisando ocorrências com `grep`

Para localizar linhas do `syslog` que contêm a palavra `error`, foi utilizado:

```bash id="h2m6vx"
grep "error" /var/log/syslog
```

Parte da saída:

```text id="t4nnc5"
2025-12-02T23:00:28.076703-03:00 ip-192-168-98-40 containerd[1076]: time="2025-12-02T23:00:28.075234187-03:00" level=info msg="skip loading plugin \"io.containerd.snapshotter.v1.blockfile\"..." error="no scratch file generator: skip plugin" type=io.containerd.snapshotter.v1
2025-12-02T23:00:28.076787-03:00 ip-192-168-98-40 containerd[1076]: time="2025-12-02T23:00:28.075518179-03:00" level=info msg="skip loading plugin \"io.containerd.snapshotter.v1.btrfs\"..." error="path /var/lib/containerd/io.containerd.snapshotter.v1.btrfs (ext4) must be a btrfs filesystem to be used with the btrfs snapshotter: skip plugin" type=io.containerd.snapshotter.v1
2025-12-02T23:00:28.076870-03:00 ip-192-168-98-40 containerd[1076]: time="2025-12-02T23:00:28.075568919-03:00" level=info msg="skip loading plugin \"io.containerd.snapshotter.v1.devmapper\"..." error="devmapper not configured: skip plugin" type=io.containerd.snapshotter.v1
...
```

O comando realiza uma busca textual pela sequência `error`. Portanto, encontrar a palavra na linha não significa necessariamente que o evento possua nível de severidade `error`.

Nesse caso, as linhas apresentadas possuem:

```text
level=info
```

e a palavra `error` aparece dentro dos detalhes da mensagem do `containerd`, indicando motivos pelos quais determinados plugins não foram carregados.

---

## 6. Acessando o aplicativo Logs

Após a análise pelo terminal, foi encerrada a sessão administrativa com:

```bash id="u7x3pd"
exit
```

Em seguida, foi aberto o aplicativo:

```text id="c8m4zr"
Logs
```

O aplicativo **Logs**, também conhecido como **GNOME Logs**, fornece uma interface gráfica para consultar os registros do sistema.

---

## 7. Explorando as categorias do GNOME Logs

No painel do aplicativo foram observadas categorias como:

* **Important**
* **All**
* **Applications**
* **System**
* **Security**
* **Hardware**

Cada categoria permite concentrar a visualização em determinados tipos de registros.

### Applications

Apresenta registros relacionados aos aplicativos executados no sistema.

### System

Exibe eventos relacionados ao funcionamento do sistema operacional e seus componentes.

### Security

Concentra registros relacionados à segurança e atividades relevantes para análise do sistema.

### Hardware

Apresenta eventos relacionados aos dispositivos e componentes de hardware reconhecidos pelo sistema.

---

## 8. Explorando a seção Security

A categoria:

```text id="n9b2wk"
Security
```

foi selecionada no aplicativo **Logs**.

Nessa seção são apresentados registros relacionados à segurança do sistema, permitindo observar eventos que podem ser relevantes durante uma investigação ou análise de comportamento do ambiente.

---

## 9. Evidência

O print obrigatório da atividade corresponde ao **passo 10**, mostrando a seção **Security** do aplicativo **Logs** do GNOME.

**Frase obrigatória antes do print:**

> **Print da atividade 12.3:** seção `Security` do aplicativo `Logs` do GNOME no Kali Linux, exibindo os registros relacionados à segurança do sistema.

[**Evidências — Módulo 12 / Aulas 45 e 46**](../evidencias.pdf)

---

## Conceitos

* **`/var/log`:** diretório tradicional utilizado pelo Linux para armazenar registros.
* **`syslog`:** registro geral de eventos gerados por diferentes componentes e serviços.
* **`journalctl`:** ferramenta para consultar o journal mantido pelo `systemd`.
* **`grep`:** ferramenta utilizada para pesquisar padrões em arquivos de texto.
* **GNOME Logs:** interface gráfica para consulta de registros do sistema.
* **Log de segurança:** registro que pode auxiliar na identificação e investigação de atividades relacionadas à segurança.

## Fluxo

```text id="x3v7qm"
Kali Linux
    ↓
/var/log
    ↓
syslog
    ↓
journalctl -b
    ↓
grep "error"
    ↓
GNOME Logs
    ↓
Security
```

## Resultado

Foram explorados os principais mecanismos de registro do Kali Linux, incluindo `/var/log`, `syslog`, `journalctl` e o aplicativo **Logs** do GNOME.

Também foi realizada uma busca textual por `error` no `syslog` e analisada a categoria **Security** na interface gráfica.
