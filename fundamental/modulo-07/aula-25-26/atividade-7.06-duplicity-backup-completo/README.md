# Atividade 7.6 — Backup Completo Local com Duplicity

## Objetivo

Realizar um backup completo local de uma pasta utilizando o `Duplicity` e, posteriormente, restaurar os arquivos armazenados em uma nova pasta.

O `Duplicity` utiliza o GnuPG para criptografar os dados do backup, permitindo armazenar os arquivos de forma protegida.

---

## 1. Acesso ao usuário root

Inicialmente, foi aberto o Terminal e obtido acesso de superusuário:

```bash
sudo -i
```

---

## 2. Criação da pasta de conteúdo

Foi criada a pasta `Conteudo` dentro de `/home/aluno/Documentos/`:

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

Foi acessada a pasta `Conteudo` e criado o arquivo `teste.txt`:

```bash
cd Conteudo
nano teste.txt
```

O conteúdo inserido no arquivo foi:

```text
Teste
```

---

## 4. Criação do backup completo com Duplicity

O backup da pasta `Conteudo` foi realizado utilizando como destino local a pasta `ArmazenaBackup`:

```bash
duplicity /home/aluno/Documentos/Conteudo file:///home/aluno/Documentos/ArmazenaBackup
```

Durante a execução, o Duplicity solicitou uma senha para criptografia do backup.

Saída registrada:

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

indica que não havia um backup anterior no destino. Dessa forma, o Duplicity realizou um **backup completo (full backup)**.

---

## 5. Verificação do diretório de backup

Após a criação do backup, foi retornado ao diretório `Documentos`:

```bash
cd ..
ls
```

Saída:

```text
ArmazenaBackup  Conteudo
```

A pasta `ArmazenaBackup` foi criada para armazenar os dados gerados pelo Duplicity.

---

## 6. Verificação dos arquivos do backup

Foi acessada a pasta de armazenamento:

```bash
cd ArmazenaBackup
ls
```

Os arquivos gerados pelo Duplicity foram apresentados no diretório:

```text
duplicity-full.20240222T032821Z.manifest.gpg
duplicity-full.20240222T032821Z.vol1.difftar.gpg
duplicity-full-signatures.20240222T032821Z.sigtar.gpg
```

Os nomes dos arquivos podem variar conforme a execução.

---

## 7. Restauração do backup

Para testar a recuperação, o backup armazenado em `ArmazenaBackup` foi restaurado para a pasta `BackupRestaurado`:

```bash
duplicity file:///home/aluno/Documentos/ArmazenaBackup /home/aluno/Documentos/BackupRestaurado
```

Durante o processo, foi solicitada a senha utilizada na criação do backup.

Saída:

```text
Nenhuma ação válida encontrada. Irá implicar 'restaurar' porque a fonte de url foi dada e o destino é um caminho local.
Os metadados remotos e locais estão sincronizados; nenhuma sincronização é necessária.
Last full backup date: Tue Oct 14 13:49:00 2025
GnuPG passphrase for decryption:
```

---

## 8. Verificação dos arquivos restaurados

Após a restauração, foi acessado o diretório `BackupRestaurado`:

```bash
cd ..
ls
```

Saída:

```text
ArmazenaBackup  BackupRestaurado  Conteudo
```

Em seguida:

```bash
cd BackupRestaurado
ls
```

Saída:

```text
teste.txt
```

Por fim, o conteúdo do arquivo foi conferido:

```bash
cat teste.txt
```

Resultado:

```text
Teste
```

O arquivo `teste.txt` foi restaurado corretamente e seu conteúdo permaneceu íntegro.

---

## Evidência

A evidência solicitada para esta atividade corresponde ao **passo 8**, mostrando o conteúdo da pasta `BackupRestaurado` e a verificação do arquivo recuperado.

[**Evidências — Módulo 7 / Aulas 25 e 26**](../evidencias.pdf)
