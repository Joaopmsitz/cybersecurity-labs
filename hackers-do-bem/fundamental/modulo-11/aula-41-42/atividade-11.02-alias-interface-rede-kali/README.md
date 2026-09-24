# Atividade 11.2 — Alias de Interface de Rede no Kali Linux

## Objetivo

Configurar **aliases de endereço IP** na interface de rede `eth0` do Kali Linux, atribuindo os endereços `192.168.98.41` e `192.168.98.42` à mesma interface física e validando a comunicação por meio de ICMP e SSH.

---

## Ambiente

* **Sistema:** Kali GNU/Linux
* **Acesso:** RDP
* **Interface:** `eth0`
* **Endereço principal:** `192.168.98.40/24`
* **Aliases:** `192.168.98.41/24` e `192.168.98.42/24`

---

## 1. Acessando o Kali Linux

A máquina Kali Linux foi acessada por RDP e o Terminal foi aberto.

Foi obtido acesso administrativo com:

```bash id="p4m7qx"
sudo -i
```

---

## 2. Editando a configuração de rede

O arquivo de configuração das interfaces de rede foi aberto com:

```bash id="v8k2ns"
nano /etc/network/interfaces
```

Foram adicionadas as configurações dos dois aliases:

```text id="r6c3wf"
auto eth0:1
iface eth0:1 inet static
    address 192.168.98.41
    netmask 255.255.255.0

auto eth0:2
iface eth0:2 inet static
    address 192.168.98.42
    netmask 255.255.255.0
```

A configuração define duas interfaces lógicas associadas à interface `eth0`.

* `eth0:1` → `192.168.98.41/24`
* `eth0:2` → `192.168.98.42/24`

Após inserir as configurações, o arquivo foi salvo com:

```text
Ctrl + X
S
ENTER
```

---

## 3. Reiniciando o sistema

Para aplicar a configuração, o Kali Linux foi reiniciado:

```bash id="n1d5zr"
reboot
```

Foi aguardado o tempo necessário para que a máquina voltasse a ficar disponível.

---

## 4. Reconectando ao Kali Linux

Após a reinicialização, a conexão RDP foi realizada novamente.

O acesso administrativo foi recuperado:

```bash id="k7w3mh"
sudo -i
```

---

## 5. Verificando os endereços da interface

A configuração da interface `eth0` foi verificada com:

```bash id="t9f4bc"
ip addr show eth0
```

A saída apresentada foi:

```text id="yh38bq"
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc mq state UP group default qlen 1000
    link/ether 12:4d:70:f0:ab:8b brd ff:ff:ff:ff:ff:ff
    inet 192.168.98.40/24 brd 192.168.98.255 scope global dynamic eth0
       valid_lft 3447sec preferred_lft 3447sec
    inet 192.168.98.41/24 brd 192.168.98.255 scope global secondary eth0:1
       valid_lft forever preferred_lft forever
    inet 192.168.98.42/24 brd 192.168.98.255 scope global secondary eth0:2
       valid_lft forever preferred_lft forever
    inet6 fe80::104d:70ff:fef0:ab8b/64 scope link proto kernel_ll
       valid_lft forever preferred_lft forever
```

A saída confirma que os dois novos endereços foram associados à interface.

### Endereços configurados

| Interface | Endereço           |
| --------- | ------------------ |
| `eth0`    | `192.168.98.40/24` |
| `eth0:1`  | `192.168.98.41/24` |
| `eth0:2`  | `192.168.98.42/24` |

Os aliases aparecem como endereços `secondary` da interface `eth0`.

Também é possível observar:

* `BROADCAST,MULTICAST,UP,LOWER_UP`: características e estado operacional da interface;
* `mtu 9001`: tamanho máximo configurado para o quadro;
* `link/ether`: endereço MAC da interface;
* `scope global`: endereço IPv4 válido para comunicação na rede;
* `scope link`: endereço IPv6 utilizado no escopo do enlace.

---

## 6. Testando o primeiro alias

O endereço `192.168.98.41` foi testado com:

```bash id="q2v6kd"
ping 192.168.98.41
```

Resultado:

```text id="pfhng8"
PING 192.168.98.41 (192.168.98.41) 56(84) bytes of data.
64 bytes from 192.168.98.41: icmp_seq=1 ttl=64 time=0.045 ms
64 bytes from 192.168.98.41: icmp_seq=2 ttl=64 time=0.044 ms
^C
--- 192.168.98.41 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1024ms
rtt min/avg/max/mdev = 0.044/0.044/0.045/0.000 ms
```

Foram recebidas respostas nos dois pacotes enviados, com **0% de perda**.

