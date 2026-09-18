# Atividade 1.10 — Adversarial Machine Learning

## Objetivo

Demonstrar o conceito de **Adversarial Machine Learning** utilizando uma aplicação interativa de reconhecimento de imagens.

A atividade compara uma imagem original com uma versão modificada por uma **perturbação adversarial**, observando como uma alteração aparentemente pequena pode fazer uma rede neural classificar a imagem de maneira diferente.

## Ambiente

* Navegador web
* Aplicação Adversarial.js
* Modelo de reconhecimento de placas de trânsito
* Dataset GTSRB (German Traffic Sign Recognition Benchmark)

## Procedimento

### 1. Acesso à aplicação

A atividade foi realizada através da aplicação:

https://kennysong.github.io/adversarial.js/

A ferramenta permite visualizar, de forma interativa, o funcionamento de um modelo de classificação de imagens e demonstrar o efeito de exemplos adversariais.

### 2. Seleção do modelo

Na aplicação, foi selecionado o modelo:

```text
GTSRB (street sign recognition)
```

Esse modelo é utilizado para reconhecimento e classificação de placas de trânsito.

### 3. Seleção da imagem original

Foi selecionada uma imagem correspondente a uma placa de:

```text
STOP
```

A imagem original foi utilizada como referência para comparar a classificação antes e depois da geração do exemplo adversarial.

### 4. Classificação da imagem original

Com a imagem original selecionada, foi executada a opção:

```text
RUN NEURAL NETWORK
```

A rede neural analisou a imagem e realizou a classificação correspondente à placa apresentada.

O resultado foi compatível com a imagem original, identificando corretamente a placa de STOP.

### 5. Geração do exemplo adversarial

Em seguida, foi utilizada a opção:

```text
GENERATE
```

A aplicação gerou uma nova versão da imagem contendo uma **perturbação adversarial**.

Essa alteração é construída de maneira a interferir no processo de classificação do modelo, mesmo mantendo a imagem visualmente semelhante à original.

### 6. Classificação da imagem adversarial

Após a geração da imagem modificada, foi executada novamente a opção:

```text
RUN NEURAL NETWORK
```

Dessa vez, o modelo produziu uma classificação diferente da classificação obtida para a imagem original.

A rede neural deixou de reconhecer corretamente a placa de STOP, demonstrando o efeito da perturbação adversarial sobre o modelo.

### 7. Comparação dos resultados

A atividade permitiu comparar diretamente os dois casos:

| Imagem             | Resultado                              |
| ------------------ | -------------------------------------- |
| Imagem original    | Classificação correta da placa de STOP |
| Imagem adversarial | Classificação incorreta pelo modelo    |

O resultado demonstra que uma modificação pequena e direcionada pode alterar a saída de um modelo de Machine Learning.

### 8. Encerramento

Após a comparação dos resultados, a atividade foi concluída e a aplicação foi encerrada.

## Comandos utilizados

Não foram utilizados comandos de terminal nesta atividade.

Todo o procedimento foi realizado através da interface web da aplicação:

https://kennysong.github.io/adversarial.js/

## Interpretação

Um **exemplo adversarial** é uma entrada modificada de forma intencional para provocar uma classificação incorreta em um modelo de Machine Learning.

Nesse experimento, a imagem original da placa de STOP foi corretamente classificada pela rede neural. Após a aplicação de uma perturbação adversarial, uma nova classificação foi produzida pelo mesmo modelo.

O ponto principal da atividade é demonstrar que o desempenho de um modelo de reconhecimento não depende apenas da aparência visual percebida por uma pessoa. Alterações específicas nos dados de entrada podem explorar características utilizadas pelo modelo durante a classificação.

Em aplicações reais, esse tipo de comportamento é relevante para a segurança de sistemas que utilizam Machine Learning, principalmente em cenários nos quais decisões automatizadas dependem de imagens ou outros dados de entrada.

## Resultado

Foi possível demonstrar, de forma controlada, a diferença entre a classificação de uma imagem original e de uma imagem contendo uma perturbação adversarial.

A imagem original da placa de STOP foi reconhecida corretamente. Após a geração do exemplo adversarial, o modelo apresentou uma classificação incorreta.

O experimento permitiu visualizar na prática o conceito de **adversarial example** e sua relação com a robustez de modelos de Machine Learning.

## Conceitos praticados

* Machine Learning
* Inteligência Artificial
* Adversarial Machine Learning
* Adversarial Examples
* Perturbações adversariais
* Classificação de imagens
* Redes neurais
* GTSRB
* Robustez de modelos
* Segurança em Inteligência Artificial

## Evidência

A execução da atividade foi registrada no PDF de evidências da Aula 03–04.

[Ver evidências — Aula 03–04](https://github.com/Joaopmsitz/hackers-do-bem-labs/blob/main/fundamental/modulo-01/aula-03-04/evidencias.pdf)
