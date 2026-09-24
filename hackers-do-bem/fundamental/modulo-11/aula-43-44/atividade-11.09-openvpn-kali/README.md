# Atividade 11.9 — Usando OpenVPN no Kali Linux

## Objetivo

Configurar e estabelecer uma conexão **VPN utilizando OpenVPN** no Kali Linux, verificar a alteração do endereço IP público durante a conexão e comparar o endereço apresentado antes e depois da desconexão.

---

## Ambiente

* **Sistema:** Kali GNU/Linux
* **Ferramenta:** OpenVPN
* **Serviço utilizado no laboratório:** VPNBook
* **Arquivo de configuração:** `vpnbook-ca149-tcp80.ovpn`
* **Servidor VPN utilizado:** CA149
* **Protocolo:** TCP
* **Porta:** `80`

> **Observação:** as credenciais utilizadas para autenticação no VPNBook não são registradas neste documento.

---

## 1. Obtendo o arquivo de configuração

Foi acessado o site do VPNBook:

```text
https://www.vpnbook.com/
```

Na página do serviço, foi selecionado um servidor OpenVPN gratuito diferente dos servidores localizados nos Estados Unidos.

Para esta atividade, foi utilizado o servidor:

```text
CA149
```

Foi realizado o download do pacote de configuração do OpenVPN.

O arquivo compactado foi extraído no diretório:

```text
/home/aluno/Downloads/
```

Após a extração, foi criado o diretório:

```text
/home/aluno/Downloads/vpnbook-openvpn-ca149/
```

Nesse diretório estavam os arquivos necessários para realizar a conexão com o servidor VPN.

---

## 2. Obtendo acesso administrativo

O Terminal do Kali Linux foi aberto e foi obtido acesso administrativo com:

```bash id="n6w3kp"
sudo -i
```

---

## 3. Acessando os arquivos de configuração

Foi acessado o diretório contendo os arquivos extraídos:

```bash id="r8m5vq"
cd /home/aluno/Downloads/vpnbook-openvpn-ca149/
```

O arquivo de configuração utilizado na atividade foi:

```text id="c4x7nz"
vpnbook-ca149-tcp80.ovpn
```

---

## 4. Iniciando a conexão OpenVPN

A conexão foi iniciada com:

```bash id="w9k2fp"
openvpn --config vpnbook-ca149-tcp80.ovpn
```

Durante a inicialização, o OpenVPN apresentou alguns avisos relacionados à configuração utilizada pelo arquivo.

A saída inicial foi:

```text id="p7m4xc"
2025-12-05 23:19:51 DEPRECATED: --persist-key option ignored. Keys are now always persisted across restarts.
2025-12-05 23:19:51 WARNING: Compression for receiving enabled. Compression has been used in the past to break encryption. Compression support is deprecated and we recommend to disable it completely.
2025-12-05 23:19:51 DEPRECATED OPTION: --cipher set to 'AES-256-CBC' but missing in --data-ciphers (DEFAULT). OpenVPN ignores --cipher for cipher negotiations.
2025-12-05 23:19:51 Note: '--allow-compression' is not set to 'no', disabling data channel offload.
2025-12-05 23:19:51 OpenVPN 2.7_rc2 x86_64-pc-linux-gnu [SSL (OpenSSL)] [LZO] [LZ4] [EPOLL] [PKCS11] [MH/PKTINFO] [AEAD] [DCO]
2025-12-05 23:19:51 library versions: OpenSSL 3.5.4 30 Sep 2025, LZO 2.10
2025-12-05 23:19:51 DCO version: N/A
Enter Auth Username: vpnbook
Enter Auth Password: •••••••
```

A autenticação foi realizada utilizando as credenciais fornecidas pelo VPNBook.

A saída seguinte apresentou um aviso importante sobre a verificação do certificado do servidor:

```text id="q5v8mb"
2025-12-05 23:20:12 WARNING: No server certificate verification method has been enabled.  See http://openvpn.net/howto.html#mitm for more info.
```

Esse aviso indica que a configuração utilizada no laboratório não possuía um método de verificação do certificado do servidor habilitado.

Em seguida, o OpenVPN estabeleceu a conexão com o servidor remoto:

```text id="x3k6rp"
2025-12-05 23:20:12 TCP/UDP: Preserving recently used remote address: [AF_INET]144.217.253.149:80
2025-12-05 23:20:12 Socket Buffers: R=[131072->131072] S=[16384->16384]
```

Após a negociação, foram configurados o DNS e o canal de dados:

```text id="m8v2cq"
2025-12-05 23:20:13 /usr/libexec/openvpn/dns-updown
setting DNS using resolv.conf file
2025-12-05 23:20:13 dns up command exited with status 0
2025-12-05 23:20:13 Data Channel: cipher 'AES-256-GCM', peer-id: 11, compression: 'lzo'
2025-12-05 23:20:13 Timers: ping 5, ping-restart 30
2025-12-05 23:20:13 Protocol options: protocol-flags cc-exit tls-ekm dyn-tls-crypt
```

Também foram adicionadas rotas para direcionar o tráfego através da VPN:

```text id="v5n9xt"
2025-12-05 23:20:15 net_route_v4_add: 144.217.253.149/32 via 192.168.98.1 dev [NULL] table 0 metric -1
2025-12-05 23:20:15 net_route_v4_add: 0.0.0.0/1 via 10.12.0.57 dev [NULL] table 0 metric -1
2025-12-05 23:20:15 net_route_v4_add: 128.0.0.0/1 via 10.12.0.57 dev [NULL] table 0 metric -1
2025-12-05 23:20:15 net_route_v4_add: 10.12.0.1/32 via 10.12.0.57 dev [NULL] table 0 metric -1
2025-12-05 23:20:15 Initialization Sequence Completed
```

