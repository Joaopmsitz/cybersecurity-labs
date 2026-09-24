# Atividade 2.7 — Explorando os eventos de sistema com o Logcheck no Linux

## Objetivo

Utilizar o **Logcheck** para analisar eventos registrados no sistema Linux, observando principalmente eventos relacionados a autenticação, serviços de rede e mensagens de erro.

A atividade demonstra como uma ferramenta de monitoramento pode filtrar e apresentar eventos relevantes dos logs do sistema, auxiliando na identificação de comportamentos que podem exigir investigação.

## Ambiente

* Kali Linux
* Terminal
* Logcheck
* Arquivos de log do sistema
* Sessão administrativa `root`

## 1. Executando o Logcheck

O Logcheck pode ser executado utilizando o usuário de serviço `logcheck`:

```bash
sudo -u logcheck logcheck -o -t
```

A execução apresentou eventos relacionados ao `sudo`, ao cliente DHCP e ao serviço XRDP:

```text
This email is sent by logcheck. If you no longer wish to receive
such mail, you can either uninstall the logcheck package or modify
its configuration file (/etc/logcheck/logcheck.conf).

Security Events for sudo
=-=-=-=-=-=-=-=-=-=-=-=-
2024-02-08T18:04:35.855136-03:00 ip-192-168-98-40 sudo: pam_unix(sudo-i:session): session closed for user root
fev 08 18:04:35 kali sudo[5209]: pam_unix(sudo-i:session): session closed for user root

System Events
=-=-=-=-=-=-=
2024-02-08T18:02:53.499503-03:00 ip-192-168-98-40 dhclient[495]: XMT: Solicit on eth0, interval 108860ms.
2024-02-08T18:04:42.410794-03:00 ip-192-168-98-40 dhclient[495]: XMT: Solicit on eth0, interval 125740ms.
2024-02-08T18:04:50.231955-03:00 ip-192-168-98-40 xrdp-chansrv[1991]: [ERROR] clipboard_event_selection_request: unknown target text/plain;charset=utf-8
2024-02-08T18:04:50.239116-03:00 ip-192-168-98-40 xrdp-chansrv[1991]: [ERROR] clipboard_event_selection_request: unknown target text/plain;charset=utf-8
fev 08 18:02:53 kali dhclient[495]: XMT: Solicit on eth0, interval 108860ms.
fev 08 18:04:42 kali dhclient[495]: XMT: Solicit on eth0, interval 125740ms.
fev 08 18:04:50 kali xrdp-chansrv[1991]: [ERROR] clipboard_event_selection_request: unknown target text/plain;charset=utf-8
fev 08 18:04:50 kali xrdp-chansrv[1991]: [ERROR] clipboard_event_selection_request: unknown target text/plain;charset=utf-8
```

### Interpretação

Os eventos apresentados podem ser divididos em três grupos principais:

* **sudo:** registra o encerramento de uma sessão administrativa do usuário `root`.
* **dhclient:** registra solicitações relacionadas à obtenção/configuração de endereço IP na interface `eth0`.
* **xrdp-chansrv:** apresenta erros relacionados a eventos de transferência de conteúdo da área de transferência durante a sessão remota.

A presença de uma mensagem `[ERROR]` no log não significa, isoladamente, que houve um incidente de segurança. O evento precisa ser analisado dentro do contexto do sistema e da atividade que estava sendo realizada.

## 2. Alterando a configuração do Logcheck

Para alterar a configuração, foi aberta uma sessão administrativa:

```bash
sudo -i
```

Em seguida, o arquivo de configuração foi aberto:

```bash
nano /etc/logcheck/logcheck.conf
```

A configuração utilizada na atividade definiu o nível de relatório como `workstation`:

```text
REPORTLEVEL="workstation"

SENDMAILTO="<endereço de e-mail configurado no laboratório>"

MAILASATTACH=1
```

### REPORTLEVEL

