# Atividade 11.7 — Bloqueando Sites usando iptables no Kali Linux

## Objetivo

Utilizar o **iptables** no Kali Linux para criar uma regra de firewall capaz de bloquear o acesso ao domínio `globo.com.br`, verificar a regra criada e posteriormente removê-la para restaurar o acesso ao site.

---

## Ambiente

* **Sistema:** Kali GNU/Linux
* **Acesso:** RDP
* **Interface:** `eth0`
* **Ferramenta:** `iptables`
* **Site utilizado no teste:** `globo.com.br`

---

## 1. Acessando o Kali Linux

O Kali Linux foi inicializado e acessado via RDP.

Após abrir o Terminal, foi obtido acesso administrativo com:

```bash id="a8f3km"
sudo -i
```

A autenticação foi realizada com a senha do usuário.

---

## 2. Abrindo o navegador em modo anônimo

O Mozilla Firefox foi aberto através de:

```text id="k5w2pn"
Aplicativos → Navegador Web
```

Em seguida, foi utilizado:

```text id="r7m4xc"
Ctrl + Shift + P
```

para abrir uma janela de navegação anônima.

---

## 3. Testando o acesso ao site

Na janela anônima do Firefox, foi acessado:

```text id="v3q9mb"
www.globo.com.br
```

O site foi carregado normalmente antes da aplicação da regra de bloqueio.

Esse teste estabelece o funcionamento normal da conexão antes da alteração do firewall.

---

## 4. Fechando o navegador e criando a regra de bloqueio

Após verificar o acesso normal ao site, as janelas do Mozilla Firefox foram fechadas.

No Terminal, foi criada uma regra no `iptables`:

```bash id="n6c4yt"
iptables -A INPUT -s globo.com.br -j DROP
```

A regra adicionada atua sobre a chain `INPUT`.

### Parâmetros utilizados

#### `iptables`

Ferramenta utilizada para configurar regras de filtragem do **Netfilter**, o framework de firewall do kernel Linux.

#### `-A INPUT`

O parâmetro `-A` significa **Append** e adiciona uma nova regra à chain `INPUT`.

A chain `INPUT` processa pacotes destinados ao próprio sistema.

#### `-s globo.com.br`

O parâmetro `-s` define a origem (*source*) dos pacotes aos quais a regra será aplicada.

Nesse laboratório, foi utilizado o nome de host:

```text id="w4x8fz"
globo.com.br
```

O `iptables` resolve o nome para o endereço correspondente no momento da configuração da regra.

#### `-j DROP`

Define a ação da regra.

`DROP` faz com que os pacotes correspondentes sejam descartados, sem serem aceitos pelo sistema.

A regra completa pode ser interpretada como:

```text id="u2k7dq"
Pacotes de origem globo.com.br
              ↓
          Chain INPUT
              ↓
             DROP
              ↓
       Pacote descartado
```

---

## 5. Visualizando as regras do iptables

Para verificar a configuração atual do firewall, foi executado:

```bash id="c9p4vr"
iptables -L
```

A saída apresentada foi:

```text id="f2m7kx"
┌──(root㉿kali)-[~]
└─# iptables -L
Chain INPUT (policy ACCEPT)
target     prot opt source               destination
DROP       all  --  186-192-83-5.prt.globo.com  anywhere

Chain FORWARD (policy DROP)
target     prot opt source               destination
DOCKER-USER  all  --  anywhere             anywhere
DOCKER-ISOLATION-STAGE-1  all  --  anywhere             anywhere
ACCEPT     all  --  anywhere             anywhere             ctstate RELATED,ESTABLISHED
DOCKER     all  --  anywhere             anywhere
ACCEPT     all  --  anywhere             anywhere
ACCEPT     all  --  anywhere             anywhere

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination

Chain DOCKER (1 references)
target     prot opt source               destination

Chain DOCKER-ISOLATION-STAGE-1 (1 references)
target     prot opt source               destination
DOCKER-ISOLATION-STAGE-2  all  --  anywhere             anywhere
RETURN     all  --  anywhere             anywhere

Chain DOCKER-ISOLATION-STAGE-2 (1 references)
target     prot opt source               destination
DROP       all  --  anywhere             anywhere
RETURN     all  --  anywhere             anywhere

Chain DOCKER-USER (1 references)
target     prot opt source               destination
RETURN     all  --  anywhere             anywhere
```

