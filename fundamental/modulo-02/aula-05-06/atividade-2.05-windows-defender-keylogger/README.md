# Atividade 2.5 — Explorando como o Windows Defender detecta um Keylogger como programa malicioso

## Objetivo

Explorar, em um ambiente controlado de laboratório, como os mecanismos de proteção do Windows identificam e bloqueiam um arquivo associado a um **keylogger**.

A atividade utilizou o **Microsoft Defender SmartScreen** para observar o comportamento do sistema de segurança diante da tentativa de download de um arquivo contendo um keylogger.

O objetivo principal foi compreender como mecanismos de proteção de endpoints podem impedir o acesso a arquivos potencialmente maliciosos antes mesmo de sua execução.

> **Aviso:** a atividade foi realizada exclusivamente para fins acadêmicos e em ambiente de laboratório. O arquivo analisado não foi executado.

## Ambiente

* Windows Server 2022
* Microsoft Edge
* Microsoft Defender SmartScreen
* Explorador de Arquivos
* Máquina virtual de laboratório
* Repositório público no GitHub contendo o exemplo de keylogger utilizado na atividade

## Procedimento

### 1. Acesso ao ambiente Windows

A máquina virtual com Windows Server 2022 foi inicializada e, após o acesso ao sistema, foi aberta a área de trabalho.

Na primeira utilização do sistema, foi apresentada a pergunta relacionada à descoberta do computador na rede:

```text
Do you want to allow your PC to be discoverable by Other PCs and devices on this network?
```

O ambiente de laboratório foi configurado conforme solicitado pela atividade.

### 2. Acesso ao repositório do keylogger

O Microsoft Edge foi aberto e o endereço abaixo foi acessado:

```text
https://github.com/MinhasKamal/StupidKeylogger
```

O repositório apresenta um projeto denominado **StupidKeylogger**, utilizado na atividade para demonstrar o funcionamento de um programa capaz de registrar entradas de teclado.

A consulta ao repositório permitiu observar a finalidade do projeto antes da tentativa de download.

### 3. Acesso ao arquivo para download

Em uma nova aba do Microsoft Edge, foi acessado o arquivo compactado disponibilizado pelo projeto:

```text
https://github.com/MinhasKamal/StupidKeylogger/archive/application.zip
```

O objetivo dessa etapa era observar como o mecanismo de proteção do Windows responderia à tentativa de obtenção do arquivo.

### 4. Bloqueio pelo Microsoft Defender SmartScreen

Durante a tentativa de download, o Microsoft Edge apresentou uma mensagem informando que o arquivo havia sido bloqueado por ser considerado inseguro:

```text
StupidKeylogger-application.zip was blocked as unsafe by Microsoft Defender SmartScreen.
```

Esse foi o principal resultado observado na atividade.

O SmartScreen impediu inicialmente o download do arquivo, demonstrando a atuação de um mecanismo de proteção integrado ao Windows e ao navegador Microsoft Edge.

### 5. Observação das opções de segurança

A mensagem de bloqueio disponibilizada pelo navegador apresentava opções relacionadas ao arquivo.

A interface permitiu visualizar as opções adicionais através do menu representado pelos três pontos.

O laboratório demonstrou que, mesmo diante de uma tentativa de obtenção de um arquivo classificado como inseguro, o mecanismo de proteção apresenta uma etapa de alerta antes que o usuário consiga acessar o conteúdo.

> A atividade foi realizada para observar o comportamento do mecanismo de segurança. O arquivo não foi executado.

### 6. Mensagem adicional de proteção

Após a interação prevista pelo exercício, o Microsoft Edge apresentou uma segunda mensagem de segurança:

```text
This app is unsafe
```

Essa mensagem reforçou a classificação do conteúdo como potencialmente perigoso.

O comportamento observado demonstra que a proteção não se limita a uma simples notificação de download: o navegador continua apresentando alertas relacionados à segurança do arquivo.

### 7. Verificação da pasta Downloads

Após a etapa de download prevista pelo laboratório, o **Explorador de Arquivos** foi aberto e a pasta `Downloads` foi acessada.

Foi localizado o arquivo associado ao projeto:

```text
StupidKeylogger-application.zip
```

A presença do arquivo permitiu verificar visualmente o resultado da atividade no sistema de arquivos.

Essa etapa corresponde ao **print solicitado pela atividade**.

O arquivo permaneceu somente como objeto de análise. Não foi realizada a instalação nem a execução do keylogger.

## Comandos e ações utilizados

Diferentemente das atividades realizadas no Kali Linux, esta atividade foi executada principalmente através da interface gráfica do Windows.

O fluxo utilizado foi:

```text
Microsoft Edge
    │
    ▼
Repositório StupidKeylogger
    │
    ▼
Arquivo application.zip
    │
    ▼
Microsoft Defender SmartScreen
    │
    ▼
Alerta de segurança
    │
    ▼
Downloads
    │
    ▼
Inspeção do arquivo
```

Não foram necessários comandos de Terminal ou PowerShell para realizar o experimento.

## Interpretação

O laboratório demonstrou a atuação do **Microsoft Defender SmartScreen** diante de um arquivo associado a um keylogger.

O SmartScreen apresentou inicialmente:

```text
StupidKeylogger-application.zip was blocked as unsafe by Microsoft Defender SmartScreen.
```

E posteriormente:

```text
This app is unsafe
```

Essas mensagens indicam que o mecanismo de proteção classificou o conteúdo como potencialmente inseguro e aplicou uma barreira durante o processo de obtenção do arquivo.

A atividade é importante para compreender uma camada de defesa presente em endpoints Windows: a proteção pode atuar **antes da execução do código**, reduzindo a possibilidade de que um usuário obtenha e execute diretamente um arquivo potencialmente malicioso.

O experimento também mostra a importância de mecanismos de segurança em conjunto com a conscientização do usuário. Um alerta de segurança durante um download pode impedir que um artefato potencialmente perigoso chegue à etapa de execução.

## Resultado

Foi possível:

* Acessar o projeto utilizado como exemplo de keylogger;
* Identificar o arquivo compactado disponibilizado pelo projeto;
* Realizar a tentativa de download no Microsoft Edge;
* Observar o bloqueio realizado pelo Microsoft Defender SmartScreen;
* Visualizar a mensagem:

```text
StupidKeylogger-application.zip was blocked as unsafe by Microsoft Defender SmartScreen.
```

* Observar posteriormente a mensagem:

```text
This app is unsafe
```

* Acessar a pasta `Downloads`;
* Localizar o arquivo utilizado na demonstração;
* Observar na prática uma camada de proteção do Windows contra conteúdo potencialmente malicioso.

O arquivo não foi executado durante a atividade.

## Conceitos praticados

* Microsoft Defender
* Microsoft Defender SmartScreen
* Segurança de endpoints
* Keylogger
* Malware
* Detecção de arquivos maliciosos
* Bloqueio de downloads
* Segurança de navegadores
* Proteção preventiva
* Análise de artefatos
* Threat Prevention

## Evidência

A execução da atividade foi registrada no PDF de evidências da Aula 05–06.

[Ver evidências — Aula 05–06](https://github.com/Joaopmsitz/hackers-do-bem-labs/blob/main/fundamental/modulo-02/aula-05-06/evidencias.pdf)
