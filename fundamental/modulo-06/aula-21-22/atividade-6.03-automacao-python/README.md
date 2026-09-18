# Atividade 6.3 — Automação de Tarefas com Python no Kali Linux

## Objetivo

Nesta atividade foi desenvolvido um script em **Python** para automatizar a coleta de informações do sistema Linux e gerar um relatório com os dados obtidos.

O script coleta informações como hostname, versão do kernel, modelo do processador, memória disponível e utilização do armazenamento, organizando esses dados em um arquivo de texto.

A atividade demonstra como a automação pode ser utilizada para realizar tarefas de inventário e coleta de informações de sistemas.

---

## Ambiente

* **Sistema:** Kali Linux
* **Acesso:** RDP
* **IP da máquina:** `192.168.98.40`
* **Usuário:** `aluno`
* **Diretório de trabalho:** `/home/aluno/Documentos`

> As credenciais utilizadas no laboratório não são registradas neste documento.

---

## 1. Acessando o terminal

Após acessar o Kali Linux por RDP, foi aberto o terminal e obtido acesso administrativo:

```bash
sudo -i
```

O acesso administrativo foi utilizado durante a execução da atividade.

---

## 2. Criando o script Python

Foi utilizado o editor Mousepad para criar o arquivo:

```text
/home/aluno/Documentos/dados_linux.py
```

O código desenvolvido foi:

```python
import os
import socket

# Função para coletar informações do sistema
def coletar_informacoes_sistema():
    hostname = socket.gethostname()
    kernel_version = os.uname().release
    cpu_info = os.popen('cat /proc/cpuinfo | grep "model name" | uniq').read().strip()
    mem_info = os.popen('free -h | grep "Mem.:"').read().strip()
    disk_space = os.popen('df -h').read()

    informacoes = {
        "Hostname": hostname,
        "Kernel Version": kernel_version,
        "CPU Info": cpu_info,
        "Memory Info": mem_info,
        "Disk Space": disk_space
    }

    return informacoes

# Função para gerar um relatório
def gerar_relatorio(informacoes):
    relatorio = "Relatório do Sistema Linux\n\n"
    for chave, valor in informacoes.items():
        relatorio += f"{chave}: {valor}\n"

    with open("relatorio_linux.txt", "w") as arquivo:
        arquivo.write(relatorio)

if __name__ == "__main__":
    informacoes_sistema = coletar_informacoes_sistema()
    gerar_relatorio(informacoes_sistema)
    print("Relatório gerado com sucesso em 'relatorio_linux.txt'")
```

---

## 3. Estrutura do script

O script utiliza módulos nativos do Python para coletar informações do sistema:

```python
import os
import socket
```

O módulo `socket` é utilizado para obter o hostname da máquina:

```python
hostname = socket.gethostname()
```

Já o módulo `os` permite interagir com recursos do sistema operacional.

A versão do kernel é obtida através de:

```python
kernel_version = os.uname().release
```

Para obter informações do processador, o script executa um comando do sistema:

```python
cpu_info = os.popen('cat /proc/cpuinfo | grep "model name" | uniq').read().strip()
```

A memória é coletada através de:

```python
mem_info = os.popen('free -h | grep "Mem.:"').read().strip()
```

E o espaço em disco através de:

```python
disk_space = os.popen('df -h').read()
```

---

## 4. Gerando o relatório

As informações coletadas são armazenadas em um dicionário:

```python
informacoes = {
    "Hostname": hostname,
    "Kernel Version": kernel_version,
    "CPU Info": cpu_info,
    "Memory Info": mem_info,
    "Disk Space": disk_space
}
```

Depois, a função `gerar_relatorio()` percorre os dados e cria o arquivo:

```text
relatorio_linux.txt
```

A gravação é realizada através de:

```python
with open("relatorio_linux.txt", "w") as arquivo:
    arquivo.write(relatorio)
```

Dessa forma, o script transforma a coleta realizada no terminal em um relatório persistente.

---

## 5. Executando o script

Após salvar o arquivo, foi acessado o diretório de trabalho:

```bash
cd /home/aluno/Documentos/
```

Em seguida, o script foi executado com:

```bash
python dados_linux.py
```

Saída observada:

```text
Relatório gerado com sucesso em 'relatorio_linux.txt'
```

A mensagem confirma que o script foi executado e que o arquivo de relatório foi criado.

---

## 6. Verificando os arquivos gerados

Foi utilizado o comando:

```bash
ls
```

Saída observada:

```text
dados_linux.py  relatorio_linux.txt
```

O resultado demonstra a presença tanto do script Python quanto do relatório gerado automaticamente.

---

## 7. Visualizando o relatório

Para visualizar o conteúdo gerado pelo script, foi executado:

```bash
cat relatorio_linux.txt
```

Saída observada:

```text
Relatório do Sistema Linux

Hostname: kali
Kernel Version: 6.12.38+kali-cloud-amd64
CPU Info: model name    : AMD EPYC 7571
Memory Info: Mem.:          3,8Gi       881Mi       924Mi        15Mi       2,3Gi       2,9Gi
Disk Space: Sist. Arq.       Tam. Usado Disp. Uso% Montado em
udev             1,9G     0  1,9G   0% /dev
tmpfs            388M  956K  387M   1% /run
/dev/nvme0n1p1    20G   19G  101M 100% /
tmpfs            1,9G  4,0K  1,9G   1% /dev/shm
tmpfs            5,0M     0  5,0M   0% /run/lock
tmpfs            1,9G   56K  1,9G   1% /tmp
tmpfs            1,0M     0  1,0M   0% /run/credentials/systemd-journald.service
/dev/nvme0n1p15  124M  294K  124M   1% /boot/efi
tmpfs            1,0M     0  1,9G   0% /run/credentials/serial-getty@ttyS0.service
/dev/nvme0n1p15  124M  294K  124M   1% /boot/efi
tmpfs            1,0M     0  1,0M   0% /run/credentials/getty@tty1.service
tmpfs            388M  120K  388M   0% /run/user/0
tmpfs            388M  140K  388M   0% /run/user/1001
```

> **Observação:** a saída acima é registrada conforme apresentada durante o laboratório. O ponto mais relevante para análise do armazenamento é `/dev/nvme0n1p1`, que aparece com **20 GB de tamanho, 19 GB utilizados, 101 MB disponíveis e 100% de utilização**.

**Este é o passo solicitado para a evidência da atividade.**

---

## Análise das informações coletadas

### Hostname

```text
Hostname: kali
```

O hostname identifica o nome atribuído à máquina dentro do ambiente.

### Kernel

```text
Kernel Version: 6.12.38+kali-cloud-amd64
```

A informação identifica a versão do kernel Linux em execução.

### CPU

```text
CPU Info: model name    : AMD EPYC 7571
```

O script identificou o processador disponibilizado para a máquina virtual.

### Memória

```text
Memory Info: Mem.:          3,8Gi       881Mi       924Mi        15Mi       2,3Gi       2,9Gi
```

A informação foi obtida utilizando o comando `free -h`, que apresenta os valores de memória em formato legível.

### Armazenamento

A saída do `df -h` apresenta informações sobre os sistemas de arquivos, incluindo:

* sistema de arquivos;
* tamanho total;
* espaço utilizado;
* espaço disponível;
* percentual de utilização;
* ponto de montagem.

Um ponto de atenção identificado no laboratório foi:

```text
/dev/nvme0n1p1    20G   19G  101M 100% /
```

Isso indica que a partição raiz estava praticamente sem espaço disponível, apresentando **100% de utilização**.

Em um ambiente real, uma situação desse tipo merece atenção porque a falta de espaço pode afetar gravações de arquivos, logs, atualizações e o funcionamento de serviços.

---

## 8. Limpeza dos arquivos

Após concluir a atividade e registrar a evidência, os arquivos utilizados foram verificados:

```bash
ls
```

Saída:

```text
dados_linux.py  relatorio_linux.txt
```

Em seguida, os arquivos foram removidos:

```bash
rm *
```

O terminal solicitou confirmação:

```text
zsh: sure you want to delete all 2 files in /home/aluno/Documentos [yn]? y
```

Após a confirmação, foi executado novamente:

```bash
ls
```

A limpeza removeu os arquivos criados durante a atividade.

---

## Conceitos envolvidos

### Automação

A automação permite transformar uma sequência de tarefas manuais em um processo executável por um programa.

Neste laboratório, em vez de executar manualmente diversos comandos para consultar o sistema, o Python reuniu essas operações em um único script.

### Coleta de informações

O script realiza uma coleta básica de informações de inventário:

```text
Hostname
Kernel
CPU
Memória
Armazenamento
```

Esse tipo de coleta pode ser útil em administração de sistemas, troubleshooting, inventário e atividades de monitoramento.

### Python + comandos do sistema

A atividade também demonstra como um programa Python pode interagir com informações fornecidas pelo sistema operacional.

Por exemplo:

```python
os.popen('df -h').read()
```

executa o comando `df -h` e captura sua saída para utilização dentro do programa.

---

## Resultado

Foi desenvolvido e executado um script Python capaz de:

1. identificar o hostname;
2. obter a versão do kernel;
3. identificar o processador;
4. consultar informações de memória;
5. consultar o espaço em disco;
6. organizar os dados coletados;
7. gerar automaticamente um arquivo `relatorio_linux.txt`.

A execução foi confirmada pela mensagem:

```text
Relatório gerado com sucesso em 'relatorio_linux.txt'
```

e pela presença dos arquivos:

```text
dados_linux.py  relatorio_linux.txt
```

O relatório posteriormente foi exibido com `cat`, permitindo visualizar as informações coletadas.

---

## Evidência

A evidência desta atividade corresponde ao **passo 8**, contendo a saída do relatório gerado pelo script Python.

[**Evidências — Módulo 6 / Aulas 1 e 2**](../evidencias.pdf)
