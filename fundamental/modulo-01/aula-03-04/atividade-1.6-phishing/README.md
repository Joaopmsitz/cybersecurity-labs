# Atividade 1.6 — Conhecendo a ferramenta ShellPhish no Kali Linux

## Objetivo

Explorar, em um ambiente controlado de laboratório, o funcionamento básico de uma ferramenta de simulação de phishing.

A atividade utiliza uma página de login falsa hospedada localmente para demonstrar como informações inseridas em um formulário podem ser capturadas por uma aplicação maliciosa.

> **Aviso:** toda a atividade foi realizada exclusivamente no ambiente de laboratório, utilizando `localhost` e credenciais fictícias fornecidas pelo exercício.

## Ambiente

* Kali Linux
* Terminal
* ShellPhish
* Firefox ESR
* Servidor local em `localhost`
* Porta `5050`

## Procedimento

### 1. Acesso ao modo administrador

Foi aberto o Terminal e utilizado o `sudo` para acessar o modo administrador:

```bash
sudo -i
```

### 2. Acesso ao diretório da ferramenta

Em seguida, foi acessado o diretório onde o ShellPhish estava disponibilizado:

```bash
cd /curso/ShellPhish
```

O conteúdo do diretório foi verificado com:

```bash
ls
```

Entre os arquivos encontrados estavam o script principal da ferramenta, arquivos de configuração e os diretórios contendo os sites utilizados na simulação.

### 3. Inicialização do ShellPhish

A ferramenta foi executada através do script principal:

```bash
bash shellphish.sh
```

Após a inicialização, foi apresentado o menu com os sites disponíveis para a simulação.

### 4. Seleção do site utilizado na simulação

Para o exercício, foi selecionada a opção correspondente ao Facebook:

```text
[01] Facebook
```

Em seguida, foi selecionada a opção de página tradicional de login:

```text
[01] Traditional Login Page
```

### 5. Configuração do acesso local

Na etapa de configuração do método de hospedagem, foi selecionada a opção:

```text
[01] LocalHost
```

Foi utilizada a porta:

```text
5050
```

A ferramenta então disponibilizou a página localmente em:

```text
http://localhost:5050
```

O uso de `localhost` mantém a simulação restrita ao próprio ambiente do laboratório.

### 6. Acesso à página simulada

O endereço abaixo foi aberto no Firefox ESR:

```text
http://localhost:5050
```

Foi apresentada uma página de login simulada.

Para a demonstração, foram utilizadas somente as credenciais fictícias fornecidas pela atividade:

```text
Usuário: teste_usuario
Senha: teste_senha
```

Essas credenciais não correspondem a uma conta real.

### 7. Observação da captura

Após o envio do formulário, a autenticação não foi realizada e a ferramenta apresentou no Terminal as informações recebidas durante a simulação.

O ShellPhish também registrou o endereço de origem utilizado no laboratório:

```text
Victim IP: 127.0.0.1
```

Em seguida, foram exibidos os dados fictícios utilizados no teste.

O resultado demonstrou, de forma controlada, que uma página de phishing pode encaminhar os dados inseridos pelo usuário para o operador da aplicação.

### 8. Encerramento

Após observar o resultado, a ferramenta foi encerrada com:

```text
Ctrl + C
```

O navegador e o Terminal foram fechados ao final da atividade.

## Comandos utilizados

```bash
sudo -i
cd /curso/ShellPhish
ls
bash shellphish.sh
```

O acesso à página simulada foi realizado pelo navegador através de:

```text
http://localhost:5050
```

## Resultado

Foi possível executar uma simulação local de phishing e observar o fluxo básico de uma página falsa de autenticação.

A atividade demonstrou:

* Hospedagem de uma página falsa em ambiente local;
* Funcionamento básico de um formulário de autenticação malicioso;
* Captura de informações submetidas pelo usuário;
* Identificação do endereço de origem da conexão;
* Importância de verificar o endereço e a autenticidade de páginas de login.

## Conceitos praticados

* Phishing
* Engenharia social
* Páginas falsas de autenticação
* Captura de credenciais
* `localhost`
* Endereço IP de loopback (`127.0.0.1`)
* Segurança de aplicações web
* Conscientização contra ataques de phishing

## Evidência

A execução da atividade foi registrada no PDF de evidências da Aula 03–04.

[Ver evidências — Aula 03–04](https://github.com/Joaopmsitz/hackers-do-bem-labs/blob/main/fundamental/modulo-01/aula-03-04/evidencias.pdf)
