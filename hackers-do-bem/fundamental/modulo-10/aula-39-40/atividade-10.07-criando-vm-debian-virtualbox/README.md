# Atividade 10.7 — Criando uma VM em um Hypervisor Tipo 2 no Kali Linux

## Objetivo

Criar uma máquina virtual utilizando o **Oracle VM VirtualBox** no Kali Linux, configurando uma instalação baseada na imagem **Debian 12.5.0 AMD64 Netinst**.

A atividade demonstra o processo de criação de uma VM em um **Hypervisor Tipo 2**, incluindo a seleção da imagem ISO, configuração de usuário, memória e armazenamento.

---

## Ambiente

* **Sistema hospedeiro:** Kali GNU/Linux
* **Hypervisor:** Oracle VM VirtualBox
* **Sistema convidado:** Debian Netinst
* **Imagem:** `debian-12.5.0-amd64-netinst.iso`
* **Memória configurada:** 512 MB
* **Disco configurado:** 10 GB
* **Nome da VM:** `DebianNetinst`

---

## 1. Iniciando a criação da máquina virtual

Com o VirtualBox aberto da atividade anterior, foi fechada a janela contendo a mensagem:

```text
Não foi possível enumerar os dispositivos USB...
```

Em seguida, na barra superior do VirtualBox, foi acessado:

```text
Máquina → Novo
```

Isso abriu o assistente de criação de uma nova máquina virtual.

---

## 2. Definindo o nome da VM

No campo de identificação da máquina virtual, foi informado:

```text id="8u1f4e"
DebianNetinst
```

Esse será o nome utilizado pelo VirtualBox para identificar a máquina virtual.

---

## 3. Selecionando a imagem ISO

No campo **Imagem ISO**, foi selecionada a opção:

```text
Outro
```

Na janela de seleção de arquivos, foram acessadas as pastas:

```text id="1e6e4m"
Outros locais
→ Computador
→ curso
```

Foi localizada a imagem:

```text id="v1p8ma"
debian-12.5.0-amd64-netinst.iso
```

A imagem foi selecionada com dois cliques.

---

## 4. Avançando no assistente

Após selecionar a imagem ISO do Debian, foi clicado:

```text
Próximo(N)
```

O assistente avançou para as configurações de usuário.

---

## 5. Configurando o usuário

No campo **Nome do Usuário**, o nome padrão foi alterado para:

```text id="qym8ml"
DebianNetinst
```

Também foi verificada a senha apresentada pelo laboratório:

```text
changeme
```

Após a configuração, foi clicado:

```text
Próximo(N)
```

As credenciais do laboratório não são reproduzidas além do necessário para documentar a configuração.

---

## 6. Configurando a memória

Na etapa de configuração de hardware, foi definida a **Memória Base** para:

```text id="bdq8m4"
512 MB
```

Em seguida, foi clicado:

```text
Próximo(N)
```

---

## 7. Configurando o armazenamento

Na configuração do disco virtual, o tamanho foi alterado para:

```text id="q0k7ap"
10 GB
```

Em seguida, foi clicado:

```text
Próximo(N)
```

---

## 8. Finalizando a criação da VM

O VirtualBox apresentou o sumário com as configurações selecionadas.

Após verificar as informações, foi clicado:

```text id="l4r9br"
Finalizar
```

A máquina virtual foi então criada no VirtualBox.

---

## Evidência — Passo 9

**Frase obrigatória antes do print:**

> **Print da atividade 10.7:** máquina virtual `DebianNetinst` criada e apresentada na coluna esquerda do Oracle VM VirtualBox.

[**Evidências — Módulo 10 / Aulas 39 e 40**](../evidencias.pdf)

---

## 9. Verificando a máquina virtual criada

Após a finalização do assistente, a VM:

```text id="xv8q34"
DebianNetinst
```

passou a aparecer na coluna esquerda do VirtualBox.

A máquina foi criada com as configurações definidas durante o assistente, incluindo a imagem ISO do Debian Netinst, **512 MB de memória** e **10 GB de armazenamento**.

O laboratório também informa que o ambiente da VM da AWS **não possui driver de virtualização**. Portanto, não é necessário iniciar a máquina virtual `DebianNetinst` nesse ambiente.

Caso a VM seja executada nesse ambiente, poderá ocorrer o erro:

```text
Kernel driver not installed
```

A criação da máquina virtual, entretanto, foi concluída normalmente.

---

## 10. Encerramento

A máquina virtual `DebianNetinst` foi criada e permaneceu disponível no VirtualBox para uma eventual instalação do Debian.

Para esta atividade, não foi necessário iniciar a máquina virtual nem realizar a instalação do sistema operacional.

Após a conclusão, as janelas foram fechadas, a conexão RDP foi encerrada e a sessão da VM da AWS foi interrompida, conforme orientação do laboratório.

---

## Conceitos

* **Máquina virtual:** ambiente computacional isolado executado sobre um hypervisor.
* **ISO Netinst:** imagem mínima de instalação do Debian, utilizada para iniciar o processo de instalação e obter os componentes necessários.
* **Hypervisor Tipo 2:** software de virtualização executado sobre um sistema operacional hospedeiro.
* **VirtualBox:** hypervisor utilizado para criar e gerenciar a máquina virtual.

## Fluxo da atividade

```text id="b5e9zn"
Abrir VirtualBox
      ↓
Máquina → Novo
      ↓
Definir DebianNetinst
      ↓
Selecionar ISO
      ↓
Configurar usuário
      ↓
512 MB RAM
      ↓
10 GB de disco
      ↓
Finalizar
      ↓
VM criada
```

## Resultado

A máquina virtual **DebianNetinst** foi criada com a imagem Debian Netinst, **512 MB de memória** e **10 GB de armazenamento**, ficando disponível na interface do VirtualBox.
