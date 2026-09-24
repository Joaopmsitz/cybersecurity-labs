# Atividade 2.8 — Tor Browser no Kali Linux

## Objetivo

Configurar e utilizar o **Tor Browser** no Kali Linux para observar, em um ambiente controlado, como uma conexão realizada através da rede Tor pode apresentar um endereço IP de saída diferente daquele observado em uma conexão convencional.

A atividade também permite visualizar informações associadas ao endereço IP apresentado por um serviço de consulta, comparando o acesso pelo Tor Browser com o acesso pelo navegador convencional.

## Ambiente

* Kali Linux
* Terminal
* Tor Browser
* Firefox
* `torbrowser-launcher`
* Rede Tor
* Serviço de consulta de endereço IP

## 1. Iniciando o Tor Browser

O Tor Browser foi iniciado através do terminal com:

```bash
torbrowser-launcher
```

Na primeira execução, o launcher realizou o download e a preparação do navegador:

```text
Lançador do Navegador Tor
By Micah Lee & Tor Project, licensed under MIT
versão 0.3.7
https://gitlab.torproject.org/tpo/applications/torbrowser-launcher/
Criando o diretório inicial do GnuPG /home/aluno/.local/share/torbrowser/gnupg_homedir
Downloading Tor Browser for the first time.
Baixando https://aus1.torproject.org/torbrowser/update_3/release/Linux_x86_64-gcc3/x/ALL
MESA: error: ZINK: failed to choose pdev
glx: failed to create drisw screen
Versão mais recente: 13.5.6
Baixando https://dist.torproject.org/torbrowser/13.5.6/tor-browser-linux-x86_64-13.5.6.tar.xz.asc
Baixando https://dist.torproject.org/torbrowser/13.5.6/tor-browser-linux-x86_64-13.5.6.tar.xz
Verificando Assinatura
Downloading latest Tor Browser signing key...
Key imported successfully
Extraindo tor-browser-linux-x86_64-13.5.6.tar.xz
Rodando /home/aluno/.local/share/torbrowser/tbb/x86_64/tor-browser/start-tor-browser.desktop
Launching './Browser/start-tor-browser --detach'...
```

O processo realizou as seguintes etapas:

1. Criou o diretório utilizado pelo launcher;
2. Verificou a versão disponível do Tor Browser;
3. Baixou o pacote do navegador;
4. Baixou a chave utilizada para verificar a assinatura;
5. Verificou a assinatura;
6. Extraiu o navegador;
7. Iniciou o Tor Browser.

As mensagens relacionadas ao `MESA`/`ZINK` apareceram durante a inicialização gráfica do ambiente e não impediram a continuação da atividade.

## 2. Estabelecendo a conexão Tor

Após a abertura do Tor Browser, foi utilizada a opção **Connect** para estabelecer a conexão com a rede Tor.

Durante o processo, caso a conexão não fosse estabelecida normalmente, foi utilizada a opção **Try a bridge**, conforme o procedimento apresentado no laboratório.

A conexão estabelecida pelo navegador permite que o tráfego seja encaminhado pela rede Tor antes de chegar ao destino.

## 3. Acessando a Web pelo Tor Browser

Com o navegador conectado à rede Tor, foi acessado:

```text
https://duckduckgo.com/
```

A página foi utilizada apenas para confirmar o funcionamento da navegação através do Tor.

Em seguida, foi aberta uma nova aba para consultar o endereço IP observado externamente:

```text
https://whatismyipaddress.com/
```

Foi aceita a solicitação de privacidade apresentada pelo site para visualizar as informações disponíveis.

## 4. Verificando o endereço IP através do Tor

A consulta apresentou um endereço IPv4 e informações associadas ao nó de saída utilizado pela conexão do laboratório.

Exemplo observado durante a atividade:

```text
IPv6: ? 2a0b:f4c0:16c:16::1

IPv4: ? 185.220.100.240

Your location may be exposed!
Hide My IP Address Now

Show Complete IP Details

My IP Information:

ISP: Stiftung Erneuerbare Freiheit

Services: Tor Exit Node

City: Frankfurt am Main

Region: Hessen

Country: Germany
```

