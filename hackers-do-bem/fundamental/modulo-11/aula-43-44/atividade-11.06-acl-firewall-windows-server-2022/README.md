# Atividade 11.6 — Explorando o ACL no Firewall do Windows Server 2022

## Objetivo

Explorar as configurações avançadas do **Firewall do Windows Server 2022**, observando as regras de entrada e saída, regras de segurança de conexão e as opções de monitoramento relacionadas ao firewall e às associações de segurança utilizadas em conexões protegidas.

---

## Ambiente

* **Sistema:** Windows Server 2022
* **Acesso:** RDP
* **Ferramenta:** Windows Defender Firewall with Advanced Security
* **Endereço do servidor:** `192.168.98.30`

---

## 1. Acessando o Windows Server 2022

O Windows Server 2022 foi inicializado e acessado por RDP.

A máquina utilizada no laboratório possui o endereço:

```text id="j8w4qn"
192.168.98.30
```

Após o acesso ao sistema, foi aberta a pesquisa do Windows através de:

```text
Type here to search
```

Foi pesquisado:

```text id="m5k2rx"
Windows Defender Firewall with Advanced Security
```

Em seguida, foi aberta a ferramenta **Windows Defender Firewall with Advanced Security**.

---

## 2. Explorando as Inbound Rules

No painel esquerdo da ferramenta, foi selecionada a opção:

```text id="v7p3cs"
Inbound Rules
```

As **Inbound Rules** são responsáveis pelo controle do tráfego que chega ao computador ou servidor.

As regras podem permitir ou bloquear conexões de entrada com base em diferentes critérios, como:

* aplicativo;
* serviço;
* protocolo;
* porta;
* endereço IP de origem;
* endereço IP de destino;
* perfil de rede;
* ação definida pela regra.

Por exemplo, uma regra pode permitir que determinado programa aceite conexões provenientes de outros dispositivos da rede.

---

## 3. Explorando as Outbound Rules

No painel esquerdo, foi selecionada:

```text id="q6d9kf"
Outbound Rules
```

As **Outbound Rules** controlam o tráfego que sai do computador ou servidor em direção a outros dispositivos, servidores ou à Internet.

Assim como nas regras de entrada, é possível criar regras baseadas em diferentes critérios para permitir ou bloquear conexões de saída.

Um exemplo de aplicação é utilizar uma regra para impedir que determinado aplicativo ou serviço realize conexões com um destino específico.

---

## 4. Explorando as Connection Security Rules

Em seguida, foi selecionada:

```text id="n3x7mb"
Connection Security Rules
```

As **Connection Security Rules** são utilizadas para definir requisitos de segurança para determinadas comunicações entre dispositivos.

Elas podem ser utilizadas em cenários que envolvem:

* VPN;
* IPsec;
* autenticação;
* criptografia;
* proteção da comunicação entre hosts.

Diferentemente das regras tradicionais de firewall, que controlam diretamente o tráfego permitido ou bloqueado, as regras de segurança de conexão podem definir os requisitos utilizados para estabelecer uma comunicação protegida.

---

## 5. Explorando o Monitoring

No painel esquerdo, foi selecionada:

```text id="r8c4vz"
Monitoring
```

A seção **Monitoring** permite acompanhar informações relacionadas ao funcionamento do firewall e às regras de segurança configuradas no sistema.

Essa área é útil para verificar o estado das configurações e observar informações relacionadas às conexões e políticas aplicadas.

---

## 6. Explorando o Firewall dentro de Monitoring

O campo `Monitoring` foi expandido e a opção:

```text id="x2m6pa"
Firewall
```

foi selecionada.

Essa seção permite visualizar informações relacionadas ao funcionamento das regras do firewall.

Entre as informações que podem ser observadas estão:

### Conexões permitidas

Mostra conexões que foram autorizadas pelas regras de entrada ou saída do firewall.

### Conexões bloqueadas

Apresenta conexões que foram impedidas por regras de firewall.

### Regras de firewall em vigor

Permite visualizar as regras que estão ativas e sendo aplicadas ao sistema.

### Detalhes das conexões

Ao selecionar uma conexão, podem ser apresentados dados relacionados à comunicação, como:

* aplicativo envolvido;
* endereço IP;
* porta;
* direção do tráfego;
* outros parâmetros da conexão.

---

## 7. Explorando Connection Security Rules no Monitoring

Dentro de `Monitoring`, foi expandida a opção:

```text id="a9f5jk"
Connection Security Rules
```

Essa seção permite visualizar informações relacionadas às conexões que utilizam regras de segurança.

Dependendo do ambiente e da existência de conexões configuradas, essa área pode estar vazia.

Entre as informações que podem ser observadas estão:

### Conexões estabelecidas

Apresenta conexões de segurança que foram estabelecidas de acordo com as regras configuradas.

### Conexões descartadas

Mostra tentativas de conexão que foram descartadas ou bloqueadas pelas regras de segurança.

### Detalhes das conexões