O `REPORTLEVEL` determina o nível de filtragem utilizado pelo Logcheck.

Os principais níveis apresentados na atividade são:

* **server:** nível padrão, voltado para sistemas que executam serviços e daemons.
* **paranoid:** nível mais restritivo e detalhado, podendo gerar uma quantidade maior de eventos.
* **workstation:** direcionado a estações de trabalho, utilizando filtros adequados a esse tipo de sistema.

Nesta atividade, foi utilizado:

```text
REPORTLEVEL="workstation"
```

O endereço de e-mail utilizado no laboratório não é reproduzido neste documento.

## 3. Executando novamente o Logcheck

Após a alteração da configuração, o Logcheck foi executado novamente:

```bash
sudo -u logcheck logcheck -o -t
```

A nova execução apresentou eventos adicionais relacionados às sessões `sudo`, além dos eventos de rede e XRDP:

```text
This email is sent by logcheck. If you no longer wish to receive
such mail, you can either uninstall the logcheck package or modify
its configuration file (/etc/logcheck/logcheck.conf).

Security Events for sudo
=-=-=-=-=-=-=-=-=-=-=-=-
2024-02-08T18:04:35.855136-03:00 ip-192-168-98-40 sudo: pam_unix(sudo-i:session): session closed for user root
2024-02-08T18:12:31.367745-03:00 ip-192-168-98-40 sudo: pam_unix(sudo-i:session): session opened for user root(uid=0) by (uid=1001)
2024-02-08T18:16:03.554902-03:00 ip-192-168-98-40 sudo: pam_unix(sudo-i:session): session closed for user root
fev 08 18:12:31 kali sudo[8454]: pam_unix(sudo-i:session): session opened for user root(uid=0) by (uid=1001)
fev 08 18:16:03 kali sudo[8454]: pam_unix(sudo-i:session): session closed for user root

System Events
=-=-=-=-=-=-=
2024-02-08T18:02:53.499503-03:00 ip-192-168-98-40 dhclient[495]: XMT: Solicit on eth0, interval 108860ms.
2024-02-08T18:04:42.410794-03:00 ip-192-168-98-40 dhclient[495]: XMT: Solicit on eth0, interval 125740ms.
2024-02-08T18:04:50.231955-03:00 ip-192-168-98-40 xrdp-chansrv[1991]: [ERROR] clipboard_event_selection_request: unknown target text/plain;charset=utf-8
2024-02-08T18:04:50.239116-03:00 ip-192-168-98-40 xrdp-chansrv[1991]: [ERROR] clipboard_event_selection_request: unknown target text/plain;charset=utf-8
2024-02-08T18:06:48.170853-03:00 ip-192-168-98-40 dhclient[495]: XMT: Solicit on eth0, interval 114710ms.
2024-02-08T18:08:42.922879-03:00 ip-192-168-98-40 dhclient[495]: XMT: Solicit on eth0, interval 112740ms.
2024-02-08T18:10:35.763167-03:00 ip-192-168-98-40 dhclient[495]: XMT: Solicit on eth0, interval 129930ms.
2024-02-08T18:12:45.793377-03:00 ip-192-168-98-40 dhclient[495]: XMT: Solicit on eth0, interval 129080ms.
2024-02-08T18:13:47.104704-03:00 ip-192-168-98-40 xrdp-chansrv[1991]: [ERROR] clipboard_event_selection_request: unknown target text/plain;charset=utf-8
2024-02-08T18:13:47.111981-03:00 ip-192-168-98-40 xrdp-chansrv[1991]: [ERROR] clipboard_event_selection_request: unknown target text/plain;charset=utf-8
2024-02-08T18:14:54.973652-03:00 ip-192-168-98-40 dhclient[495]: XMT: Solicit on eth0, interval 114690ms.
fev 08 18:08:42 kali dhclient[495]: XMT: Solicit on eth0, interval 112740ms.
fev 08 18:10:35 kali dhclient[495]: XMT: Solicit on eth0, interval 129930ms.
fev 08 18:12:45 kali dhclient[495]: XMT: Solicit on eth0, interval 129080ms.
fev 08 18:13:47 kali xrdp-chansrv[1991]: [ERROR] clipboard_event_selection_request: unknown target text/plain;charset=utf-8
fev 08 18:13:47 kali xrdp-chansrv[1991]: [ERROR] clipboard_event_selection_request: unknown target text/plain;charset=utf-8
fev 08 18:14:54 kali dhclient[495]: XMT: Solicit on eth0, interval 114690ms.
```

