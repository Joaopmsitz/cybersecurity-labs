# Atividade 4.2 — Explorando o SELinux no Kali Linux

## Objetivo

Explorar o **SELinux (Security-Enhanced Linux)** no Kali Linux, compreendendo seu funcionamento como mecanismo de **controle de acesso obrigatório (MAC — Mandatory Access Control)**.

Durante a atividade foram realizadas operações de ativação, verificação e consulta das configurações do SELinux, incluindo seu modo de operação, usuários, associações de login, variáveis booleanas e tipos de portas.

> **Atenção:** o roteiro alerta que alterações incorretas na configuração do SELinux podem causar indisponibilidade de acesso ao ambiente. As etapas foram realizadas exclusivamente no laboratório acadêmico.

---

## Ambiente

* **Sistema:** Kali Linux
* **Ferramentas:** `selinux-activate`, `sestatus`, `semanage`
* **Serviço de segurança:** SELinux
* **Política observada:** `default`

---

## 1. Acesso administrativo

Inicialmente, foi obtido acesso administrativo ao sistema:

```bash id="m8p5tz"
sudo -i
```

O `sudo -i` inicia uma sessão de shell com privilégios administrativos, permitindo executar os comandos necessários para configuração e consulta do SELinux.

---

## 2. Ativação do SELinux

O SELinux foi ativado utilizando:

```bash id="r2q8wj"
selinux-activate
```

Saída observada:

```text id="9s7m2k"
Activating SE Linux
Generating grub configuration file ...
Found background image: /usr/share/images/desktop-base/desktop-grub.png
Found linux image: /boot/vmlinuz-6.5.0-kali3-cloud-amd64
Found initrd image: /boot/initrd.img-6.5.0-kali3-cloud-amd64
Found linux image: /boot/vmlinuz-6.1.0-kali7-cloud-amd64
Found initrd image: /boot/initrd.img-6.1.0-kali7-cloud-amd64
Found linux image: /boot/vmlinuz-6.1.0-kali5-cloud-amd64
Found initrd image: /boot/initrd.img-6.1.0-kali5-cloud-amd64
done
SE Linux is activated.  You may need to reboot now.
```

O comando realizou a ativação do SELinux e regenerou a configuração do **GRUB**, identificando os kernels e respectivas imagens `initrd` disponíveis no sistema.

A mensagem final:

```text id="l2cz9d"
SE Linux is activated.  You may need to reboot now.
```

indica que uma reinicialização pode ser necessária para que a configuração entre em funcionamento.

---

## 3. Reinicialização

O sistema foi reiniciado com:

```bash id="qv4f31"
reboot
```

Durante a inicialização, o SELinux pode realizar o **relabeling** do sistema de arquivos para aplicar os contextos de segurança necessários.

O roteiro apresenta uma saída semelhante a:

```text id="1f5v8c"
*** Warning -- SELinux default policy relabel is requires.
*** Relabeling could take a very long time, dependeing on file
*** system size and speed of hard drives.
libsemanage.add_user: user sddm not in password file
Warning: Skipping the following R/O filesystems:
/run/credentials/systemd-sysctl.service
/run/credentials/systemd-sysusers.service
/run/credentials/systemd-tmpfiles-setup-dev.service
/run/credentials/systemd-tmpfiles-setup.service
Relabeling /
75.5%
```

O **relabeling** consiste na aplicação dos contextos de segurança do SELinux aos arquivos e recursos do sistema.

Como o ambiente remoto perde a conexão durante o reboot, essa etapa pode não ficar visível diretamente pela sessão RDP.

---

## 4. Verificação do status do SELinux

Após aguardar o tempo indicado pelo laboratório e iniciar novamente o Kali Linux, foi consultado o status do SELinux:

```bash id="nq0g6b"
sestatus
```

Saída observada:

```text id="6r8j3p"
SELinux status:                 enabled
SELinuxfs mount:                /sys/fs/selinux
SELinux root directory:         /etc/selinux
Loaded policy name:             default
Current mode:                   permissive
Mode from config file:          permissive
Policy MLS status:              enabled
Policy deny_unknown status:     allowed
Memory protection checking:     actual (secure)
Max kernel policy version:      33
```

### Interpretação

* **SELinux status:** `enabled` — o SELinux está habilitado.
* **SELinuxfs mount:** `/sys/fs/selinux` — ponto de montagem do sistema de arquivos utilizado pelo SELinux.
* **SELinux root directory:** `/etc/selinux` — diretório onde ficam as configurações do SELinux.
* **Loaded policy name:** `default` — política carregada.
* **Current mode:** `permissive` — violações são registradas, mas os acessos não são bloqueados pela política.
* **Mode from config file:** `permissive` — o modo configurado também é permissivo.
* **Policy MLS status:** `enabled` — suporte relacionado a MLS está habilitado.
* **Policy deny_unknown status:** `allowed` — o comportamento configurado para permissões desconhecidas é permitir.
* **Memory protection checking:** `actual (secure)` — mecanismo de verificação de proteção de memória indicado pela instalação.
* **Max kernel policy version:** `33` — versão máxima de política suportada pelo kernel apresentado.

