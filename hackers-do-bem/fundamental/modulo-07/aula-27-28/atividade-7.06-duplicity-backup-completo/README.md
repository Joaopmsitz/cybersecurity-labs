# Atividade 7.6 — Backup Completo Local com Duplicity

## Objetivo

Realizar um **backup completo local** utilizando o `Duplicity` no Kali Linux e, em seguida, restaurar os arquivos para verificar a integridade do backup.

O `Duplicity` realiza backups utilizando criptografia e pode armazenar os dados em diferentes destinos. Neste laboratório, o armazenamento será feito localmente em outra pasta do sistema.

---

## Ambiente

* **Sistema:** Kali Linux
* **Ferramenta:** Duplicity
* **Origem:** `/home/aluno/Documentos/Conteudo`
* **Destino do backup:** `/home/aluno/Documentos/ArmazenaBackup`
* **Diretório de restauração:** `/home/aluno/Documentos/BackupRestaurado`

> As credenciais utilizadas no ambiente de laboratório não são registradas neste README.

---

## 1. Acesso como root

Foi utilizado o usuário `root` para executar as operações do laboratório.

```bash
sudo -i
```

---

## 2. Criação do diretório de conteúdo

Acessando o diretório `Documentos` e criando a pasta que será utilizada como origem do backup:

```bash
cd /home/aluno/Documentos
mkdir Conteudo
ls
```

Saída:

```text
Conteudo
```

---

## 3. Criação do arquivo para backup

Entrando na pasta `Conteudo`:

```bash
cd Conteudo
nano teste.txt
```

No arquivo foi inserido o seguinte conteúdo:

```text
Teste
```

Esse arquivo será utilizado posteriormente para verificar se a restauração foi realizada corretamente.

---

## 4. Criação do backup completo

O backup foi realizado com o seguinte comando:

```bash
duplicity /home/aluno/Documentos/Conteudo file:///home/aluno/Documentos/ArmazenaBackup
```

Saída apresentada pelo Duplicity:

```text
Nenhuma ação válida encontrada. Irá implicar 'backup' porque uma fonte de caminho foi informada e o destino é um local URL.
Os metadados remotos e locais estão sincronizados; nenhuma sincronização é necessária.
Data da última cópia de segurança completa: nenhuma
GnuPG passphrase for decryption: 
Redigite a senha para descriptografar para confirmar: 
Não encontrou assinaturas, a mudança para backup completo.
--------------[ Estatísticas de backup ]--------------
StartTime 1760460572.13 (Tue Oct 14 13:49:32 2025)
EndTime 1760460572.14 (Tue Oct 14 13:49:32 2025)
ElapsedTime 0.01 (0.01 seconds)
SourceFiles 2
SourceFileSize 4102 (4.01 KB)
NewFiles 2
NewFileSize 4102 (4.01 KB)
DeletedFiles 0
ChangedFiles 0
ChangedFileSize 0 (0 bytes)
ChangedDeltaSize 0 (0 bytes)
DeltaEntries 2
RawDeltaSize 6 (6 bytes)
TotalDestinationSizeChange 227 (227 bytes)
Errors 0
------------------------------------------------------
```

A mensagem:

```text
Não encontrou assinaturas, a mudança para backup completo.
```

indica que não havia uma assinatura de backup anterior disponível para comparação. Dessa forma, o Duplicity realizou um **backup completo**.

As estatísticas também indicam que foram processados **2 arquivos**, totalizando aproximadamente **4,01 KB**, sem erros:

```text
SourceFiles 2
SourceFileSize 4102 (4.01 KB)
NewFiles 2
NewFileSize 4102 (4.01 KB)
Errors 0
```

---

## 5. Verificação dos arquivos de backup

Após a execução do backup, foi verificado o conteúdo do diretório `Documentos`:

```bash
cd ..
ls
```

Saída:

```text
ArmazenaBackup  Conteudo
```

O diretório `ArmazenaBackup` foi criado para armazenar os dados gerados pelo Duplicity.

Em seguida:

```bash
cd ArmazenaBackup
ls
```

Saída registrada no laboratório:

```text
duplicity-full.20240222T032821Z.manifest.gpg
duplicity-full.20240222T032821Z.vol1.difftar.gpg
duplicity-full-signatures.20240222T032821Z.sigtar.gpg
```

Os nomes dos arquivos podem variar conforme a data e o horário em que o backup é executado.

Os arquivos armazenados pelo Duplicity incluem o manifesto, os dados do backup e as informações de assinatura necessárias para o gerenciamento dos backups.

---

## 6. Restauração do backup

Com o backup criado, foi realizada a restauração para um novo diretório:

```bash
duplicity file:///home/aluno/Documentos/ArmazenaBackup /home/aluno/Documentos/BackupRestaurado
```

Saída:

```text
Nenhuma ação válida encontrada. Irá implicar 'restaurar' porque a fonte de url foi dada e o destino é um caminho local.
Os metadados remotos e locais estão sincronizados; nenhuma sincronização é necessária.
Last full backup date: Tue Oct 14 13:49:00 2025
GnuPG passphrase for decryption:
```

Nesse processo, o Duplicity utiliza os arquivos armazenados em `ArmazenaBackup` para reconstruir o conteúdo original no diretório `BackupRestaurado`.

---

## 7. Verificação dos arquivos restaurados

Após a restauração, foi acessado novamente o diretório `Documentos`:

```bash
cd ..
ls
```

Saída:

```text
ArmazenaBackup  BackupRestaurado  Conteudo
```

Foi acessado o diretório de restauração:

```bash
cd BackupRestaurado
ls
```

Saída:

```text
teste.txt
```

Por fim, o conteúdo do arquivo restaurado foi verificado:

```bash
cat teste.txt
```

Saída:

```text
Teste
```

A restauração reproduziu o arquivo `teste.txt` com o mesmo conteúdo criado originalmente em `Conteudo`, confirmando a recuperação dos dados do backup.

---

## Evidência

A evidência solicitada para esta atividade corresponde ao **passo 8**, apresentando a pasta `BackupRestaurado`, o arquivo `teste.txt` e seu conteúdo após a restauração.

[**Evidências — Módulo 7 / Aulas 27 e 28**](../evidencias.pdf)
