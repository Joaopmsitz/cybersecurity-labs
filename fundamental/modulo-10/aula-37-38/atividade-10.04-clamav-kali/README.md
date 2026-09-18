# Atividade 10.4 — ClamAV no Kali Linux

## Objetivo

Instalar, atualizar e utilizar o **ClamAV** no Kali Linux para realizar uma verificação de arquivos, analisando também a versão do mecanismo, a atualização das bases de assinaturas e as informações de configuração do antivírus.

---

## Ambiente

* **Sistema:** Kali GNU/Linux Rolling
* **Ferramenta:** ClamAV
* **Versão:** 1.4.3
* **Acesso:** RDP
* **Máquina:** Kali Linux
* **Diretório analisado:** `/home`

> As credenciais utilizadas para acesso ao laboratório não são registradas neste README.

---

## 1. Acesso ao terminal como root

Após acessar a máquina Kali Linux, foi aberto um terminal e executado:

```bash
sudo -i
```

O terminal passou a operar com privilégios de `root`.

---

## 2. Verificação da versão do ClamAV

Foi executado:

```bash
clamscan --version
```

Saída:

```text
ClamAV 1.4.3/27833/Thu Nov 27 06:13:22 2025
```

A saída apresenta a versão do mecanismo do ClamAV e a versão da base de dados de assinaturas disponível inicialmente no ambiente.

---

## 3. Parada do serviço de atualização automática

Antes de realizar a atualização manual da base de assinaturas, foi interrompido o serviço `clamav-freshclam`:

```bash
systemctl stop clamav-freshclam.service
```

Essa etapa evita que o serviço de atualização automática entre em conflito com a execução manual do `freshclam`.

---

## 4. Atualização da base de assinaturas

Foi executado:

```bash
freshclam
```

Saída:

```text
Fri Dec  5 17:43:00 2025 -> ClamAV update process started at Fri Dec  5 17:43:00 2025
Fri Dec  5 17:43:00 2025 -> daily database available for update (local version: 27833, remote version: 27841)
Current database is 8 versions behind.
Downloading database patch # 27834...
Time:    0.1s, ETA:    0.0s [========================>]    1.58KiB/1.58KiB
Downloading database patch # 27835...
Time:    0.0s, ETA:    0.0s [========================>]       791B/791B
Downloading database patch # 27836...
Time:    0.1s, ETA:    0.0s [========================>]    3.39KiB/3.39KiB
Downloading database patch # 27837...
Time:    0.1s, ETA:    0.0s [========================>]    2.18KiB/2.18KiB
Downloading database patch # 27838...
Time:    0.1s, ETA:    0.0s [========================>]      1023B/1023B
Downloading database patch # 27839...
Time:    0.1s, ETA:    0.0s [========================>]    3.99KiB/3.99KiB
Downloading database patch # 27840...
Time:    0.1s, ETA:    0.0s [========================>]    4.57KiB/4.57KiB
Downloading database patch # 27841...
Time:    0.1s, ETA:    0.0s [========================>]       790B/790B
Fri Dec  5 17:43:03 2025 -> Testing database: '/var/lib/clamav/tmp.6ea2feafb0/clamav-a484adb123cfedf1746b313bb5ea45b2.tmp-daily.cld' ...
Fri Dec  5 17:43:13 2025 -> Database test passed.
Fri Dec  5 17:43:13 2025 -> daily.cld updated (version: 27841, sigs: 2077269, f-level: 90, builder: svc.clamav-publisher)
Fri Dec  5 17:43:13 2025 -> main.cvd database is up-to-date (version: 62, sigs: 6647427, f-level: 90, builder: sigmgr)
Fri Dec  5 17:43:13 2025 -> bytecode.cld database is up-to-date (version: 339, sigs: 80, f-level: 90, builder: nrandolp)
WARNING: Fri Dec  5 17:43:13 2025 -> Clamd was NOT notified: Can't connect to clamd through /var/run/clamav/clamd.ctl: No such file or directory
```

A base `daily.cld` foi atualizada da versão **27833** para a **27841**, totalizando **8 versões de diferença**.

O teste da nova base foi concluído com:

```text
Database test passed.
```

Foi apresentada também uma mensagem de aviso informando que o `clamd` não foi notificado porque o socket `/var/run/clamav/clamd.ctl` não estava disponível. Isso não impediu a atualização da base de assinaturas.

---

## 5. Verificação do diretório `/home`

Com a base atualizada, foi executado:

```bash
clamscan -r /home
```

A opção `-r` realiza a verificação de forma recursiva, permitindo que o ClamAV percorra os diretórios e subdiretórios encontrados em `/home`.

Parte da saída apresentada durante a análise:

