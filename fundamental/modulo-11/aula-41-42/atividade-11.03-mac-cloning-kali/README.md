# Atividade 11.3 — MAC Cloning no Kali Linux

## Objetivo

Explorar a alteração do endereço MAC de uma interface de rede no Kali Linux, realizando um **MAC cloning** temporário na interface `docker0` e restaurando posteriormente o endereço MAC original.

A atividade demonstra como o endereço físico de uma interface pode ser alterado em software e como verificar a alteração utilizando ferramentas de rede do Linux.

---

## Ambiente

* **Sistema:** Kali GNU/Linux
* **Interface analisada:** `docker0`
* **Ferramentas:** `ip link` e `ifconfig`
* **MAC original da `docker0`:** `02:42:4c:36:59:3d`
* **MAC utilizado no teste:** `08:00:27:8b:c0:05`

---

## 1. Acessando o Kali Linux

A máquina Kali Linux foi acessada e o Terminal foi aberto.

Foi obtido acesso administrativo com:

```bash id="f7k3qm"
sudo -i
```

---

## 2. Visualizando as interfaces de rede

As interfaces disponíveis foram verificadas com:

```bash id="m2v8xc"
ip link show
```

A saída apresentada foi:

```text id="ysiu2p"
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc mq state UP mode DEFAULT group default qlen 1000
    link/ether 12:4d:70:f0:ab:8b brd ff:ff:ff:ff:ff:ff
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN mode DEFAULT group default qlen 1000
    link/ether 02:42:4c:36:59:3d brd ff:ff:ff:ff:ff:ff
```

A interface `docker0` estava configurada com o endereço MAC:

```text id="c5n9rv"
02:42:4c:36:59:3d
```

Esse endereço foi registrado para que pudesse ser restaurado ao final da atividade.

### Interfaces observadas

* `lo`: interface de loopback;
* `eth0`: interface de rede principal;
* `docker0`: bridge virtual utilizada pelo Docker.

---

## 3. Visualizando as interfaces com ifconfig

Também foi utilizado:

```bash id="p8x4kt"
ifconfig
```

A saída permitiu confirmar as informações das interfaces de rede, incluindo o endereço MAC da `docker0`:

```text id="w6r2jd"
docker0: ...
          ether 02:42:4c:36:59:3d
```

O endereço MAC original da interface `docker0` foi mantido como referência para a etapa de restauração.

> **Importante:** o MAC original pode variar de acordo com a máquina ou ambiente. Neste laboratório, o endereço original observado foi `02:42:4c:36:59:3d`.

---

## 4. Desativando a interface docker0

Antes de alterar o endereço MAC, a interface foi desativada:

```bash id="q9m5bx"
ip link set docker0 down
```

A desativação evita realizar a alteração enquanto a interface está operacional.

---

## 5. Alterando o endereço MAC

Foi definido um novo endereço MAC para a interface `docker0`:

```bash id="r3k7nv"
ip link set dev docker0 address 08:00:27:8b:c0:05
```

Nesse momento, o endereço MAC da interface foi alterado temporariamente para:

```text id="x8d2pf"
08:00:27:8b:c0:05
```

Essa técnica é conhecida como **MAC cloning** ou **MAC spoofing**, pois permite fazer uma interface utilizar um endereço MAC diferente daquele originalmente configurado.

---

## 6. Reativando a interface

Após a alteração, a interface foi ativada novamente:

```bash id="t4c6mz"
ip link set docker0 up
```

---

## 7. Verificando o novo endereço MAC

A alteração foi confirmada com:

```bash id="n7v2ks"
ip link show
```

A interface `docker0` passou a apresentar:

```text id="3k729l"
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN mode DEFAULT group default
    link/ether 08:00:27:8b:c0:05 brd ff:ff:ff:ff:ff:ff
```

O endereço MAC exibido passou de:

```text
02:42:4c:36:59:3d
```

para:

```text
08:00:27:8b:c0:05
```

Isso confirma que a alteração foi aplicada à interface.

---

## 8. Restaurando o endereço MAC original

Após concluir o teste, o endereço MAC original foi restaurado.

Primeiro, a interface foi desativada:

```bash id="u5p8wc"
ip link set docker0 down
```

Em seguida, foi configurado novamente o endereço MAC original observado no início da atividade:

```bash id="k3r9fm"
ip link set dev docker0 address 02:42:4c:36:59:3d
```

Por fim, a interface foi reativada:

```bash id="z6n4qt"
ip link set docker0 up
```

### Evidência — Passo 8

**Frase obrigatória antes do print:**

> **Print da atividade 11.3:** restauração do endereço MAC original da interface `docker0`, após o teste de MAC cloning, utilizando novamente o endereço `02:42:4c:36:59:3d`.

[**Evidências — Módulo 11 / Aulas 41 e 42**](../evidencias.pdf)

> **Observação:** caso o endereço MAC original seja diferente em outra máquina, deve ser utilizado o valor registrado antes da alteração, e não necessariamente `02:42:4c:36:59:3d`.

---

## 9. Verificando a restauração

Após a restauração, a configuração da interface foi verificada novamente:

```bash id="b8m5qx"
ip link show
```

A interface `docker0` deve voltar a apresentar o MAC original registrado no início da atividade:

```text
link/ether 02:42:4c:36:59:3d
```

---

## 10. Encerrando a atividade

Após confirmar a restauração do endereço MAC, o Terminal foi fechado.

---

## Conceitos

* **Endereço MAC:** identificador utilizado na camada de enlace para identificar uma interface de rede.
* **MAC cloning:** alteração do endereço MAC apresentado por uma interface para outro endereço.
* **`ip link`:** ferramenta do Linux para visualizar e modificar interfaces de rede.
* **`docker0`:** bridge virtual criada pelo Docker para comunicação de containers.
* **MAC spoofing:** técnica de alteração do endereço MAC utilizado por uma interface.

## Fluxo da atividade

```text id="v9c2la"
Verificar MAC original
        ↓
Desativar docker0
        ↓
Alterar endereço MAC
        ↓
Reativar interface
        ↓
Verificar alteração
        ↓
Restaurar MAC original
        ↓
Verificar restauração
```

## Resultado

O endereço MAC da interface `docker0` foi alterado temporariamente para `08:00:27:8b:c0:05` e a alteração foi confirmada com `ip link show`. Ao final, o endereço MAC original `02:42:4c:36:59:3d` foi restaurado.
