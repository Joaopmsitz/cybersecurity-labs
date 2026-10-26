# Activity 7.04 — Automated Rsync with Cron

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 07  
> **Classes:** 25–26  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Automate synchronization between two directories using `rsync` and `cron`. The goal is to configure a script that runs the copy operation automatically every minute, allowing files added to `PastaA` to be synchronized to `PastaB`.

## 1. Checking the Directories

First, the directory used in the lab was accessed:

```bash
sudo -i
cd /home/aluno/Documentos
ls
```

Output:

```text
PastaA  PastaB
```

Next, the contents of `PastaA` were checked:

```bash
cd PastaA
ls
```

Output:

```text
Teste.txt
```

`PastaB` was initially empty:

```bash
cd /home/aluno/Documentos/PastaB
ls
```

## 2. Creating the Synchronization Script

The script was created in `/home/aluno/Documentos/`:

```bash
cd /home/aluno/Documentos
nano sync_script.sh
```

File contents:

```bash
#!/bin/bash

rsync -avz /home/aluno/Documentos/PastaA/ /home/aluno/Documentos/PastaB/
```

The script uses `rsync` to synchronize all contents from `PastaA` to `PastaB`.

### Parameters Used

- `-a` — archive mode, preserving file attributes and enabling recursive copying.
- `-v` — displays information about the files being processed.
- `-z` — enables compression during transfer.
- `/home/aluno/Documentos/PastaA/` — source directory.
- `/home/aluno/Documentos/PastaB/` — destination directory.

## 3. Making the Script Executable

After saving the script, execute permission was granted:

```bash
chmod +x sync_script.sh
```

## 4. Configuring Cron

The root user's task scheduler was opened:

```bash
crontab -e
```

Because there was no existing crontab configuration, the system displayed:

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

The following entry was added:

```cron
* * * * * /home/aluno/Documentos/sync_script.sh
```

This expression schedules the script to run every minute.

### Cron Expression Structure

```text
* * * * * command
│ │ │ │ │
│ │ │ │ └── Day of the week
│ │ │ └──── Month
│ │ └────── Day of the month
│ └──────── Hour
└────────── Minute
```

Because every field contains `*`, the script runs once per minute, regardless of the hour, day, or month.

## 5. Verifying Automatic Synchronization

After waiting for the scheduled cron job to run, the destination directory was accessed in a second terminal:

```bash
sudo -i
cd /home/aluno/Documentos/PastaB
ls
```

The file in `PastaA` was automatically synchronized to `PastaB`.

## 6. Testing with a Second File

To verify the automation again, a second file was created in `PastaA`:

```bash
cd /home/aluno/Documentos/PastaA
nano Teste2.txt
```

Content:

```text
Novo teste!
```

After the next cron execution, the file became available in `PastaB`, demonstrating that synchronization did not require manually running `rsync`.

The output recorded during the lab was:

```text
┌──(root㉿kali)-[/home/aluno/Documentos/PastaB]
└─# ls
Teste1.txt  Teste2.txt
```

The output above has been preserved as recorded during the activity.

## 7. Cleaning Up the Environment

After testing, the session returned to the main directory:

```bash
cd /home/aluno/Documentos/
ls
```

Output:

```text
PastaA  PastaB  sync_script.sh
```

The contents used in the lab were removed:

```bash
rm -r *
```

The system requested confirmation:

```text
zsh: sure you want to delete all 3 files in /home/aluno/Documentos [yn]? y
```

Finally:

```bash
ls
```

The directory was empty.

## 8. Restarting the System

At the end of the activity, the machine was restarted:

```bash
reboot
```

## Evidence

Evidence for this activity is included in the PDF for Module 7, Classes 25–26.

[View Evidence — Classes 25–26](../evidencias.pdf)

---

[Back to Classes 25–26](../) · [Back to Module 7](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
