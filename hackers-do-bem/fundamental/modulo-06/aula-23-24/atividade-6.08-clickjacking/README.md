# Atividade 6.8 — Conhecendo o Ataque Clickjacking

## Objetivo

Nesta atividade foi estudado o conceito de **Clickjacking**, uma técnica na qual elementos de uma página podem ser posicionados sobre uma interface aparentemente legítima para induzir o usuário a clicar em um elemento diferente daquele que acredita estar selecionando.

O exercício foi realizado em ambiente de laboratório, utilizando uma página HTML local. O objetivo foi observar o comportamento de um `iframe`, alterar sua transparência com CSS e verificar as proteções existentes no navegador.

> O laboratório não envolveu a tentativa de realizar ações em uma conta real ou explorar um usuário real.

---

## Ambiente

* **Sistema:** Kali Linux
* **Acesso:** RDP
* **IP da máquina:** `192.168.98.40`
* **Usuário:** `aluno`
* **Navegador:** Firefox 128.14.0esr
* **Diretório de trabalho:** `/home/aluno/Documentos`

> As credenciais utilizadas no laboratório não são registradas neste documento.

---

## 1. Conceito de Clickjacking

No cenário apresentado pelo laboratório, uma página maliciosa poderia apresentar ao visitante um conteúdo aparentemente inofensivo, enquanto um `iframe` transparente contendo outro site seria posicionado sobre uma área clicável.

A ideia conceitual é:

```text
Usuário
   │
   │ acredita clicar em:
   ▼
[ Botão visível ]
   │
   │
   └──────► elemento sobreposto por um iframe
                         │
                         ▼
                  conteúdo incorporado
```

Com o uso de CSS, o `iframe` pode ser posicionado sobre outros elementos da página e sua opacidade pode ser alterada.

---

## 2. Criando a página HTML

Foi utilizado o Mousepad para criar uma página HTML de laboratório.

O conteúdo utilizado foi:

```html
<!doctype html>
<html>

<head>
  <meta charset="UTF-8">
</head>

<body>

  <style>
    iframe {
      width: 400px;
      height: 100px;
      position: absolute;
      top: 5px;
      left: -14px;
      opacity: 1;
      z-index: 1;
    }
  </style>

  <div>Click to get rich now:</div>

  <!-- The url from the victim site -->
  <iframe src="https://www.facebook.com"></iframe>

  <button>Click here!</button>

  <div>...And you're cool (I'm a cool hacker actually)!</div>

</body>
</html>
```

O arquivo foi salvo como:

```text
/home/aluno/Documentos/teste.html
```

Ao salvar pelo Mousepad, foi selecionada a opção para salvar o arquivo como **All files**, mantendo a extensão `.html`.

---

## 3. Abrindo a página no navegador

O arquivo `teste.html` foi localizado através do Thunar e aberto no Firefox.

Na configuração inicial:

```css
opacity: 1;
```

o conteúdo incorporado pelo `iframe` permanecia visível, apresentando inicialmente um retângulo preto na página.

---

## 4. Tornando o iframe transparente

O valor:

```css
opacity: 1;
```

foi alterado para:

```css
opacity: 0;
```

Após salvar o arquivo e recarregar a página, o conteúdo do `iframe` deixou de ficar visualmente visível, enquanto o texto e o botão da página continuaram sendo apresentados.

Isso demonstra como a propriedade CSS `opacity` pode alterar a visibilidade de um elemento sem necessariamente removê-lo da página.

---

## 5. Testando a interação

Foi realizado um teste clicando no botão apresentado na página.

O navegador não permitiu que o clique fosse utilizado para realizar a ação esperada através do conteúdo incorporado.

O Firefox apresentou proteção contra esse comportamento, impedindo que o cenário do laboratório funcionasse como uma exploração real.

---

## 6. Testando opacidade parcial

O valor da propriedade foi alterado novamente:

```css
opacity: 0;
```

para:

```css
opacity: 0.5;
```