O resultado identificou o endereço como pertencente a um **Tor Exit Node**, indicando que a conexão estava saindo para a Internet através de um nó de saída da rede Tor.

A localização apresentada pelo serviço corresponde ao ponto associado ao endereço IP de saída, e não necessariamente à localização real do usuário.

## 5. Comparação com uma conexão convencional

Para comparar o resultado, o mesmo serviço foi acessado pelo Firefox convencional, fora do Tor Browser.

O resultado observado foi:

```text
IPv4: 107.22.123.86

IPv6: Not detected

Your location may be exposed!
Hide My IP Address Now

Show Complete IP Details

My IP Information:

ISP: Amazon.com Inc.

City: Ashburn

Region: Virginia

Country: United States
```

Os resultados demonstram que os dois navegadores apresentaram endereços IP diferentes para o serviço consultado.

### Comparação observada

| Acesso               | IPv4 observado    | Informações apresentadas          |
| -------------------- | ----------------- | --------------------------------- |
| Tor Browser          | `185.220.100.240` | Tor Exit Node / Frankfurt am Main |
| Firefox convencional | `107.22.123.86`   | Amazon.com Inc. / Ashburn         |

Os endereços acima correspondem aos resultados observados no laboratório e não devem ser interpretados como endereços atuais.

## 6. Como a rede Tor se relaciona com o resultado

Em uma conexão convencional, o serviço acessado normalmente observa o endereço IP público utilizado pela conexão do cliente.

No Tor Browser, o tráfego é encaminhado pela rede Tor, que utiliza múltiplos relays para transportar a comunicação. Para um serviço externo, o endereço observado pode ser o do **nó de saída**, em vez do endereço público original do cliente.

A atividade demonstra essa diferença de forma prática através da consulta do endereço IP.

O resultado não significa que o Tor torne toda atividade automaticamente anônima ou que elimine todas as possibilidades de identificação. A proteção depende também da forma como o navegador e os serviços são utilizados.

## 7. Conceitos praticados

### Tor

O **Tor (The Onion Router)** é uma rede projetada para aumentar a privacidade das comunicações por meio do encaminhamento do tráfego através de uma sequência de relays.

### Tor Browser

É um navegador configurado para utilizar a rede Tor, buscando reduzir determinadas formas de rastreamento e exposição da origem da conexão.

### Tor Exit Node

O **nó de saída** é o ponto da rede Tor responsável por encaminhar o tráfego para a Internet convencional.

É o endereço associado a esse nó que pode ser observado pelo serviço de destino.

### IP público

O endereço IP público é utilizado para identificar a origem de uma conexão na Internet. A comparação realizada na atividade demonstra que o endereço observado por um serviço pode variar conforme o caminho utilizado para estabelecer a conexão.

### Privacidade na Internet

A atividade demonstra, de forma prática, como diferentes mecanismos de conexão podem alterar as informações de rede observadas externamente.

## 8. Resultado

A atividade permitiu:

1. Instalar e iniciar o Tor Browser através do `torbrowser-launcher`;
2. Estabelecer uma conexão com a rede Tor;
3. Realizar uma navegação simples através do Tor Browser;
4. Consultar o endereço IP observado externamente;
5. Identificar um Tor Exit Node no resultado;
6. Comparar o endereço apresentado pelo Tor Browser com uma conexão convencional;
7. Compreender a função dos nós de saída e o impacto da rede Tor na visibilidade do endereço IP.

A principal observação foi a diferença entre o endereço IP apresentado pelo Tor Browser e o endereço apresentado pelo Firefox convencional durante o laboratório.

## Evidência

A evidência da atividade está no PDF geral das Aulas 7 e 8:

[Ver evidências — Aulas 7 e 8](https://github.com/Joaopmsitz/hackers-do-bem-labs/blob/main/fundamental/modulo-02/aula-07-08/evidencias.pdf)

**Print registrado:** etapa 7 da atividade, conforme solicitado pelo roteiro.