---

## 7. Testando o segundo alias

O segundo endereço foi testado com:

```bash id="c8r5mx"
ping 192.168.98.42
```

Resultado:

```text id="8spd8z"
PING 192.168.98.42 (192.168.98.42) 56(84) bytes of data.
64 bytes from 192.168.98.42: icmp_seq=1 ttl=64 time=0.038 ms
64 bytes from 192.168.98.42: icmp_seq=2 ttl=64 time=0.044 ms
^C
--- 192.168.98.42 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1003ms
rtt min/avg/max/mdev = 0.038/0.041/0.044/0.003 ms
```

Novamente, os dois pacotes receberam resposta e houve **0% de perda**.

---

## 8. Testando SSH através do segundo alias

Foi realizada uma conexão SSH utilizando o endereço `192.168.98.42`:

```bash id="d3n7kp"
ssh aluno@192.168.98.42
```

Na primeira conexão, foi apresentada a confirmação da chave do host:

```text id="818ju3"
The authenticity of host '192.168.98.42 (192.168.98.42)' can't be established.
ED25519 key fingerprint is SHA256:hsrbT/3IfQ22bAUQPUE8T3dpJA/aBVyt3wcyb6zKgO0.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.98.42' (ED25519) to the list of known hosts.
aluno@192.168.98.42's password:
Linux kali 6.6.9-cloud-amd64 #1 SMP PREEMPT_DYNAMIC Kali 6.6.9-1kali1 (2024-01-08) x86_64

The programs included with the Kali GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Kali GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the
extent permitted by applicable law.
┏━(Message from Kali developers)
┃ This is a minimal installation of Kali Linux, you likely
┃ want to install supplementary tools. Learn how:
┃ ⇒ https://www.kali.org/docs/troubleshooting/common-minimum-setup/
┃ This is a cloud installation of Kali Linux. Learn more about
┃ the specificities of the various cloud images:
┃ ⇒ https://www.kali.org/docs/troubleshooting/common-cloud-setup/
┗━(Run: “touch ~/.hushlogin” to hide this message)
┌──(aluno㉿kali)-[~]
└─$ exit
sair
Connection to 192.168.98.42 closed.
```

A conexão foi estabelecida com sucesso utilizando o segundo endereço IP configurado como alias.

### Evidência — Passo 8

**Frase obrigatória antes do print:**

> **Print da atividade 11.2:** conexão SSH realizada com sucesso utilizando o endereço `192.168.98.42`, demonstrando que o alias configurado na interface `eth0` pode ser utilizado para acesso ao serviço SSH.

[**Evidências — Módulo 11 / Aulas 41 e 42**](../evidencias.pdf)

---

## 9. Removendo os aliases

Após a validação, o arquivo de configuração foi aberto novamente:

```bash id="f5j8rc"
nano /etc/network/interfaces
```

Foram removidas as configurações adicionadas anteriormente:

```text id="rsik8d"
auto eth0:1
iface eth0:1 inet static
    address 192.168.98.41
    netmask 255.255.255.0

auto eth0:2
iface eth0:2 inet static
    address 192.168.98.42
    netmask 255.255.255.0
```

O arquivo foi salvo com:

```text
Ctrl + X
S
ENTER
```

---

## 10. Reiniciando novamente o sistema

Para aplicar a remoção dos aliases:

```bash id="w2c9mv"
reboot
```

Após a reinicialização, a configuração retorna ao estado anterior, sem os dois endereços adicionais.

---

## Conceitos

* **Alias de interface:** permite associar múltiplos endereços IP a uma mesma interface de rede.
* **`eth0:1` e `eth0:2`:** identificadores utilizados no laboratório para representar os aliases da interface `eth0`.
* **IP secundário:** endereço adicional configurado na mesma interface física.
* **ICMP:** protocolo utilizado pelo `ping` para verificar conectividade.
* **SSH:** protocolo utilizado para acesso remoto seguro a outro sistema.
* **`ip addr`:** comando utilizado para visualizar endereços e configurações das interfaces.

## Fluxo da atividade

```text
Editar /etc/network/interfaces
          ↓
Adicionar 192.168.98.41
Adicionar 192.168.98.42
          ↓
Reiniciar Kali
          ↓
Verificar com ip addr
          ↓
Testar com ping
          ↓
Testar SSH
          ↓
Remover aliases
          ↓
Reiniciar
```

## Resultado

Foram configurados dois endereços IP secundários na interface `eth0`. Os endereços `192.168.98.41` e `192.168.98.42` responderam aos testes de ICMP, e o segundo alias também foi utilizado com sucesso para uma conexão SSH.
