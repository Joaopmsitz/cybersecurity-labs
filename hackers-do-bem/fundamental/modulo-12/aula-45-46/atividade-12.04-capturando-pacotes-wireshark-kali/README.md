# Atividade 12.4 — Capturando Pacotes com Wireshark no Kali Linux

## Objetivo

Realizar uma captura de tráfego de rede no **Kali Linux** utilizando o **Wireshark**, acessando um site HTTPS durante a captura e analisando os pacotes transmitidos.

Ao final, será utilizado o recurso **Follow → TCP Stream** para visualizar o conteúdo de um fluxo TCP e observar o efeito da criptografia TLS sobre os dados da aplicação.

---

## Ambiente

* **Sistema operacional:** Kali Linux
* **Ferramenta:** Wireshark
* **Interface de rede:** `eth0`
* **Endereço IP:** `192.168.98.40`
* **Site acessado:** `https://esr.rnp.br/`
* **Protocolo analisado:** TCP/TLS
* **Porta:** `443`

---

## 1. Acessando o Kali Linux

O Kali Linux foi iniciado e acessado através de RDP.

Após o acesso, foi aberto um terminal e obtido acesso administrativo com:

```bash id="k7v3pm"
sudo -i
```

---

## 2. Verificando as interfaces de rede

Antes de iniciar a captura, foi executado:

```bash id="m4x8qr"
ifconfig
```

Saída:

```text id="oqr4oq"
docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        ether 02:42:b8:59:44:51  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 6 overruns 0  carrier 0  collisions 0

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9001
        inet 192.168.98.40  netmask 255.255.255.0  broadcast 192.168.98.255
        inet6 fe80::104d:70ff:fef0:ab8b  prefixlen 64  scopeid 0x20<link>
        ether 12:4d:70:f0:ab:8b  txqueuelen 1000  (Ethernet)
        RX packets 37230  bytes 2104203 (2.0 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 71233  bytes 386912752 (368.9 MiB)
        TX errors 0  dropped 0  overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<link>
        loop  txqueuelen 1000  (Ethernet)
        RX packets 15  bytes 1157 (1.1 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 15  bytes 1157 (1.1 KiB)
        TX errors 0  dropped 0  overruns 0  carrier 0  collisions 0
```

A interface utilizada para a captura é a `eth0`, que possui o endereço IPv4 `192.168.98.40`.

---

## 3. Abrindo o Wireshark

O aplicativo **Wireshark** foi aberto pelo menu de aplicativos do Kali Linux.

Na tela inicial foram apresentadas as interfaces de rede disponíveis para captura.

---

## 4. Iniciando a captura na interface `eth0`

Na lista de interfaces do Wireshark, foi localizada:

```text id="b8n5vc"
eth0
```

Foi realizado um duplo clique sobre a interface `eth0` para iniciar a captura de pacotes.

A partir desse momento, o Wireshark passou a monitorar o tráfego que atravessava a interface.

---

## 5. Gerando tráfego HTTPS

Com a captura em andamento, foi aberto o Firefox.

No navegador, foi acessado:

```text id="p6r2xm"
https://esr.rnp.br/
```

A página foi carregada enquanto o Wireshark registrava os pacotes de rede gerados pela comunicação.

Após aguardar alguns instantes para gerar tráfego suficiente, o Firefox foi fechado.

---

## 6. Encerrando a captura

Após retornar ao Wireshark, a captura foi interrompida utilizando o botão de parada, representado pelo quadrado vermelho na barra de ferramentas.

Os pacotes capturados permaneceram disponíveis para análise na janela principal do Wireshark.

---

## 7. Entendendo as informações dos pacotes

Na lista de pacotes do Wireshark, foram observadas colunas utilizadas para identificar e analisar o tráfego:

* **Time:** momento em que o pacote foi capturado.
* **Source:** endereço de origem do pacote.
* **Destination:** endereço de destino.
* **Protocol:** protocolo identificado no pacote.
* **Length:** tamanho do pacote.
* **Info:** informações adicionais sobre o conteúdo ou operação observada.

