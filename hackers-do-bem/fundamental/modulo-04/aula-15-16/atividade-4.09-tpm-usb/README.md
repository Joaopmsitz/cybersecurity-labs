# Atividade 4.9 — TPM e USB

## Objetivo

Verificar a disponibilidade de um **TPM (Trusted Platform Module)** no Kali Linux e identificar dispositivos USB disponíveis no ambiente do laboratório.

A atividade também demonstra como o ambiente virtualizado pode apresentar limitações em relação ao hardware físico da máquina.

---

## Ambiente

* Kali Linux em máquina virtual
* Kernel Linux
* TPM
* USB
* `journalctl`
* `usbview`

---

## 1. Verificando o TPM

Primeiramente, foi obtido acesso administrativo:

```bash
sudo -i
```

Em seguida, foi consultado o log do kernel procurando por mensagens relacionadas ao TPM:

```bash
journalctl -k --grep=tpm
```

Saída observada:

```text id="youj7b"
fev 09 22:01:37 kali kernel: ima: No TPM chip found, activating TPM-bypass!
fev 09 22:01:37 kali systemd[1]: systemd 252.6-1 running in system mode (+PAM +AUDIT +SELINUX +APPARMOR +IMA +>
```

### Interpretação

A mensagem:

```text
No TPM chip found
```

indica que o sistema não encontrou um dispositivo TPM disponível para a máquina virtual.

Como consequência, o **IMA (Integrity Measurement Architecture)** ativou um mecanismo de bypass para funcionar sem a presença do TPM.

Isso é uma característica do ambiente utilizado no laboratório e não significa, por si só, que exista uma vulnerabilidade no sistema.

---

## 2. Retornando ao usuário normal

Após a verificação:

```bash
exit
```

---

## 3. Verificando dispositivos USB

Foi utilizado o `usbview`, ferramenta gráfica para visualizar informações sobre dispositivos USB:

```bash
usbview
```

No terminal foi apresentada a mensagem:

```text id="tgvmy8"
/sys/bus/usb/devices/ must be present, exiting...
```

Apesar dessa mensagem inicial, a interface gráfica do **USBView** foi aberta durante a atividade.

Como o Kali estava sendo executado em uma máquina virtual, os dispositivos USB físicos do computador não estavam necessariamente disponíveis para o sistema convidado.

---

## Conceitos

### TPM

O **Trusted Platform Module (TPM)** é um componente de segurança baseado em hardware utilizado para operações relacionadas a chaves criptográficas, integridade da inicialização e armazenamento protegido de informações sensíveis.

Em computadores físicos compatíveis, o TPM pode ser utilizado por recursos de segurança do sistema operacional.

### IMA

O **Integrity Measurement Architecture (IMA)** é um mecanismo do kernel Linux utilizado para medir e verificar a integridade de arquivos e componentes do sistema.

No laboratório, o log mostrou que o IMA identificou a ausência de um TPM e ativou o modo de bypass correspondente.

### USBView

O `usbview` permite visualizar dispositivos conectados ao barramento USB e informações relacionadas a eles.

Em máquinas virtuais, a disponibilidade desses dispositivos depende da configuração de passthrough/compartilhamento de hardware entre o sistema hospedeiro e a máquina virtual.

---

## Resultado

A consulta ao log do kernel confirmou que **não havia um chip TPM disponível para o Kali Linux no ambiente virtualizado**:

```text
ima: No TPM chip found, activating TPM-bypass!
```

Também foi executado o `usbview` para verificar o barramento USB. A atividade evidenciou uma limitação comum de ambientes virtualizados: o sistema convidado pode não possuir acesso direto ao hardware físico do computador.

---

## Evidências

[**Evidências — Módulo 4 / Aulas 3 e 4**](../evidencias.pdf)

**Evidência registrada:** passo 5 — execução do `usbview` e visualização da interface no ambiente do laboratório.
