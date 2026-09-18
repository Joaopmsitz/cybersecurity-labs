# Atividade 2.9 — Navegação na Deep Web via Tor Browser

## Objetivo

Utilizar o **Tor Browser** para compreender, em um ambiente educacional controlado, o acesso a serviços disponíveis na rede Tor, observando a estrutura dos endereços `.onion` e a diferença entre a Web convencional e os serviços acessíveis exclusivamente através da rede Tor.

A atividade foi realizada seguindo as orientações do laboratório, com foco na compreensão da tecnologia e sem interação com conteúdo ilegal ou serviços destinados a atividades criminosas.

## Ambiente

* Kali Linux
* Firefox
* Tor Browser
* Rede Tor
* Serviços `.onion`
* The Hidden Wiki

## 1. Acessando a referência na Web convencional

Inicialmente, foi utilizado o Firefox para acessar:

```text
https://thehiddenwiki.org
```

A página apresentou uma relação de endereços e serviços associados à rede Tor.

Os endereços `.onion` são diferentes dos domínios convencionais utilizados na Internet. Eles identificam serviços que são acessados através da rede Tor.

## 2. Identificando endereços `.onion`

Na página consultada foi possível observar uma lista de endereços terminados em:

```text
.onion
```

Esses endereços são utilizados para identificar **Onion Services**, também conhecidos como serviços ocultos ou serviços onion.

Diferentemente de um domínio convencional, um endereço `.onion` é resolvido e acessado dentro da própria rede Tor.

## 3. Acessando um Onion Service pelo Tor Browser

Em seguida, o Tor Browser foi utilizado para acessar um dos serviços `.onion` apresentados no material do curso.

O acesso foi realizado através de uma nova aba do Tor Browser, já conectado à rede Tor.

O endereço utilizado no laboratório era um serviço onion fornecido pelo próprio roteiro da atividade. Por segurança e para evitar transformar o material do curso em um diretório de serviços onion ativos, o endereço não é reproduzido neste README.

## 4. Resultado observado

O serviço acessado apresentou a página **The Hidden Wiki**, com informações sobre a própria infraestrutura do serviço:

```text
The Hidden Wiki

The Original Hidden Wiki - Only @ [endereço onion do laboratório]

Update 07.2020: The old short v2 .onion hidden service links will no longer work after october 2021. We will list only v3 .onion's in the future.
```

A mensagem também fazia referência à migração dos endereços antigos **Onion v2** para o formato **Onion v3**.

O resultado demonstrou que o Tor Browser conseguiu estabelecer comunicação com um serviço disponível através da rede Tor.

## 5. Serviços Onion

O laboratório também apresentou outros endereços `.onion` como exemplos de serviços disponíveis na rede.

A existência de um endereço `.onion` não significa, por si só, que o conteúdo disponibilizado pelo serviço seja legítimo ou seguro. Por esse motivo, a atividade foi limitada ao escopo educacional definido pelo curso.

Não foram realizadas interações com mercados ilegais, serviços criminosos, distribuição de malware ou qualquer outro conteúdo ilícito.

## 6. Deep Web e rede Tor

O termo **Deep Web** normalmente se refere a conteúdos que não são indexados ou facilmente encontrados pelos mecanismos tradicionais de busca. Isso inclui diversos serviços legítimos, como sistemas privados, bancos de dados, páginas autenticadas e outros recursos que não são públicos para mecanismos de busca.

A rede Tor é uma tecnologia diferente desse conceito. Ela fornece uma infraestrutura de comunicação voltada à privacidade e também permite a existência de serviços `.onion`.

Portanto:

* **Deep Web:** conteúdo que não está necessariamente indexado pelos mecanismos de busca convencionais;
* **Dark Web:** conjunto de serviços que dependem de tecnologias específicas para serem acessados;
* **Tor:** rede que permite comunicação através de múltiplos relays e também hospeda Onion Services;
* **`.onion`:** domínio utilizado para identificar serviços dentro da rede Tor.

Esses conceitos são relacionados, mas não são sinônimos.

## 7. Onion Services

Os Onion Services são serviços projetados para serem acessados através da rede Tor.

Entre suas características está a utilização de endereços `.onion` e a comunicação através da infraestrutura Tor, sem depender da publicação do serviço da mesma forma que um servidor Web convencional.

O modelo permite que tanto o usuário quanto o serviço tenham características de privacidade diferentes das observadas em uma conexão Web tradicional.

## 8. Considerações de segurança

O acesso à rede Tor não significa que todos os serviços disponíveis nela sejam seguros.

Durante uma atividade prática envolvendo Onion Services, é importante:

* permanecer dentro do escopo autorizado do laboratório;
* evitar serviços de procedência desconhecida;
* não realizar downloads suspeitos;
* não executar arquivos obtidos de fontes não confiáveis;
* não fornecer informações pessoais;
* não interagir com serviços ilegais;
* encerrar a sessão ao concluir o exercício.

Nesta atividade, a navegação foi utilizada para compreender a tecnologia e a estrutura dos serviços `.onion`.

## 9. Resultado

A atividade permitiu:

1. Acessar uma referência relacionada à rede Tor através da Web convencional;
2. Identificar a estrutura de endereços `.onion`;
3. Utilizar o Tor Browser para acessar um Onion Service;
4. Observar uma página do The Hidden Wiki;
5. Identificar a referência aos formatos Onion v2 e Onion v3;
6. Compreender a relação entre Tor, Deep Web, Dark Web e Onion Services;
7. Praticar navegação controlada dentro de um ambiente educacional.

O principal aprendizado foi compreender que os serviços `.onion` fazem parte da infraestrutura da rede Tor e possuem características diferentes dos sites convencionais da Web.

## Evidência

A evidência da atividade está no PDF geral das Aulas 7 e 8:

[Ver evidências — Aulas 7 e 8](https://github.com/Joaopmsitz/hackers-do-bem-labs/blob/main/fundamental/modulo-02/aula-07-08/evidencias.pdf)

**Print registrado:** etapa 4 da atividade, conforme solicitado pelo roteiro.
