# Atividade 4.1 — Modificando os parâmetros de Controle de Autenticação no Kali Linux

## Objetivo

Modificar e validar a senha de autenticação de um usuário no **Kali Linux**, observando também como as informações de usuários e grupos são organizadas nos arquivos `/etc/passwd` e `/etc/group`.

A atividade foi realizada em ambiente acadêmico controlado e teve como objetivo compreender o funcionamento básico do controle de autenticação baseado em senha no Linux.

---

## Ambiente

* **Sistema:** Kali Linux
* **Usuário utilizado:** `aluno`
* **Ferramentas/comandos:** `whoami`, `pwd`, `cat`, `sudo`, `passwd`
* **Arquivos analisados:** `/etc/passwd` e `/etc/group`

---

## 1. Identificação do usuário e diretório atual

Inicialmente, foram executados os comandos `whoami` e `pwd`:

```bash
whoami
pwd
```

Saída:

```text
┌──(aluno㉿kali)-[~]
└─$ whoami
aluno
                                                                                   
┌──(aluno㉿kali)-[~]
└─$ pwd
/home/aluno
```

O comando `whoami` informa o usuário associado ao processo atual.

Já o comando `pwd` (**Print Working Directory**) mostra o caminho completo do diretório de trabalho atual.

Neste caso:

* Usuário atual: `aluno`
* Diretório inicial: `/home/aluno`

---

## 2. Análise do arquivo `/etc/passwd`

Em seguida, foi consultado o arquivo `/etc/passwd`:

```bash
cat /etc/passwd
```

Saída observada:

```text
root:x:0:0:root:/root:/usr/bin/zsh
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/run/ircd:/usr/sbin/nologin
_apt:x:42:65534::/nonexistent:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-network:x:998:998:systemd Network Management:/:/usr/sbin/nologin
messagebus:x:100:107::/nonexistent:/usr/sbin/nologin
tcpdump:x:101:109::/nonexistent:/usr/sbin/nologin
sshd:x:102:65534::/run/sshd:/usr/sbin/nologin
polkitd:x:997:997:polkit:/nonexistent:/usr/sbin/nologin
_chrony:x:103:111:Chrony daemon,,,:/var/lib/chrony:/usr/sbin/nologin
kali:x:1000:1001:Kali Linux:/home/kali:/bin/zsh
aluno:x:1001:1002::/home/aluno:/bin/bash
rtkit:x:104:112:RealtimeKit,,,:/proc:/usr/sbin/nologin
usbmux:x:105:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
avahi:x:106:113:Avahi mDNS daemon,,,:/run/avahi-daemon:/usr/sbin/nologin
lightdm:x:107:114:Light Display Manager:/var/lib/lightdm:/bin/false
pulse:x:108:115:PulseAudio daemon,,,:/run/pulse:/usr/sbin/nologin
saned:x:109:118::/var/lib/saned:/usr/sbin/nologin
colord:x:110:119:colord colour management daemon,,,:/usr/sbin/nologin
xrdp:x:111:121::/run/xrdp:/usr/sbin/nologin
Debian-exim:x:112:122::/var/spool/exim4:/usr/sbin/nologin
logcheck:x:113:123:logcheck system account,,,:/var/lib/logcheck:/usr/sbin/nologin
debian-tor:x:114:124::/var/lib/tor:/bin/false
clamav:x:115:125::/var/lib/clamav:/bin/false
geoclue:x:116:126::/var/lib/geoclue:/usr/sbin/nologin
postgres:x:117:130:PostgreSQL administrator,,,:/var/lib/postgresql:/bin/bash
```

O `/etc/passwd` é um arquivo de configuração que mantém informações básicas das contas locais.

Cada entrada possui sete campos separados por `:`:

```text
usuário:senha:UID:GID:GECOS:home:shell
```

Tomando como exemplo a conta `aluno`:

```text
aluno:x:1001:1002::/home/aluno:/bin/bash
```

* `aluno` — nome da conta.
* `x` — indica que o hash da senha não fica armazenado diretamente nesse arquivo; em sistemas Linux modernos, ele fica normalmente em `/etc/shadow`.
* `1001` — UID (**User ID**) do usuário.
* `1002` — GID (**Group ID**) do grupo primário.
* campo vazio — campo GECOS/comentário.
* `/home/aluno` — diretório pessoal.
* `/bin/bash` — shell de login.

---

## 3. Análise do arquivo `/etc/group`

Foi consultado o arquivo responsável pelas informações dos grupos:

```bash
cat /etc/group
```

Saída:

```text
root:x:0:
daemon:x:1:
bin:x:2:
sys:x:3:
adm:x:4:kali,logcheck
tty:x:5:
disk:x:6:
lp:x:7:
mail:x:8:
news:x:9:
uucp:x:10:
man:x:12:
proxy:x:13:
kmem:x:15:
dialout:x:20:kali
fax:x:21:
voice:x:22:
cdrom:x:24:kali
floppy:x:25:kali
tape:x:26:
sudo:x:27:kali,aluno
audio:x:29:kali,pulse
dip:x:30:kali
www-data:x:33:
backup:x:34:
operator:x:37:
list:x:38:
irc:x:39:
src:x:40:
shadow:x:42:
utmp:x:43:
video:x:44:kali
sasl:x:45:
plugdev:x:46:kali
staff:x:50:
games:x:60:
users:x:100:
nogroup:x:65534:
systemd-journal:x:999:
systemd-network:x:998:
crontab:x:101:
input:x:102:
sgx:x:103:
kvm:x:104:
render:x:105:
netdev:x:106:kali
messagebus:x:107:
_ssh:x:108:
tcpdump:x:109:
polkitd:x:997:
kali-trusted:x:110:
_chrony:x:111:
lxd:x:1000:kali
kali:x:1001:
aluno:x:1002:
rtkit:x:112:
avahi:x:113:
lightdm:x:114:
pulse:x:115:
pulse-access:x:116:
scanner:x:117:saned
saned:x:118:
colord:x:119:
ssl-cert:x:120:aluno,postgres
xrdp:x:121:
Debian-exim:x:122:
logcheck:x:123:
debian-tor:x:124:
clamav:x:125:
geoclue:x:126:
vboxusers:x:127:
docker:x:128:
_cvsadmin:x:129:
postgres:x:130:
```

O formato das entradas é:

```text
grupo:senha:GID:membros
```

Por exemplo:

```text
sudo:x:27:kali,aluno
```

indica o grupo `sudo`, com GID `27`, tendo `kali` e `aluno` como membros.

A consulta também mostra que o usuário `aluno` possui associação ao grupo `sudo`, permitindo a execução de comandos administrativos mediante autenticação.

---

## 4. Alteração da senha do usuário

Para alterar a senha da conta `aluno`, foi obtido acesso administrativo:

```bash
sudo -i
```

Depois, foi utilizado:

```bash
passwd aluno
```

O sistema solicitou a nova senha duas vezes e confirmou a alteração:

```text
┌──(aluno㉿kali)-[~]
└─$ sudo -i
[sudo] senha para aluno:

┌──(root㉿kali)-[~]
└─# passwd aluno
Nova senha:
Redigite a nova senha:
passwd: senha atualizada com sucesso
```

A mensagem:

```text
passwd: senha atualizada com sucesso
```

confirma que a alteração foi realizada.

A senha utilizada no laboratório não é reproduzida neste README.

---

## 5. Validação da nova autenticação

Após alterar a senha, foi encerrada a sessão gráfica do usuário.

Em seguida, o Kali Linux foi inicializado novamente e a nova senha definida no passo anterior foi utilizada para autenticação.

O login foi realizado com sucesso, demonstrando que a alteração efetuada pelo comando `passwd` foi aplicada corretamente.

---

## 6. Restauração da senha original

Após validar a nova credencial, foi repetido o procedimento de alteração da senha para restaurar a credencial original utilizada pelo laboratório.

O procedimento foi realizado através do comando:

```bash
sudo -i
passwd aluno
```

Após a confirmação da alteração, a sessão foi encerrada novamente.

Essa etapa garante que o ambiente do laboratório permaneça com a configuração esperada para as atividades seguintes.

---

## Conceitos praticados

### `/etc/passwd`

Arquivo que armazena informações básicas das contas locais do Linux, como nome do usuário, UID, GID, diretório pessoal e shell.

### `/etc/group`

Arquivo que mantém informações sobre os grupos locais e seus respectivos membros.

### UID e GID

* **UID:** identificador numérico de um usuário.
* **GID:** identificador numérico de um grupo.

### `/etc/shadow`

Embora não tenha sido necessário consultar seu conteúdo nesta atividade, o `/etc/shadow` é utilizado pelo Linux para armazenar os hashes das senhas e informações relacionadas à expiração e validade das credenciais.

### `passwd`

Comando utilizado para definir ou alterar a senha de uma conta local.

### `sudo`

Permite que usuários autorizados executem comandos com privilégios administrativos.

---

## Resultado

A atividade demonstrou o funcionamento básico do controle de autenticação por senha no Kali Linux.

Foi possível:

* identificar o usuário atualmente autenticado;
* verificar o diretório de trabalho;
* analisar a estrutura do `/etc/passwd`;
* analisar a estrutura do `/etc/group`;
* compreender a relação entre usuários, UIDs e GIDs;
* alterar a senha de uma conta com `passwd`;
* validar a nova autenticação;
* restaurar a configuração original do laboratório.

A atividade reforça a importância do gerenciamento adequado de credenciais e dos mecanismos de controle de acesso presentes em sistemas Linux.

---

## Evidência

[**Evidências — Módulo 4 / Aulas 1 e 2**](../evidencias.pdf)

**Print registrado:** etapa 7 da atividade, conforme solicitado pelo roteiro, referente à validação da autenticação após a alteração e restauração da senha.

