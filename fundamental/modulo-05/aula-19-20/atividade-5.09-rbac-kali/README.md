# Atividade 5.9 — RBAC no Kali Linux

## Objetivo

Nesta atividade foi realizada uma prática relacionada ao **RBAC (Role-Based Access Control)** no Kali Linux.

O exercício consiste em criar um grupo específico para uma função, adicionar um usuário a esse grupo e associar o grupo ao arquivo utilizado na atividade. Dessa forma, o acesso ao recurso pode ser administrado por meio da associação do usuário ao grupo responsável pela função.

---

## Ambiente

* **Sistema:** Kali Linux
* **Acesso:** RDP
* **IP da máquina:** `192.168.98.40`
* **Usuário:** `aluno`
* **Diretório utilizado:** `/home/aluno/Documentos/`

> As credenciais utilizadas no laboratório não são registradas neste documento.

---

## 1. Acessando o terminal

Após acessar a máquina Kali Linux por RDP, foi aberto o terminal e obtido acesso administrativo:

```bash id="7j1s5f"
sudo -i
```

Em seguida, foi acessado o diretório utilizado na atividade:

```bash id="5g7p8d"
cd /home/aluno/Documentos/
```

---

## 2. Verificando o arquivo existente

Foi utilizado o comando `ls` para verificar os arquivos presentes no diretório:

```bash id="j3x8pw"
ls
```

Saída observada:

```text id="pg1g2u"
┌──(root㉿kali)-[/home/aluno/Documentos]
└─# ls            
texto.txt
```

O arquivo `texto.txt` corresponde ao arquivo criado na atividade anterior e será utilizado nesta prática para demonstrar a associação de permissões a um grupo.

---

## 3. Listando os usuários do sistema

Para visualizar os usuários existentes no sistema, foi executado:

```bash id="9b2h6q"
getent passwd | cut -d: -f1
```

Saída observada:

```text id="0be9x0"
root
daemon
bin
sys
sync
games
man
lp
mail
news
uucp
proxy
www-data
backup
list
irc
_apt
nobody
systemd-network
messagebus
tcpdump
sshd
polkitd
_chrony
kali
systemd-timesync
aluno
rtkit
xrdp
usbmux
avahi
pulse
saned
lightdm
colord
tss
dnsmasq
strongswan
speech-dispatcher
nm-openvpn
nm-openconnect
postgres
Debian-exim
logcheck
debian-tor
freerad
clamav
geoclue
_rpc
pipewire
statd
teste1
```

O comando utilizado combina duas operações:

```text id="8k3xj4"
getent passwd
```

consulta as entradas de usuários disponíveis através das bases configuradas no sistema.

Já:

```text id="f8v1q2"
cut -d: -f1
```

separa os campos utilizando `:` como delimitador e exibe somente o primeiro campo, que corresponde ao nome do usuário.

---

## 4. Listando os grupos do sistema

Para visualizar os grupos existentes, foi executado:

```bash id="4m0r7x"
getent group | cut -d: -f1
```

Saída observada:

```text id="x9ftzw"
root
daemon
bin
sys
adm
tty
disk
lp
mail
news
uucp
man
proxy
kmem
dialout
fax
voice
cdrom
floppy
tape
sudo
audio
dip
www-data
backup
operator
list
irc
src
shadow
utmp
video
sasl
plugdev
staff
games
users
nogroup
systemd-journal
systemd-network
crontab
input
sgx
kvm
render
netdev
messagebus
tcpdump
_ssh
polkitd
kali-trusted
_chrony
lxd
kali
systemd-timesync
aluno
rtkit
ssl-cert
xrdp
avahi
pulse
pulse-access
scanner
saned
lightdm
colord
tss
bluetooth
plocate
nm-openvpn
pipewire
nm-openconnect
postgres
wireshark
Debian-exim
logcheck
debian-tor
freerad
clamav
geoclue
docker
_cvsadmin
vboxusers
clock
teste1
```

Assim como no comando anterior, `getent group` consulta as informações de grupos e `cut -d: -f1` exibe somente o nome de cada grupo.

---

## 5. Criando o grupo de função

Para representar uma função específica dentro do ambiente, foi criado o grupo `contabilidade`:

```bash id="e4h8s2"
groupadd contabilidade
```

O comando `groupadd` cria um novo grupo no sistema.

Neste caso, o grupo utilizado no laboratório foi:

```text id="p7m3kc"
contabilidade
```

A utilização de grupos permite organizar usuários de acordo com uma determinada função ou responsabilidade.

---

## 6. Confirmando a criação do grupo

Após criar o grupo, a listagem de grupos foi executada novamente:

```bash id="r5k2w9"
getent group | cut -d: -f1
```

Ao final da saída, foi possível observar:

```text id="p0rey3"
contabilidade
```

Isso confirma que o novo grupo foi criado no sistema.

---

## 7. Adicionando o usuário ao grupo

O usuário `teste1` foi adicionado ao grupo `contabilidade` utilizando:

```bash id="c9v4n6"
usermod -aG contabilidade teste1
```

O comando possui os seguintes elementos:

* `usermod` → modifica uma conta de usuário;
* `-a` → adiciona a nova associação sem remover as associações existentes;
* `-G` → define grupos suplementares;
* `contabilidade` → grupo ao qual o usuário será adicionado;
* `teste1` → usuário que receberá a associação.

O uso de `-aG` é importante porque permite adicionar o usuário ao novo grupo preservando suas demais associações.

---

## 8. Associando o arquivo ao grupo

Depois de criar o grupo e adicionar o usuário, o grupo `contabilidade` foi associado ao arquivo `texto.txt`:

```bash id="t8w3k1"
chown :contabilidade texto.txt
```

O comando `chown` é utilizado para alterar o proprietário e/ou grupo associado a um arquivo.

Nesse caso, a sintaxe:

```text id="h5q2z7"
chown :contabilidade texto.txt
```

indica que somente o **grupo** do arquivo será alterado, mantendo o proprietário existente.

Assim, o arquivo passa a estar associado ao grupo:

```text id="n2d6x4"
contabilidade
```

---

## 9. Alterando as permissões do arquivo

Para finalizar a configuração de acesso ao recurso, foi executado:

```bash id="uln16c"
chmod 770 texto.txt
```

A permissão `770` pode ser dividida da seguinte maneira:

```text id="x7r3p9"
7    7    0
│    │    │
│    │    └── others
│    └─────── group
└──────────── owner
```

Cada número é formado pela combinação das permissões:

```text id="m4z8q1"
4 = leitura   (r)
2 = escrita    (w)
1 = execução   (x)
```

Portanto:

```text id="d9c2v5"
7 = 4 + 2 + 1 = rwx
```

Com `770`, o resultado é:

```text id="a6k1s8"
owner  → rwx
group  → rwx
others → ---
```

Ou seja:

* o proprietário possui leitura, escrita e execução;
* os membros do grupo possuem leitura, escrita e execução;
* outros usuários não possuem permissões sobre o arquivo.

Essa configuração permite utilizar o grupo como mecanismo de controle do acesso ao recurso.

---

## Conceitos envolvidos

### RBAC — Role-Based Access Control

O **RBAC (Role-Based Access Control)** é um modelo de controle de acesso no qual as permissões são associadas a funções ou papéis, e os usuários recebem acesso aos recursos por meio da sua associação a essas funções.

Em um ambiente real, por exemplo, poderia existir uma função:

```text
Contabilidade
```

e os usuários responsáveis por essa função seriam associados ao grupo correspondente.

Nesta atividade, o grupo:

```text
contabilidade
```

foi utilizado para representar essa função.

### Grupos no Linux

Os grupos permitem organizar usuários e controlar o acesso a recursos compartilhados.

Neste exercício:

```text id="e1f4u8"
Usuário:
teste1

Grupo:
contabilidade

Arquivo:
texto.txt
```

A associação pode ser representada conceitualmente como:

```text id="s3v7n2"
teste1
   │
   ▼
contabilidade
   │
   ▼
texto.txt
```

### chmod 770

A permissão `770` garante acesso completo ao proprietário e ao grupo, enquanto remove as permissões dos demais usuários.

```text id="z5k9q2"
Owner   → rwx
Group   → rwx
Others  → ---
```

Isso permite restringir o acesso ao recurso aos usuários autorizados por meio do proprietário ou do grupo.

---

## Resultado

A atividade demonstrou a criação de um grupo específico, a associação de um usuário a esse grupo e a atribuição do grupo ao arquivo utilizado no laboratório.

O fluxo realizado foi:

```text id="b2m7x6"
Criar grupo
    ↓
contabilidade
    ↓
Adicionar usuário teste1
    ↓
Associar grupo ao arquivo texto.txt
    ↓
Aplicar chmod 770
```

Dessa forma, o arquivo foi configurado para permitir acesso completo ao proprietário e aos membros do grupo `contabilidade`, enquanto os demais usuários não possuem permissões.

---

## Evidência

A evidência desta atividade corresponde ao **passo 9**, após a execução do comando:

```bash id="r8w3m1"
chmod 770 texto.txt
```

[**Evidências — Módulo 5 / Aulas 3 e 4**](../evidencias.pdf)