Na chain `INPUT`, a regra criada aparece como:

```text id="q5v9nx"
DROP       all  --  186-192-83-5.prt.globo.com  anywhere
```

Isso demonstra que foi adicionada uma regra para descartar os pacotes correspondentes à origem resolvida para o domínio utilizado no laboratório.

### Evidência — Passo 6

**Frase obrigatória antes do print:**

> **Print da atividade 11.7:** listagem das regras do `iptables`, mostrando a regra `DROP` adicionada à chain `INPUT` para bloquear o tráfego relacionado ao domínio `globo.com.br`.

[**Evidências — Módulo 11 / Aulas 43 e 44**](../evidencias.pdf)

---

## 6. Testando novamente o acesso ao site

Após a criação da regra, o Mozilla Firefox foi aberto novamente em modo anônimo.

Foi acessado:

```text id="d7w3mq"
www.globo.com.br
```

Diferentemente do primeiro teste, o site não carregou normalmente.

Isso ocorre porque a regra adicionada ao `iptables` descarta os pacotes correspondentes à origem especificada.

O comportamento observado demonstra o efeito da regra de filtragem criada durante a atividade.

---

## 7. Removendo a regra de bloqueio

Após verificar o bloqueio, o Terminal foi aberto novamente e a regra foi removida com:

```bash id="k2p8wf"
iptables -D INPUT -s globo.com.br -j DROP
```

O parâmetro:

```text id="n5x7cs"
-D
```

significa **Delete**, ou seja, remove uma regra existente da chain.

Os demais parâmetros correspondem à regra que havia sido adicionada anteriormente:

```text id="r3m6vk"
INPUT
-s globo.com.br
-j DROP
```

Assim, o comando remove especificamente a regra criada no início da atividade.

---

## 8. Verificando novamente as regras

Após remover o bloqueio, foi executado:

```bash id="p4c8yt"
iptables -L
```

A chain `INPUT` voltou a não apresentar a regra `DROP` criada para o domínio:

```text id="j8m2qx"
Chain INPUT (policy ACCEPT)
target     prot opt source               destination
```

As demais chains relacionadas ao ambiente Docker continuaram presentes.

---

## 9. Confirmando o acesso novamente

Com a regra removida, o Mozilla Firefox foi aberto novamente e o endereço:

```text id="s6q3vk"
www.globo.com.br
```

foi acessado.

O site voltou a carregar normalmente, demonstrando que a regra de bloqueio havia sido removida.

Após a verificação, o navegador foi fechado.

---

## 10. Reiniciando o Kali Linux

Para finalizar a atividade, o sistema foi reiniciado com:

```bash id="w9f4mb"
reboot
```

---

## Conceitos

* **iptables:** ferramenta de configuração do firewall Netfilter no Linux.
* **Netfilter:** framework de filtragem e processamento de pacotes do kernel Linux.
* **INPUT:** chain responsável por processar tráfego destinado ao próprio sistema.
* **OUTPUT:** chain responsável pelo tráfego gerado pelo próprio sistema.
* **DROP:** descarta pacotes que correspondem à regra.
* **`-A`:** adiciona uma regra.
* **`-D`:** remove uma regra.
* **`-s`:** especifica a origem dos pacotes.

## Fluxo da atividade

```text id="c7m5zn"
Acessar globo.com.br
        ↓
Site funciona normalmente
        ↓
Criar regra DROP
        ↓
iptables -L
        ↓
Site deixa de carregar
        ↓
Remover regra
        ↓
iptables -L
        ↓
Site volta a carregar
```

## Resultado

Foi criada uma regra no `iptables` para descartar tráfego associado ao `globo.com.br`. Após a aplicação da regra, o acesso ao site foi bloqueado. Em seguida, a regra foi removida e o acesso ao site voltou ao funcionamento normal.