### Enforcing x Permissive

O SELinux possui diferentes modos de operação. Os dois principais observados no roteiro são:

**Enforcing**

* As políticas são aplicadas.
* Acessos não autorizados pelas políticas podem ser bloqueados.
* As violações também podem ser registradas.

**Permissive**

* As políticas são avaliadas e as violações podem ser registradas.
* Os acessos não são efetivamente bloqueados pela política.

O laboratório apresentou o SELinux em **permissive** após a ativação.

---

## 5. Consulta dos usuários SELinux

Foi utilizada a ferramenta `semanage` para listar os usuários SELinux:

```bash id="5e7x2n"
semanage user -l
```

Saída observada:

```text id="4u9q6s"
                Rótulo     MLS/       MLS/                          
Usuário do SELinux Prefixo    Nível MCS  Intervalo MCS                  Funções do SELinux

guest_u         user       s0         s0                             guest_r
root            sysadm     s0         s0-s0:c0.c1023                 staff_r sysadm_r system_r
staff_u         staff      s0         s0-s0:c0.c1023                 staff_r sysadm_r
sysadm_u        sysadm     s0         s0-s0:c0.c1023                 sysadm_r
system_u        user       s0         s0-s0:c0.c1023                 system_r
unconfined_u    unconfined s0         s0-s0:c0.c1023                 system_r unconfined_r
user_u          user       s0         s0                             user_r
xdm             user       s0         s0                             system_r xdm_r
xguest_u        user       s0         s0                             xguest_r
```

A consulta apresenta associações entre usuários SELinux, seus níveis e as funções (**roles**) disponíveis.

Algumas funções presentes na saída:

* `guest_r` — função destinada a usuários convidados.
* `staff_r` — função relacionada a usuários de staff.
* `sysadm_r` — função administrativa.
* `system_r` — função utilizada por processos e componentes do sistema.
* `unconfined_r` — função com restrições reduzidas.
* `user_r` — função destinada a usuários comuns.
* `xdm_r` — função relacionada ao gerenciador gráfico.
* `xguest_r` — função destinada a ambientes de convidado com restrições adicionais.

---

## 6. Consulta das associações de login

Em seguida, foram consultadas as associações entre contas de login e usuários SELinux:

```bash id="1h8v5a"
semanage login -l
```

Saída:

```text id="7b4s2x"
Login Name           SELinux User         MLS/MCS Range        Service

__default__          unconfined_u         s0-s0:c0.c1023       *
root                 unconfined_u         s0-s0:c0.c1023       *
sddm                 xdm                  s0-s0                *
```

A tabela apresenta:

* **Login Name:** conta utilizada para login.
* **SELinux User:** identidade SELinux associada à conta.
* **MLS/MCS Range:** intervalo de níveis/categorias de segurança.
* **Service:** serviço ao qual a associação se aplica.

Nesse ambiente:

* `__default__` utiliza `unconfined_u`.
* `root` está associado a `unconfined_u`.
* `sddm` está associado ao usuário SELinux `xdm`.

---

## 7. Consulta das variáveis booleanas

Foi utilizada a seguinte consulta:

```bash id="e3w5k7"
semanage boolean -l
```

A saída apresenta uma grande quantidade de variáveis booleanas do SELinux. Entre os exemplos observados:

```text id="c5q1md"
SELinux boolean                State  Default Description

aide_mmap_files                (off  ,  off)  Control if AIDE can mmap files. AIDE can be compiled with the option 'with-mmap' in which case it will attempt to mmap files while running.
allow_cvs_read_shadow          (off  ,  off)  Determine whether cvs can read shadow password files.
allow_execheap                 (off  ,  off)  Allow unconfined executables to make their heap memory executable.  Doing this is a really bad idea. Probably indicates a badly coded executable, but could indicate an attack. This executable should be reported in bugzilla
allow_execmem                  (off  ,  off)  Allow unconfined executables to map a memory region as both executable and writable, this is dangerous and the executable should be reported in bugzilla")

…

xguest_use_bluetooth           (off  ,  off)  Determine whether xguest can use blue tooth devices.
xscreensaver_read_generic_user_content (on   ,   on)  Grant the xscreensaver domains read access to generic user content
xserver_allow_dri              (off  ,  off)  Allow DRI access
xserver_can_network            (off  ,  off)  Allows the X server to use TCP/IP networking functionality (insecure).
xserver_client_writes_xserver_tmpfs (off  ,  off)  Allows clients to write to the X server tmpfs files.
xserver_gnome_xdm              (off  ,  off)  Use gnome-shell in gdm mode in gdm mode as the X Display Manager (XDM)
xserver_object_manager         (off  ,  off)  Support X userspace object manager
xserver_xdm_can_network        (off  ,  off)  Allows the X display manager to use TCP/IP networking functionality (insecure).
zabbix_can_network             (off  ,  off)  Determine whether zabbix can connect to all TCP ports
```

