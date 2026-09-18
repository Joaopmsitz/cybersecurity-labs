# Atividade 1.8 — Explorando a ferramenta Maltego no Kali Linux

## Objetivo

Conhecer a ferramenta **Maltego** e sua utilização para atividades de OSINT e reconhecimento de informações públicas.

A atividade consistiu em realizar a configuração inicial da ferramenta, autenticar uma conta Maltego e explorar as fontes de dados e recursos disponíveis no **Maltego Data Hub**.

## Ambiente

* Kali Linux
* Terminal
* Maltego
* Firefox
* Maltego Data Hub

## Procedimento

### 1. Criação da conta

Antes de iniciar a ferramenta no Kali Linux, foi criada uma conta gratuita no Maltego utilizando o navegador do computador pessoal.

A conta foi utilizada posteriormente para realizar a ativação da aplicação.

### 2. Inicialização do Maltego

No Kali Linux, a ferramenta foi iniciada pelo Terminal com:

```bash id="e8q3zr"
maltego
```

Após a inicialização, foi apresentada a tela de configuração inicial do programa.

### 3. Seleção do método de ativação

Na tela **Welcome to Maltego**, foi selecionada a opção:

```text
MALTEGO ID
```

Em seguida, foi escolhido:

```text
Online Activation (Default)
```

### 4. Aceite da configuração

Na janela **Configure Maltego**, foi selecionada a opção de aceite para prosseguir com a configuração.

### 5. Autenticação pelo navegador

Na etapa de autenticação, foi selecionada a opção:

```text
Browser Login
```

O Firefox foi aberto automaticamente e as credenciais da conta criada anteriormente foram utilizadas para realizar o login.

Após a autenticação, o navegador apresentou a confirmação:

```text
Authentication Complete
```

### 6. Finalização da configuração

Após retornar ao Maltego, foi apresentada a mensagem:

```text
Have fun using Maltego
```

As etapas de configuração foram avançadas até a seção relacionada aos termos das fontes de dados.

Foi marcada a opção de aceite dos termos e a configuração foi concluída através do botão:

```text
Finish
```

Durante a inicialização também foram fechadas as mensagens introdutórias e o aviso relacionado à alocação de memória.

### 7. Acesso ao Data Hub

Com o Maltego aberto, foi acessada a área:

```text
Transforms → Maltego Data Hub
```

Nessa área foram exploradas as aplicações e fontes de dados disponíveis para utilização em atividades de OSINT.

Essa etapa foi utilizada como evidência da atividade.

## Comandos utilizados

O único comando utilizado no Terminal para iniciar a ferramenta foi:

```bash id="e3h36v"
maltego
```

As demais etapas foram realizadas através da interface gráfica do Maltego e do navegador.

## Resultado

Foi concluída a configuração inicial do Maltego e realizada a autenticação da conta.

Também foi possível acessar o **Maltego Data Hub** e visualizar as fontes de dados e aplicações disponíveis para atividades de OSINT.

## Conceitos praticados

* OSINT
* Reconhecimento passivo
* Maltego
* Maltego Data Hub
* Fontes de dados
* Engenharia social
* Coleta de informações públicas
* Reconhecimento de infraestrutura

## Evidência

A execução da atividade foi registrada no PDF de evidências da Aula 03–04.

[Ver evidências — Aula 03–04](https://github.com/Joaopmsitz/hackers-do-bem-labs/blob/main/fundamental/modulo-01/aula-03-04/evidencias.pdf)