Quando existe uma conexão disponível, podem ser observadas informações como:

* dispositivos envolvidos;
* redes envolvidas;
* método de autenticação;
* estado da conexão;
* parâmetros de segurança utilizados.

---

## 8. Acessando Security Associations

Dentro da seção `Monitoring`, foi expandido:

```text id="f4w7nc"
Security Associations
```

Essa seção apresenta informações relacionadas às **Associações de Segurança (Security Associations)** utilizadas em comunicações protegidas.

Foram observadas as opções relacionadas aos modos de negociação utilizados pelo IPsec:

```text
Security Associations
├── Main Mode
└── Quick Mode
```

---

## 9. Explorando o Main Mode

Dentro de:

```text id="z8k3qp"
Monitoring
→ Security Associations
→ Main Mode
```

foi acessada a seção **Main Mode**.

O **Main Mode** está relacionado ao processo de negociação inicial utilizado pelo **IKE (Internet Key Exchange)** para estabelecer parâmetros de segurança entre os dispositivos.

Durante essa negociação, podem ocorrer etapas relacionadas a:

### Autenticação

Os dispositivos envolvidos realizam a autenticação de suas identidades para estabelecer uma relação de confiança.

### Negociação de parâmetros

Os dispositivos negociam os parâmetros criptográficos que serão utilizados na comunicação segura.

Entre esses parâmetros podem estar:

* algoritmos de criptografia;
* algoritmos de autenticação;
* parâmetros de troca de chaves;
* tempo de vida das associações.

### Estabelecimento da associação

Após a negociação e autenticação, os parâmetros necessários para uma comunicação protegida são estabelecidos.

A seção **Main Mode** permite acompanhar informações relacionadas a essas negociações, incluindo dados dos dispositivos envolvidos, parâmetros de segurança e estado das associações.

### Evidência — Passo 9

**Frase obrigatória antes do print:**

> **Print da atividade 11.6:** tela de monitoramento das **Security Associations → Main Mode** do Firewall do Windows Server 2022, exibindo as informações relacionadas às negociações de segurança realizadas pelo IKE.

[**Evidências — Módulo 11 / Aulas 43 e 44**](../evidencias.pdf)

> **Observação:** dependendo do ambiente do laboratório, a lista de associações pode estar vazia caso não exista uma negociação IPsec ativa. O importante nesta etapa é apresentar a tela solicitada pelo roteiro.

---

## 10. Explorando o Quick Mode

Depois do registro da evidência, foi acessado:

```text id="s6v2md"
Monitoring
→ Security Associations
→ Quick Mode
```

O **Quick Mode** é utilizado após a negociação inicial do Main Mode para estabelecer ou atualizar associações de segurança específicas para o tráfego protegido.

Entre suas funções estão:

### Renovação de chaves

Permite estabelecer novas chaves de criptografia e autenticação quando necessário.

### Definição do tráfego protegido

São definidos parâmetros relacionados ao tráfego que deverá utilizar a proteção da associação de segurança.

Isso pode envolver informações como:

* endereços IP;
* portas;
* protocolos;
* escopo da comunicação.

### Integridade da comunicação

Os parâmetros negociados também podem incluir mecanismos utilizados para garantir a integridade dos dados transmitidos.

A seção **Quick Mode** permite acompanhar informações relacionadas a essas negociações e às associações de segurança estabelecidas nesse estágio.

---

## 11. Encerrando a atividade

Após explorar as diferentes seções do Firewall do Windows Server 2022, todas as janelas foram fechadas.

---

## Conceitos

* **ACL:** conjunto de regras utilizado para controlar o acesso e o tráfego de rede.
* **Firewall:** mecanismo que controla conexões de rede de acordo com regras configuradas.
* **Inbound Rules:** regras aplicadas ao tráfego recebido.
* **Outbound Rules:** regras aplicadas ao tráfego de saída.
* **Connection Security Rules:** regras utilizadas para estabelecer requisitos de segurança para comunicações.
* **IPsec:** conjunto de protocolos utilizado para proteger comunicações IP.
* **IKE:** protocolo utilizado para negociar parâmetros e estabelecer associações de segurança.
* **Main Mode:** etapa de negociação inicial de parâmetros de segurança.
* **Quick Mode:** etapa utilizada para estabelecer ou atualizar associações de segurança específicas para o tráfego.

## Fluxo da atividade

```text id="c9p5xr"
Firewall Advanced Security
          ↓
Inbound Rules
          ↓
Outbound Rules
          ↓
Connection Security Rules
          ↓
Monitoring
          ↓
Firewall
          ↓
Connection Security Rules
          ↓
Security Associations
     ↙             ↘
Main Mode       Quick Mode
```

## Resultado

Foram exploradas as principais seções do **Windows Defender Firewall with Advanced Security**, incluindo regras de entrada e saída, regras de segurança de conexão e o monitoramento de associações de segurança nos modos **Main Mode** e **Quick Mode**.
