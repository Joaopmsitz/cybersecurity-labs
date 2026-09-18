# Fundamental

Documentação da etapa **Fundamental** do programa Hackers do Bem: 12 módulos, cada um dividido em duas aulas, cobrindo desde integridade de arquivos e hashing até forense básica e análise de tráfego.

Cada atividade possui sua própria pasta com objetivo, ambiente, procedimento, comandos utilizados, resultado e conceitos praticados. As evidências de cada aula estão reunidas em um `evidencias.pdf` dentro da respectiva pasta de aula.

## Módulos

### Módulo 01 — Integridade, Hashing e Reconhecimento Inicial
**Aula 01-02:** integridade de texto · integridade de arquivos · hash · criptografia · Taskwarrior
**Aula 03-04:** phishing · WHOIS · Maltego · OSINT · adversarial ML

### Módulo 02 — Malware e Anonimato
**Aula 05-06:** trojan de acesso remoto · keylogger (XSpy) · ransomware · múltiplos payloads de malware · Windows Defender vs. keylogger
**Aula 07-08:** ccrypt · logcheck · Tor Browser · deep web / Tor · políticas de segurança do Windows

### Módulo 03 — Reconhecimento e Testes de Intrusão
**Aula 09-10:** ExploitDB · Nmap · Burp Suite · Netcat listener · Ncat (redirecionamento de portas)
**Aula 11-12:** diagnóstico de rede · honeypot (Pentbox) · enumeração DNS (host, nslookup, dig)

### Módulo 04 — Autenticação e Controle de Acesso
**Aula 13-14:** controle de autenticação · SELinux · KeePassXC · John the Ripper (dicionário) · credential manager
**Aula 15-16:** RADIUS · Google Authenticator · Google Authenticator no Firefox · TPM/USB · OTP Client

### Módulo 05 — Active Directory
**Aula 17-18:** Active Directory · Domain Controller · usuário no AD · cliente no domínio · política de senhas (GPO)
**Aula 19-20:** DAC no Windows · OU no Active Directory · DAC no Kali · RBAC no Kali · rotação de senha no Kali

### Módulo 06 — Automação e Segurança Web
**Aula 21-22:** reuso de código em Python · JDK/NetBeans · automação em Python · assinaturas ClamAV · PowerShell
**Aula 23-24:** HTTP via cURL · encurtador de URL com QR code · clickjacking · verificação de clickjacking · SQL injection

### Módulo 07 — Backup e Descarte Seguro
**Aula 25-26:** RAID 0 no Kali · RAID 1 no Kali · rsync manual · rsync via cron · backup no OneDrive
**Aula 27-28:** Duplicity (backup completo) · Duplicity (backup diferencial) · formatação completa · sobrescrita simples · sobrescrita DoD

### Módulo 08 — Criptografia
**Aula 29-30:** esteganografia no Kali · ofuscação em Python · AES-256 · 3DES · Blowfish
**Aula 31-32:** hash MD5/RIPEMD-160/BLAKE2 · hash SHA · RSA-2048 (confidencialidade) · ECC-256 (confidencialidade) · RSA-2048 (assinatura digital)

### Módulo 09 — Certificados Digitais
**Aula 33-34:** criando autoridade certificadora · emitindo certificados · conhecendo certificado digital · avaliando certificados web · certificado autoassinado no Kali
**Aula 35-36:** revogando certificado (Windows Server) · cancelando revogação (Windows Server) · verificando certificados web via OCSP no Kali · criando carteira Bitcoin (Electrum) · recuperando carteira Bitcoin (Electrum)

### Módulo 10 — Hardening e Virtualização
**Aula 37-38:** integridade de memória / manutenção (Windows Server) · controle de aplicativos e navegadores (Windows Server) · atualizações (Windows Server) · ClamAV no Kali · Suricata no Kali
**Aula 39-40:** hypervisor tipo 2 no Kali · criando VM Debian no VirtualBox · UEFI/BIOS (simulação) · full disk encryption no Kali · container Ubuntu com Docker no Kali

### Módulo 11 — Redes e Firewall
**Aula 41-42:** tabela ARP no Kali · alias de interface de rede no Kali · MAC cloning no Kali · QoS no Kali · QoS no Windows Server
**Aula 43-44:** ACL/firewall no Windows Server 2022 · bloqueando sites com iptables (Kali) · redirecionando DNS com iptables (Kali) · OpenVPN no Kali · bloqueando ICMP (Windows Server + Kali)

### Módulo 12 — Logs e Forense Básica
**Aula 45-46:** logs no Windows Server 2022 · NTP no Windows Server 2022 · explorando logs no Kali · capturando pacotes com Wireshark no Kali · analisando pacotes TLS com tcpdump/Wireshark
**Aula 47-48:** lendo metadados no Kali · apagando metadados no Kali · escrevendo metadados no Kali · explorando o TSK (The Sleuth Kit) no Kali · aquisição de imagem de disco no Kali

## Estrutura de Pastas

```
fundamental/
├── README.md
├── modulo-01/
│   ├── aula-01-02/
│   │   ├── atividade-1.1-integridade-texto/
│   │   ├── atividade-1.2-integridade-arquivos/
│   │   ├── ...
│   │   └── evidencias.pdf
│   └── aula-03-04/
│       ├── atividade-1.6-phishing/
│       ├── ...
│       └── evidencias.pdf
├── modulo-02/
│   └── ...
...
└── modulo-12/
    └── ...
```

## Voltar

→ [Repositório principal](../README.md)
