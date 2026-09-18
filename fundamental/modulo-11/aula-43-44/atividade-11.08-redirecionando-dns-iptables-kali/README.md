# Atividade 11.8 — Redirecionando Requisições DNS usando iptables no Kali Linux

## Objetivo

Utilizar o **iptables** no Kali Linux para redirecionar requisições DNS utilizando uma regra de **DNAT**, observando o efeito da alteração sobre a resolução de nomes e verificando a configuração da tabela `nat`.

---

## Ambiente

* **Sistema:** Kali GNU/Linux
* **Acesso:** RDP
* **Ferramenta:** `iptables`
* **Interface:** `eth0`
* **Porta DNS utilizada no laboratório:** `53/UDP`
* **Destino configurado:** `127.0.0.1:53`

---

## 1. Acessando o Kali Linux

O Kali Linux foi inicializado e acessado através de RDP.

Após abrir o Terminal, foi obtido acesso administrativo com:

```bash id="r4k8pz"
sudo -i
```

---

## 2. Testando a resolução DNS normalmente

O Mozilla Firefox foi aberto em uma janela de navegação anônima utilizando:

```text id="x7m3qc"
Ctrl + Shift + P
```

Em seguida, foi acessado:

```text id="p9v5kd"
https://www.facebook.com/
```

O site foi carregado normalmente.

Esse primeiro acesso serviu como referência para verificar o comportamento do sistema antes da aplicação da regra de redirecionamento DNS.

Após o teste, o navegador foi fechado.

---

## 3. Criando a regra de redirecionamento DNS

No Terminal, foi executado:

```bash id="h3w6nb"
iptables -t nat -A OUTPUT -p udp --dport 53 -j DNAT --to-destination 127.0.0.1:53
```

A regra foi adicionada à tabela `nat`, na chain `OUTPUT`.

### Parâmetros utilizados

#### `-t nat`

Seleciona a tabela **NAT** (*Network Address Translation*).

Essa tabela é utilizada para realizar alterações relacionadas aos endereços e portas dos pacotes.

#### `-A OUTPUT`

Adiciona a regra à chain `OUTPUT`.

A chain `OUTPUT` processa pacotes gerados pelo próprio sistema.

#### `-p udp`

Define que a regra será aplicada ao protocolo **UDP**.

O DNS tradicional utiliza frequentemente UDP para consultas.

#### `--dport 53`

Seleciona o tráfego destinado à porta:

```text id="v8c2qm"
53
```

A porta 53 é a porta tradicionalmente utilizada pelo serviço DNS.

#### `-j DNAT`

Define a ação **Destination NAT**, utilizada para alterar o destino do pacote.

#### `--to-destination 127.0.0.1:53`

Define o novo destino:

```text id="s5n9rx"
127.0.0.1:53
```

Dessa forma, as requisições UDP destinadas à porta 53 são redirecionadas para a própria máquina, na porta 53.

O fluxo configurado pode ser representado como:

```text id="m2q7vf"
Aplicação
   ↓
Consulta DNS UDP/53
   ↓
iptables / tabela nat
   ↓
OUTPUT
   ↓
DNAT
   ↓
127.0.0.1:53
```

---

## 4. Testando o efeito do redirecionamento

Após adicionar a regra, o Mozilla Firefox foi aberto novamente em modo anônimo.

Foi acessado:

```text id="c6w4kp"
https://www.facebook.com/
```

Após o redirecionamento, o navegador não conseguiu realizar normalmente a resolução do endereço.

Foi apresentada a mensagem:

```text id="b8x3qm"
Hmm. We’re having trouble finding that site.
```

Esse comportamento demonstra o efeito da alteração realizada no caminho das consultas DNS utilizadas pelo navegador no ambiente do laboratório.

> **Observação:** a regra criada atua especificamente sobre **UDP na porta 53**. Portanto, ela não representa um bloqueio universal de todos os mecanismos modernos de resolução DNS, que também podem utilizar outras formas de transporte, como DNS sobre HTTPS (DoH) ou DNS sobre TLS (DoT).

---

## 5. Verificando a tabela NAT

Para visualizar as regras existentes na tabela `nat`, foi executado:

```bash id="q9m4xt"
iptables -t nat -L
```

A saída apresentada foi:

```text id="u5k8rc"
┌──(root㉿kali)-[~]
└─# iptables -t nat -L
Chain PREROUTING (policy ACCEPT)
target     prot opt source               destination
DOCKER     all  --  anywhere             anywhere             ADDRTYPE match dst-type LOCAL

Chain INPUT (policy ACCEPT)
target     prot opt source               destination

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination
DOCKER     all  --  anywhere             !loopback/8           ADDRTYPE match dst-type LOCAL
DNAT       udp  --  anywhere             anywhere             udp dpt:domain to:127.0.0.1:53

Chain POSTROUTING (policy ACCEPT)
target     prot opt source               destination
MASQUERADE  all  --  172.17.0.0/16        anywhere

Chain DOCKER (2 references)
target     prot opt source               destination
RETURN     all  --  anywhere             anywhere
```

A regra adicionada pode ser identificada na chain `OUTPUT`:

```text id="n7p3wb"
DNAT       udp  --  anywhere  anywhere  udp dpt:domain to:127.0.0.1:53
```

Ela demonstra que o tráfego UDP destinado à porta DNS (`53`) está sendo redirecionado para `127.0.0.1:53`.

### Evidência — Passo 7

**Frase obrigatória antes do print:**

> **Print da atividade 11.8:** saída de `iptables -t nat -L` exibindo a regra DNAT da chain `OUTPUT`, responsável por redirecionar consultas UDP na porta 53 para `127.0.0.1:53`.

[**Evidências — Módulo 11 / Aulas 43 e 44**](../evidencias.pdf)

---

## 6. Removendo a regra DNAT

Após verificar o comportamento do redirecionamento, a regra foi removida com:

```bash id="t4v8mq"
iptables -t nat -D OUTPUT -p udp --dport 53 -j DNAT --to-destination 127.0.0.1:53
```

O parâmetro:

```text id="w6c2pn"
-D
```

remove uma regra existente.

Os demais parâmetros correspondem à regra criada anteriormente, permitindo que o `iptables` identifique exatamente qual configuração deve ser removida.

---

## 7. Verificando a remoção

Após excluir a regra, foi executado novamente:

```bash id="y3k7fz"
iptables -t nat -L
```

A saída passou a não apresentar a regra `DNAT` criada anteriormente:

```text id="e8m4qc"
┌──(root㉿kali)-[~]
└─# iptables -t nat -L
Chain PREROUTING (policy ACCEPT)
target     prot opt source               destination
DOCKER     all  --  anywhere             anywhere             ADDRTYPE match dst-type LOCAL

Chain INPUT (policy ACCEPT)
target     prot opt source               destination

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination
DOCKER     all  --  anywhere             !ip-127-0-0-0.ec2.internal/8  ADDRTYPE match dst-type LOCAL

Chain POSTROUTING (policy ACCEPT)
target     prot opt source               destination
MASQUERADE  all  --  ip-172-17-0-0.ec2.internal/16  anywhere

Chain DOCKER (2 references)
target     prot opt source               destination
RETURN     all  --  anywhere             anywhere
```

A ausência da regra `DNAT` confirma que o redirecionamento criado durante o laboratório foi removido.

---

## 8. Confirmando a resolução DNS novamente

Após remover a regra, o Firefox foi atualizado e o endereço:

```text id="p6r2vk"
https://www.facebook.com/
```

foi acessado novamente.

O site voltou a carregar normalmente, demonstrando que a regra responsável pelo redirecionamento das consultas DNS havia sido removida.

Após a confirmação, o navegador foi fechado.

---

## Conceitos

* **DNS:** sistema responsável pela resolução de nomes de domínio em endereços IP.
* **iptables:** ferramenta de configuração das regras do Netfilter no Linux.
* **NAT:** mecanismo utilizado para modificar informações de endereçamento dos pacotes.
* **DNAT:** altera o destino de um pacote.
* **OUTPUT:** chain responsável pelo tráfego gerado pelo próprio sistema.
* **UDP/53:** combinação tradicional utilizada por consultas DNS.
* **Loopback:** interface utilizada para comunicação com o próprio sistema, representada por `127.0.0.1`.

## Fluxo da atividade

```text id="z4m8xc"
Facebook funciona normalmente
          ↓
Criar regra DNAT
          ↓
UDP/53 → 127.0.0.1:53
          ↓
Consultar Facebook novamente
          ↓
Falha na resolução do domínio
          ↓
iptables -t nat -L
          ↓
Remover regra DNAT
          ↓
Facebook volta a funcionar
```

## Resultado

Foi criada uma regra DNAT no `iptables` para redirecionar o tráfego **UDP destinado à porta 53** para `127.0.0.1:53`. Após a aplicação da regra, o acesso ao Facebook apresentou falha de resolução no ambiente do laboratório. A regra foi posteriormente removida e o acesso voltou ao funcionamento normal.