Essas informações permitem analisar a comunicação entre os diferentes hosts envolvidos na conexão.

---

## 8. Filtrando o tráfego HTTPS

Para concentrar a análise no tráfego TCP associado à porta HTTPS, foi utilizado o filtro:

```text id="c3w7pk"
tcp.port == 443
```

Esse filtro faz com que o Wireshark exiba pacotes TCP cuja porta de origem ou destino seja `443`, normalmente utilizada para conexões HTTPS.

Na captura, foi possível observar o tráfego relacionado à comunicação segura estabelecida pelo navegador.

Dependendo da conexão e da versão negociada, o Wireshark pode identificar protocolos TLS, como **TLS 1.2** ou **TLS 1.3**.

---

## 9. Seguindo o fluxo TCP

Após localizar um pacote pertencente à comunicação HTTPS, foi realizado um clique com o botão direito sobre o pacote.

No menu de contexto, foi selecionado:

```text id="r8v2qm"
Follow → TCP Stream
```

O Wireshark então abriu uma janela mostrando os dados associados ao fluxo TCP selecionado.

---

## 10. Analisando o conteúdo do TCP Stream

O conteúdo apresentado na janela **Follow TCP Stream** não apareceu como texto legível.

Isso ocorre porque a comunicação realizada através de HTTPS utiliza **TLS para proteger os dados da camada de aplicação**.

Durante uma conexão HTTPS, é possível observar informações de rede como endereços, portas, tamanho dos pacotes e outros metadados. Entretanto, o conteúdo da aplicação é protegido pela criptografia da sessão TLS.

Portanto, ao seguir o fluxo TCP sem possuir as chaves necessárias para descriptografar a sessão, o conteúdo transmitido não é apresentado como texto legível.

Em uma comunicação HTTP sem criptografia, o conteúdo da aplicação poderia aparecer de forma muito mais facilmente interpretável no fluxo TCP.

---

## 11. Evidência

O print obrigatório corresponde ao **passo 11**, mostrando a janela **Follow TCP Stream** após a captura de tráfego HTTPS.

**Frase obrigatória antes do print:**

> **Print da atividade 12.4:** janela `Follow TCP Stream` do Wireshark após a captura de tráfego HTTPS, exibindo o conteúdo do fluxo de forma não legível devido à criptografia da conexão TLS.

[**Evidências — Módulo 12 / Aulas 45 e 46**](../evidencias.pdf)

---

## 12. Encerramento

Após a análise do fluxo TCP, a janela foi fechada.

O Wireshark foi encerrado sem salvar a captura em arquivo, conforme orientado na atividade.

---

## Conceitos

* **Wireshark:** analisador de protocolos utilizado para capturar e examinar tráfego de rede.
* **TCP:** protocolo orientado à conexão utilizado para transporte dos dados.
* **HTTPS:** comunicação HTTP protegida por TLS.
* **TLS:** protocolo criptográfico utilizado para proteger a comunicação.
* **TCP Stream:** conjunto de dados pertencentes a um fluxo TCP específico.
* **Filtro de captura/análise:** recurso utilizado para restringir os pacotes exibidos no Wireshark.

## Fluxo

```text id="u4c9sx"
Kali Linux
    ↓
Wireshark
    ↓
Captura em eth0
    ↓
Acesso ao esr.rnp.br
    ↓
Tráfego HTTPS / TCP 443
    ↓
Filtro tcp.port == 443
    ↓
Follow → TCP Stream
    ↓
Dados protegidos por TLS
```

## Resultado

Foi realizada uma captura de tráfego na interface `eth0` do Kali Linux durante o acesso a um site HTTPS. O tráfego TCP da porta `443` foi filtrado e um fluxo foi analisado através do recurso **Follow TCP Stream**.

O conteúdo da aplicação não foi apresentado de forma legível porque a comunicação HTTPS utiliza TLS para proteger os dados transmitidos.