## 4. Análise dos eventos

A segunda execução permite observar com mais detalhes o comportamento do sistema durante o período analisado.

### Eventos de autenticação

Os registros do `sudo` mostram a abertura e o encerramento de uma sessão administrativa:

```text
sudo: pam_unix(sudo-i:session): session opened for user root(uid=0) by (uid=1001)
sudo: pam_unix(sudo-i:session): session closed for user root
```

Esses eventos são importantes em uma análise de segurança porque permitem identificar quando privilégios administrativos foram utilizados.

### Eventos DHCP

As mensagens:

```text
dhclient[495]: XMT: Solicit on eth0
```

indicam que o cliente DHCP estava realizando solicitações na interface de rede `eth0`.

Esse tipo de evento é esperado em determinadas situações de configuração ou renovação de endereço IP.

### Eventos XRDP

Foram identificadas mensagens:

```text
xrdp-chansrv[1991]: [ERROR] clipboard_event_selection_request: unknown target text/plain;charset=utf-8
```

Elas estão relacionadas ao componente responsável pelos canais da sessão XRDP e indicam uma solicitação de área de transferência que não foi reconhecida pelo serviço.

No contexto do laboratório, esses eventos foram observados durante o uso da sessão remota e não foram tratados isoladamente como um incidente.

## 5. Conceitos praticados

### Logcheck

Ferramenta utilizada para analisar e filtrar eventos de logs, destacando mensagens que podem ser relevantes para a administração e segurança do sistema.

### Análise de logs

A análise de logs é uma atividade importante para identificar:

* autenticações e uso de privilégios;
* alterações e atividades administrativas;
* eventos de rede;
* erros de serviços;
* comportamentos fora do padrão;
* possíveis indicadores de comprometimento.

### Monitoramento e detecção

O Logcheck funciona como um mecanismo de apoio à detecção, reduzindo a necessidade de analisar manualmente todos os eventos registrados pelo sistema.

### `sudo` e PAM

Os eventos relacionados ao `sudo` utilizam o **PAM (Pluggable Authentication Modules)** para registrar informações sobre sessões administrativas.

### DHCP

O `dhclient` é responsável por interagir com o serviço DHCP para obter ou renovar configurações de rede.

### XRDP

O XRDP permite acesso remoto a ambientes gráficos Linux. Seus componentes também podem registrar eventos relacionados à sessão, incluindo problemas com recursos como a área de transferência.

## 6. Resultado

A atividade demonstrou o uso do Logcheck para filtrar e apresentar eventos do sistema Linux.

Foi possível observar:

1. Eventos de abertura e encerramento de sessões administrativas;
2. Solicitações DHCP na interface de rede;
3. Mensagens de erro do serviço XRDP;
4. A influência do `REPORTLEVEL` na filtragem dos eventos;
5. A importância de interpretar cada evento considerando o contexto do sistema.

O exercício reforçou a importância da análise de logs como parte do monitoramento e da identificação de possíveis eventos de segurança.

## Evidência

A evidência da atividade está no PDF geral das Aulas 7 e 8:

[Ver evidências — Aulas 7 e 8](https://github.com/Joaopmsitz/hackers-do-bem-labs/blob/main/fundamental/modulo-02/aula-07-08/evidencias.pdf)

**Print registrado:** etapa 5 da atividade, conforme solicitado pelo roteiro.