```text
┌──(root㉿kali)-[~]
└─# clamscan -r /home
Loading:    21s, ETA:   0s [========================>]    8.71M/8.71M sigs       
Compiling:   5s, ETA:   0s [========================>]       41/41 tasks 

/home/aluno/.zshrc: OK
/home/aluno/.xsession-errors: OK
/home/aluno/.local/share/nautilus/scripts/Terminal: OK
/home/aluno/.local/share/keyrings/login.keyring: OK
/home/aluno/.local/share/keyrings/user.keystore: OK
/home/aluno/.local/share/xrdp/xrdp-chansrv.10.log: OK
/home/aluno/.local/share/torbrowser/tbb/x86_64/tor-browser/start-tor-browser.desktop: OK 

...

----------- SCAN SUMMARY -----------
Known viruses: 8708962
Engine version: 1.4.3
Scanned directories: 1015
Scanned files: 6128
Infected files: 0
Data scanned: 1319.81 MB
Data read: 1553.00 MB (ratio 0.85:1)
Time: 583.507 sec (9 m 43 s)
Start Date: 2025:12:05 17:45:28
End Date:   2025:12:05 17:55:12
```

O `clamscan` verificou recursivamente o diretório `/home`.

O resultado mais importante do resumo foi:

```text
Scanned directories: 1015
Scanned files: 6128
Infected files: 0
Data scanned: 1319.81 MB
Data read: 1553.00 MB (ratio 0.85:1)
Time: 583.507 sec (9 m 43 s)
```

Portanto, **nenhum arquivo foi identificado como infectado pelo ClamAV durante essa verificação**.

---

## Evidência — Passo 5

**Frase obrigatória antes do print:**

> **Print da atividade 10.4:** resultado da verificação recursiva do diretório `/home` realizada pelo ClamAV, incluindo o `SCAN SUMMARY` com a quantidade de arquivos analisados e o resultado de arquivos infectados.

[**Evidências — Módulo 10 / Aulas 37 e 38**](../evidencias.pdf)

---

## 6. Análise do resumo da verificação

Após a conclusão do `clamscan`, foram analisadas as informações apresentadas no `SCAN SUMMARY`.

Os principais dados observados foram:

| Informação            |  Resultado |
| --------------------- | ---------: |
| Versão do mecanismo   |      1.4.3 |
| Diretórios analisados |       1015 |
| Arquivos analisados   |       6128 |
| Arquivos infectados   |          0 |
| Dados analisados      | 1319.81 MB |
| Dados lidos           | 1553.00 MB |
| Tempo de execução     | 9 min 43 s |

---

## 7. Verificação das configurações do ClamAV

Foi executado:

```bash
clamconf
```

O comando apresentou as configurações existentes no ambiente, além das informações relacionadas ao mecanismo e às bases de assinaturas.

Parte relevante da saída:

```text
Checking configuration files in /etc/clamav

Config file: clamd.conf
-----------------------
AlertExceedsMax disabled
CacheSize = "65536"
PreludeEnable disabled
PreludeAnalyzerName = "ClamAV"
LogFile = "/var/log/clamav/clamav.log"
LogFileUnlock disabled
LogFileMaxSize = "9223372036854775807"
LogTime = "yes"
LogClean disabled

...

clamav-milter.conf not found

Software settings
-----------------
Version: 1.4.3
Optional features supported: MEMPOOL AUTOIT_EA06 ICONV 

Database information
--------------------
Database directory: /var/lib/clamav
bytecode.cld: version 339, sigs: 80, built on Thu Sep 11 09:29:19 2025
main.cvd: version 62, sigs: 6647427, built on Thu Sep 16 09:32:42 2021
daily.cld: version 27841, sigs: 2077269, built on Fri Dec  5 06:23:11 2025
Total number of signatures: 8724776

Platform information
--------------------
uname: Linux 6.16.8+kali-cloud-amd64 #1 SMP PREEMPT_DYNAMIC Kali 6.16.8-1kali1 (2025-09-24) x86_64
OS: Linux, ARCH: x86_64, CPU: x86_64
Full OS version: Kali GNU/Linux Rolling
zlib version: 1.3.1 (1.3.1), compile flags: a9
platform id: 0x0a21d5d508000000000e0300

Build information
-----------------
GNU C: 14.3.0
sizeof(void*) = 8
Engine flevel: 213, dconf: 213
```

A saída confirmou, entre outros dados, que:

* O ClamAV utilizado era a versão **1.4.3**.
* A base `daily.cld` estava na versão **27841** após a atualização.
* O diretório das bases era `/var/lib/clamav`.
* O total informado era de **8.724.776 assinaturas**.
* O sistema utilizado era **Kali GNU/Linux Rolling**, arquitetura `x86_64`.

---

## 8. Encerramento

Após a análise das configurações do ClamAV, a atividade foi encerrada.

---

## Conceitos

* **ClamAV:** antivírus de código aberto utilizado para detecção de malware.
* **Freshclam:** ferramenta responsável pela atualização das bases de assinaturas.
* **Clamscan:** utilitário de linha de comando utilizado para realizar verificações.
* **Assinaturas:** informações utilizadas pelo mecanismo para identificar ameaças conhecidas.
* **Scan recursivo:** permite verificar um diretório e seus subdiretórios.

## Fluxo da atividade

```text
Verificar versão
      ↓
Parar atualização automática
      ↓
Atualizar assinaturas
      ↓
Verificar /home
      ↓
Analisar SCAN SUMMARY
      ↓
Consultar configurações
```

## Resultado

O ClamAV foi atualizado e utilizado para analisar recursivamente o diretório `/home`.

Foram verificados **6128 arquivos**, sem identificação de arquivos infectados na análise realizada.