As colunas principais são:

* **SELinux boolean:** nome da variável.
* **State:** estado atual.
* **Default:** estado padrão.
* **Description:** finalidade da variável.

Os booleanos permitem ajustar determinados comportamentos das políticas SELinux sem necessariamente modificar toda a política.

---

## 8. Consulta das portas definidas no SELinux

Por fim, foram listadas as definições de portas conhecidas pelo SELinux:

```bash id="k4r7vc"
semanage port -l
```

A saída apresenta o tipo SELinux, protocolo e número da porta:

```text id="2n8s5x"
SELinux Port Type              Proto    Port Number

afs3_callback_port_t           tcp      7001
afs3_callback_port_t           udp      7001
afs_bos_port_t                 udp      7007

...

zookeeper_client_port_t        tcp      2181
zookeeper_election_port_t      tcp      3888
zookeeper_leader_port_t        tcp      2888
zope_port_t                    tcp      8021
```

Essa associação permite que o SELinux saiba quais tipos de portas estão relacionados a determinados serviços e protocolos.

Os principais campos são:

* **SELinux Port Type:** tipo de segurança associado à porta.
* **Proto:** protocolo utilizado, como TCP ou UDP.
* **Port Number:** número da porta.

---

## 9. Desativação do SELinux

O roteiro apresenta uma etapa opcional para desabilitar o SELinux, destinada exclusivamente a uma VM local e **não ao ambiente Hacker do Bem**.

Por esse motivo, essa alteração não deve ser realizada nas VMs compartilhadas do laboratório.

O procedimento descrito pelo roteiro consiste em alterar:

```text id="0b7j8k"
SELINUX=permissive
```

para:

```text id="0r3q5m"
SELINUX=disabled
```

no arquivo:

```text id="z7x1vc"
/etc/selinux/config
```

e posteriormente reiniciar o sistema.

Após a desativação, o `sestatus` poderia apresentar:

```text id="8p2m4d"
SELinux status:                 disabled
```

Essa etapa serve para demonstrar como a configuração persistente do SELinux pode ser alterada, mas não faz parte da execução recomendada no ambiente remoto do curso.

---

## Conceitos praticados

### SELinux

**Security-Enhanced Linux** é um mecanismo de segurança que implementa **controle de acesso obrigatório (MAC)**, adicionando políticas e contextos de segurança além das permissões tradicionais de usuários e grupos do Linux.

### MAC

**Mandatory Access Control** é um modelo no qual as regras de acesso são determinadas por políticas de segurança, independentemente das permissões tradicionais do sistema de arquivos.

### Permissive

Modo em que o SELinux registra violações das políticas, mas não bloqueia os acessos com base nessas violações.

### Enforcing

Modo em que as políticas SELinux são efetivamente aplicadas e acessos não autorizados podem ser bloqueados.

### `sestatus`

Comando utilizado para consultar o estado atual do SELinux, sua política carregada e seu modo de operação.

### `semanage`

Ferramenta utilizada para administrar partes da configuração de políticas SELinux, incluindo usuários, logins, booleanos e portas.

### Booleanos SELinux

Variáveis que permitem controlar determinados comportamentos das políticas de segurança de maneira dinâmica.

### Contextos e tipos

O SELinux utiliza informações adicionais de segurança para determinar como usuários, processos, arquivos e outros recursos podem interagir.

---

## Resultado

A atividade permitiu explorar o funcionamento do SELinux no Kali Linux e compreender como o mecanismo complementa o modelo tradicional de permissões do Linux.

Foram realizadas consultas e verificações relacionadas a:

* ativação do SELinux;
* estado e modo de operação;
* política carregada;
* usuários SELinux;
* associações entre logins e usuários SELinux;
* variáveis booleanas;
* tipos de portas;
* configuração persistente do serviço.

A atividade também demonstrou a diferença prática entre os modos **permissive** e **enforcing** e mostrou como o `semanage` pode ser utilizado para consultar diferentes componentes da política SELinux.

---

## Evidência

[**Evidências — Módulo 4 / Aulas 1 e 2**](../evidencias.pdf)

**Print registrado:** etapa 5 da atividade, conforme solicitado pelo roteiro, mostrando a consulta do status do SELinux com `sestatus`.