Após salvar e recarregar a página, o elemento incorporado passou a ficar parcialmente visível.

Mesmo nessa configuração, a proteção do Firefox continuou impedindo o comportamento esperado pelo laboratório.

---

## 7. Tornando o iframe praticamente invisível

A opacidade foi alterada novamente:

```css
opacity: 0.5;
```

para:

```css
opacity: 0.03;
```

Após salvar e recarregar a página, o `iframe` ficou praticamente invisível, enquanto os elementos da página continuaram aparentando ser uma interface normal.

Essa etapa demonstra visualmente uma das características exploradas pelo conceito de Clickjacking: um elemento sobreposto pode permanecer presente na estrutura da página mesmo quando praticamente não é percebido visualmente pelo usuário.

---

## 8. Proteção do navegador

Durante os testes, o Firefox impediu que o cenário funcionasse como uma exploração efetiva.

Isso é importante porque o funcionamento de Clickjacking não depende apenas do HTML e do CSS utilizados. Os navegadores modernos possuem mecanismos de proteção que podem impedir determinados comportamentos de conteúdo incorporado e navegação entre frames.

---

## 9. Exibindo somente o conteúdo do frame

Para observar o conteúdo incorporado diretamente, foi utilizado o menu de contexto do Firefox:

```text
Clique com o botão direito
        ↓
This Frame
        ↓
Show Only This Frame
```

Essa ação fez com que o navegador exibisse somente o conteúdo do frame selecionado.

**Este é o passo utilizado como evidência da atividade.**

---

## Conceitos envolvidos

### Clickjacking

Clickjacking é uma técnica baseada na sobreposição de elementos de uma página para fazer com que a interação do usuário ocorra sobre um elemento diferente daquele que ele acredita estar selecionando.

Um cenário típico pode utilizar:

* `iframe`;
* posicionamento absoluto com CSS;
* controle de transparência;
* elementos sobrepostos;
* uma interface visualmente enganosa.

### `iframe`

O elemento:

```html
<iframe src="https://www.facebook.com"></iframe>
```

permite incorporar conteúdo externo dentro de uma página HTML.

No laboratório, ele foi utilizado para demonstrar o conceito de sobreposição de conteúdo.

### `opacity`

A propriedade CSS:

```css
opacity
```

controla a transparência de um elemento.

Exemplos utilizados na atividade:

```css
opacity: 1;
```

```css
opacity: 0.5;
```

```css
opacity: 0.03;
```

Quanto menor o valor, mais transparente fica o elemento.

### `z-index`

A propriedade:

```css
z-index: 1;
```

define a posição do elemento no eixo de profundidade em relação a outros elementos posicionados.

Em conjunto com `position: absolute`, ela pode ser utilizada para posicionar elementos sobre outros conteúdos.

---

## Resultado

A atividade permitiu observar, em um ambiente controlado:

1. a estrutura básica de uma página que utiliza `iframe`;
2. o posicionamento de um conteúdo incorporado;
3. o efeito da propriedade CSS `opacity`;
4. o comportamento de um elemento praticamente invisível;
5. a atuação das proteções do Firefox;
6. a visualização isolada do conteúdo de um frame.

O teste não resultou em uma exploração funcional contra o site incorporado. O navegador bloqueou o comportamento esperado pelo laboratório, demonstrando a importância das proteções implementadas nos navegadores modernos.

---

## Limpeza

Após a conclusão dos testes, o Firefox, Mousepad e Thunar foram fechados.

No terminal, o arquivo criado para o laboratório foi removido:

```bash
sudo -i
cd /home/aluno/Documentos
rm teste.html
```

A sessão RDP foi encerrada e a máquina virtual utilizada no laboratório foi interrompida.

---

## Evidência

A evidência desta atividade corresponde ao **passo 9**, mostrando a opção **This Frame → Show Only This Frame** utilizada para visualizar o conteúdo do frame isoladamente.

[**Evidências — Módulo 6 / Aulas 3 e 4**](../evidencias.pdf)
