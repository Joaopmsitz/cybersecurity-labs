# Atividade 7.4 — Rsync Automático com Cron

## Objetivo

Automatizar a sincronização entre dois diretórios utilizando `rsync` e `cron`. O objetivo é configurar um script que execute a cópia automaticamente a cada minuto, permitindo que arquivos adicionados à `PastaA` sejam sincronizados para a `PastaB`.

---

## 1. Verificação dos diretórios

Primeiro, foi acessado o diretório utilizado no laboratório:

```bash
sudo -i
cd /home/aluno/Documentos
ls
```

Saída:

```text
PastaA  PastaB
```

Em seguida, foi verificado o conteúdo da `PastaA`:

```bash
cd PastaA
ls
```

Saída:

```text
Teste.txt
```

A `PastaB` estava inicialmente vazia:

```bash
cd /home/aluno/Documentos/PastaB
ls
```

---

## 2. Criação do script de sincronização

O script foi criado no diretório `/home/aluno/Documentos/`:

```bash
cd /home/aluno/Documentos
nano sync_script.sh
```

Conteúdo do arquivo:

```bash
#!/bin/bash

rsync -avz /home/aluno/Documentos/PastaA/ /home/aluno/Documentos/PastaB/
```

O script utiliza o `rsync` para sincronizar todo o conteúdo da `PastaA` com a `PastaB`.

### Parâmetros utilizados

* `-a` — modo *archive*, preservando atributos dos arquivos e realizando a cópia de forma recursiva.
* `-v` — exibe informações sobre os arquivos processados.
* `-z` — utiliza compressão durante a transferência.
* `/home/aluno/Documentos/PastaA/` — origem.
* `/home/aluno/Documentos/PastaB/` — destino.

---

## 3. Tornando o script executável

Após salvar o script, foi concedida permissão de execução:

```bash
chmod +x sync_script.sh
```

---

## 4. Configuração do Cron

Foi aberto o agendador de tarefas do usuário `root`:

```bash
crontab -e
```

Como não havia uma configuração anterior de `crontab`, o sistema apresentou:

```text
no crontab for root - using an empty one

Select an editor.  To change later, run 'select-editor'.
  1. /bin/nano        <---- easiest
  2. /usr/bin/vim.basic
  3. /usr/bin/vim.tiny
Choose 1-3 [1]: 1
no crontab for root - using an empty one
crontab: installing new crontab
```

Foi adicionada a seguinte entrada:

```cron
* * * * * /home/aluno/Documentos/sync_script.sh
```

Essa expressão agenda a execução do script **a cada minuto**.

### Estrutura da expressão

```text
* * * * * comando
│ │ │ │ │
│ │ │ │ └── Dia da semana
│ │ │ └──── Mês
│ │ └────── Dia do mês
│ └──────── Hora
└────────── Minuto
```

Como todos os campos possuem `*`, o script é executado uma vez por minuto, independentemente da hora, dia ou mês.

---

## 5. Verificação da sincronização automática

Após aguardar a execução programada do `cron`, foi acessado o diretório de destino em um segundo terminal:

```bash
sudo -i
cd /home/aluno/Documentos/PastaB
ls
```

O arquivo presente na `PastaA` foi sincronizado automaticamente para a `PastaB`.

---

## 6. Teste com um segundo arquivo

Para verificar novamente o funcionamento da automação, foi criado um segundo arquivo na `PastaA`:

```bash
cd /home/aluno/Documentos/PastaA
nano Teste2.txt
```

Conteúdo:

```text
Novo teste!
```

Após a próxima execução do `cron`, o arquivo foi disponibilizado na `PastaB`, demonstrando que a sincronização não dependia de uma execução manual do `rsync`.

A saída registrada no laboratório foi:

```text
┌──(root㉿kali)-[/home/aluno/Documentos/PastaB]
└─# ls
Teste1.txt  Teste2.txt
```

> A saída acima foi mantida conforme registrada durante a atividade.

---

## 7. Limpeza do ambiente

Após os testes, foi retornado ao diretório principal:

```bash
cd /home/aluno/Documentos/
ls
```

Saída:

```text
PastaA  PastaB  sync_script.sh
```

O conteúdo utilizado no laboratório foi removido:

```bash
rm -r *
```

O sistema solicitou confirmação:

```text
zsh: sure you want to delete all 3 files in /home/aluno/Documentos [yn]? y
```

Por fim:

```bash
ls
```

O diretório ficou vazio.

---

## 8. Reinicialização

Ao final da atividade, a máquina foi reinicializada:

```bash
reboot
```

---

## Evidência

[**Evidências — Módulo 7 / Aulas 1 e 2**](../evidencias.pdf)
