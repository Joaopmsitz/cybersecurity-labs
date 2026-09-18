# Atividade 7.7 — Backup Diferencial Local com Duplicity

## Objetivo

Realizar um **backup diferencial local** utilizando o `Duplicity`, aproveitando o backup completo criado na atividade anterior.

Nesta atividade, o conteúdo do arquivo `teste.txt` será alterado e um novo arquivo será criado. Em seguida, o Duplicity será executado novamente sobre o mesmo destino para registrar somente as alterações desde o último backup completo.

---

## Ambiente

* **Sistema:** Kali Linux
* **Ferramenta:** Duplicity
* **Diretório de origem:** `/home/aluno/Documentos/Conteudo`
* **Destino dos backups:** `/home/aluno/Documentos/ArmazenaBackup`
* **Diretório de restauração:** `/home/aluno/Documentos/BackupRestaurado2`

> As credenciais utilizadas no ambiente de laboratório não são registradas neste README.

---

## 1. Verificação do ambiente

Primeiramente, foi acessado o diretório `Documentos` e verificado o conteúdo deixado pela atividade anterior:

```bash
sudo -i
cd /home/aluno/Documentos/
ls
```

Saída:

```text
ArmazenaBackup  BackupRestaurado  Conteudo
```

O diretório `ArmazenaBackup` contém os arquivos gerados pelo backup completo.

Foi realizada a verificação do diretório de armazenamento:

```bash
cd /home/aluno/Documentos/ArmazenaBackup
ls
```

Saída:

```text
duplicity-full.20240222T032821Z.manifest.gpg
duplicity-full.20240222T032821Z.vol1.difftar.gpg
duplicity-full-signatures.20240222T032821Z.sigtar.gpg
```

Também foi verificado o diretório utilizado na restauração anterior:

```bash
cd /home/aluno/Documentos/BackupRestaurado
ls
```

Saída:

```text
teste.txt
```

Por fim, foi acessado o diretório que contém os arquivos originais:

```bash
cd /home/aluno/Documentos/Conteudo/
ls
```

Saída:

```text
teste.txt
```

---

## 2. Alteração do arquivo existente

O arquivo `teste.txt` foi aberto para alteração:

```bash
nano teste.txt
```

Seu conteúdo foi modificado de:

```text
Teste
```

para:

```text
Teste Diferencial
```

Essa alteração será identificada pelo Duplicity durante a execução do novo backup.

---

## 3. Criação de um novo arquivo

Além da alteração do arquivo existente, foi criado um novo arquivo:

```bash
nano teste2.txt
```

Conteúdo:

```text
Teste2
```

Dessa forma, o diretório de origem passou a conter tanto um arquivo modificado quanto um novo arquivo.

---

## 4. Execução do backup diferencial

O mesmo destino utilizado no backup completo foi informado novamente ao Duplicity:

```bash
duplicity /home/aluno/Documentos/Conteudo file:///home/aluno/Documentos/ArmazenaBackup
```

Saída completa registrada no laboratório:

```text
Nenhuma ação válida encontrada. Irá implicar 'backup' porque uma fonte de caminho foi informada e o destino é um local URL.
Os metadados remotos e locais estão sincronizados; nenhuma sincronização é necessária.
Last full backup date: Tue Oct 14 13:49:00 2025
GnuPG passphrase for decryption: 
Redigite a senha para descriptografar para confirmar: 
--------------[ Estatísticas de backup ]--------------
StartTime 1760461046.11 (Tue Oct 14 13:57:26 2025)
EndTime 1760461046.11 (Tue Oct 14 13:57:26 2025)
ElapsedTime 0.01 (0.01 seconds)
SourceFiles 3
SourceFileSize 4121 (4.02 KB)
NewFiles 2
NewFileSize 4103 (4.01 KB)
DeletedFiles 0
ChangedFiles 1
ChangedFileSize 18 (18 bytes)
ChangedDeltaSize 0 (0 bytes)
DeltaEntries 3
RawDeltaSize 31 (31 bytes)
TotalDestinationSizeChange 283 (283 bytes)
Errors 0
------------------------------------------------------
```

### Interpretação da saída

O Duplicity identificou as alterações existentes desde o backup completo anterior.

Entre as informações apresentadas:

```text
SourceFiles 3
```

indica que o diretório de origem passou a conter três arquivos considerados pelo processo de backup.

O campo:

```text
ChangedFiles 1
ChangedFileSize 18 (18 bytes)
```

indica que um arquivo existente foi alterado. Nesse caso, trata-se do `teste.txt`, cujo conteúdo foi modificado para `Teste Diferencial`.

Também foram registrados novos arquivos:

```text
NewFiles 2
NewFileSize 4103 (4.01 KB)
```

O Duplicity utilizou o backup completo anterior como referência e registrou as alterações no destino `ArmazenaBackup`.

O processo foi concluído sem erros:

```text
Errors 0
```

---

## 5. Restauração do backup diferencial

Após a criação do novo backup, foi realizada uma restauração para um diretório diferente:

```bash
duplicity file:///home/aluno/Documentos/ArmazenaBackup /home/aluno/Documentos/BackupRestaurado2
```

Saída:

```text
Nenhuma ação válida encontrada. Irá implicar 'restaurar' porque a fonte de url foi dada e o destino é um caminho local.
Os metadados remotos e locais estão sincronizados; nenhuma sincronização é necessária.
Last full backup date: Tue Oct 14 13:49:00 2025
GnuPG passphrase for decryption:
```

O Duplicity utilizou o backup completo e as alterações armazenadas posteriormente para reconstruir o estado mais recente dos arquivos.

---

## 6. Verificação da restauração

Após a restauração, foi acessado novamente o diretório `Documentos`:

```bash
cd ..
ls
```

Saída:

```text
ArmazenaBackup  BackupRestaurado  BackupRestaurado2  Conteudo
```

Em seguida:

```bash
cd BackupRestaurado2
ls
```

Saída:

```text
teste2.txt  teste.txt
```

A presença dos dois arquivos demonstra que o novo arquivo `teste2.txt` e o arquivo modificado `teste.txt` foram recuperados na restauração.

---

## 7. Conceito aplicado

O backup diferencial registra as alterações realizadas após o último backup completo.

Neste laboratório:

```text
Backup completo
       ↓
teste.txt = "Teste"
       ↓
Alterações
       ├── teste.txt → "Teste Diferencial"
       └── criação de teste2.txt
       ↓
Novo backup
       ↓
Restauração
       ↓
teste.txt + teste2.txt
```

A principal diferença em relação ao backup completo é que o processo posterior utiliza o backup completo como base e registra as alterações realizadas desde ele.

---

## 8. Limpeza do ambiente

Após a validação da restauração, os diretórios utilizados no laboratório foram removidos:

```bash
cd ..
rm -r *
```

Confirmação apresentada pelo sistema:

```text
zsh: sure you want to delete all 4 files in /home/aluno/Documentos [yn]? y
```

Depois:

```bash
ls
```

Saída:

```text
```

O diretório `Documentos` ficou vazio após a limpeza do ambiente.

---

## Evidência

A evidência solicitada para esta atividade corresponde ao **passo 9**, mostrando o conteúdo da pasta `BackupRestaurado2` após a restauração.

[**Evidências — Módulo 7 / Aulas 27 e 28**](../evidencias.pdf)