A mensagem:

```text id="k4p7cz"
Initialization Sequence Completed
```

indica que a sequência de inicialização do OpenVPN foi concluída e a conexão VPN estava estabelecida.

---

## 5. Verificando o endereço IP público

Com a VPN ativa, foi aberto o navegador e acessado:

```text
https://whatismyipaddress.com/
```

O endereço IP público apresentado durante a conexão VPN foi:

```text id="z6m3qw"
My IP Address is:
IPv4: ? 144.217.253.149
IPv6: ? Not detected

My IP Information:

ISP: OVH Hosting Inc.
Services: Network Sharing Device
City: Trois-Rivières
Region: Quebec
Country: Canada
```

O resultado demonstra que, durante a conexão com o servidor VPN, o serviço de consulta identificou o endereço público:

```text id="f8c2mp"
144.217.253.149
```

e associou o endereço à infraestrutura da OVH no Canadá.

### Evidência — Passo 13

**Frase obrigatória antes do print:**

> **Print da atividade 11.9:** página de consulta de IP após o estabelecimento da conexão OpenVPN, mostrando o endereço IP público e as informações de localização associadas à saída da VPN.

[**Evidências — Módulo 11 / Aulas 43 e 44**](../evidencias.pdf)

---

## 6. Encerrando a conexão VPN

Após a verificação do endereço IP, o processo do OpenVPN foi interrompido utilizando:

```text id="b5r9vx"
Ctrl + C
```

Isso encerrou a conexão com o servidor VPN.

---

## 7. Verificando novamente o endereço IP

Depois de desconectar da VPN, a página:

```text
https://whatismyipaddress.com/
```

foi atualizada.

O resultado apresentado no ambiente do laboratório foi:

```text id="j7c4zn"
My IP Address is:
IPv4: ? 18.234.103.188
IPv6: ? Not detected

My IP Information:

ISP: Amazon Technologies Inc.
City: Ashburn
Region: Virginia
Country: United States
```

Nesse momento, o endereço público apresentado foi:

```text id="q2m8vk"
18.234.103.188
```

O resultado foi diferente do endereço apresentado durante a conexão VPN.

---

## 8. Removendo os arquivos do laboratório

Após finalizar os testes, foi acessado o diretório de downloads:

```bash id="c9x5mp"
cd /home/aluno/Downloads
```

Os arquivos existentes foram listados:

```bash id="n4v7qs"
ls
```

Resultado:

```text id="t8k2fz"
cacert.der vpnbook-openvpn-ca149 vpnbook-openvpn-ca149.zip
```

Os arquivos utilizados na atividade foram então removidos:

```bash id="m6p3wr"
rm -r *
```

O sistema solicitou confirmação para a remoção:

```text id="y5q9kc"
zsh: sure you want to delete all 2 files in /home/aluno/Downloads [yn]? y
```

A confirmação foi realizada com:

```text id="v3n8mx"
y
```

---

## Observações de segurança

Durante a inicialização da VPN, o OpenVPN apresentou alguns avisos que são relevantes para a análise da atividade.

### Compressão habilitada

O log apresentou:

```text
WARNING: Compression for receiving enabled.
```

O próprio OpenVPN informa que a compressão possui histórico de problemas relacionados a ataques contra canais criptografados e recomenda desabilitá-la.

### Verificação do certificado

Também foi apresentado:

```text
WARNING: No server certificate verification method has been enabled.
```

Isso significa que a configuração utilizada no laboratório não habilitou um método de verificação do certificado do servidor.

### Cipher configurado no arquivo

O OpenVPN também informou:

```text
DEPRECATED OPTION: --cipher set to 'AES-256-CBC' but missing in --data-ciphers (DEFAULT).
```

O aviso indica que a opção `--cipher` presente no arquivo utiliza uma configuração considerada obsoleta para a negociação atual.

Apesar dos avisos, o log mostrou que o canal de dados estabelecido utilizou:

```text
AES-256-GCM
```

Esses avisos são importantes porque demonstram que uma conexão VPN estabelecida não significa, por si só, que toda a configuração esteja seguindo as recomendações de segurança mais atuais.

---

## Conceitos

* **VPN:** cria um túnel de comunicação entre o cliente e um servidor VPN.
* **OpenVPN:** software utilizado para estabelecer conexões VPN.
* **IP público:** endereço utilizado para identificar a saída do dispositivo na Internet.
* **Roteamento:** determina por quais caminhos os pacotes devem ser enviados.
* **DNS:** resolução de nomes utilizada durante a conexão.
* **AES-256-GCM:** algoritmo/modo criptográfico utilizado pelo canal de dados observado no laboratório.
* **`Initialization Sequence Completed`:** mensagem que indica a conclusão da inicialização da conexão OpenVPN.

## Fluxo da atividade

```text id="r7m4cx"
Baixar configuração VPNBook
          ↓
Executar OpenVPN
          ↓
Autenticar
          ↓
Estabelecer túnel VPN
          ↓
Configurar DNS e rotas
          ↓
Initialization Sequence Completed
          ↓
Consultar IP público
          ↓
IP da saída VPN
          ↓
Ctrl + C
          ↓
Desconectar VPN
          ↓
Consultar IP novamente
          ↓
IP da saída original
```

## Resultado

Foi estabelecida uma conexão OpenVPN utilizando o servidor CA149 do VPNBook. Durante a conexão, o endereço público observado foi `144.217.253.149`, associado à saída da VPN no Canadá. Após a desconexão, o ambiente voltou a apresentar o endereço público `18.234.103.188`.

A atividade também permitiu observar avisos de segurança presentes na configuração utilizada pelo laboratório, incluindo compressão habilitada, ausência de método de verificação do certificado do servidor e uso de uma opção `--cipher` obsoleta.
