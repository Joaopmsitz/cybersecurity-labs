# Atividade 1.5 — Taskwarrior

## Objetivo

Praticar o gerenciamento de tarefas pelo terminal utilizando o **Taskwarrior**, criando tarefas, adicionando prioridade, definindo prazo e marcando tarefas como concluídas.

## Ambiente

* Kali Linux
* Terminal
* Taskwarrior

## Procedimento

### 1. Preparação do Taskwarrior

Primeiro, foi acessado o modo administrador e configurado o diretório utilizado pelo Taskwarrior:

```bash
sudo -i
mkdir -p ~/.task
echo 'data.location=~/.task' > ~/.taskrc
```

A opção `data.location` define o local onde o Taskwarrior armazenará seus dados.

### 2. Criação das tarefas

Foram criadas três tarefas:

```bash
task add Comprar leite
task add Comprar cafe
task add Comprar salgados
```

Em seguida, foi utilizado o comando abaixo para visualizar as tarefas:

```bash
task list
```

As tarefas receberam identificadores numéricos, que foram utilizados posteriormente para modificá-las.

### 3. Adicionando prioridade

A tarefa de número 2 recebeu a tag `urgent`:

```bash
task 2 modify +urgent
```

Depois, a lista foi consultada novamente:

```bash
task list
```

A tag `+urgent` adiciona uma característica à tarefa que pode influenciar sua organização e seu nível de urgência dentro do Taskwarrior.

### 4. Definindo uma data de vencimento

A tarefa de número 3 recebeu uma data de vencimento:

```bash
task 3 modify due:2036-12-31
```

Depois, foi executado:

```bash
task list
```

A tarefa passou a apresentar a data definida como prazo.

### 5. Concluindo uma tarefa

A tarefa de número 1 foi marcada como concluída:

```bash
task 1 done
```

Por fim, a lista foi consultada novamente:

```bash
task list
```

A tarefa concluída deixou de aparecer entre as tarefas pendentes.

## Comandos utilizados

```bash
sudo -i
mkdir -p ~/.task
echo 'data.location=~/.task' > ~/.taskrc

task add Comprar leite
task add Comprar cafe
task add Comprar salgados

task list

task 2 modify +urgent
task list

task 3 modify due:2036-12-31
task list

task 1 done
task list
```

## Resultado

Foi possível utilizar o Taskwarrior para criar e organizar tarefas diretamente pelo terminal, aplicando diferentes recursos de gerenciamento:

* Criação de tarefas;
* Visualização da lista;
* Adição de prioridade/urgência;
* Definição de prazo;
* Conclusão de tarefas.

## Conceitos praticados

* Gerenciamento de tarefas via terminal
* Linux
* Taskwarrior
* Tags de tarefas
* Prioridade e urgência
* Datas de vencimento
* Controle de tarefas concluídas

## Evidência

A execução da atividade foi registrada no PDF de evidências da Aula 01–02.

[Ver evidências — Aula 01–02](https://github.com/Joaopmsitz/hackers-do-bem-labs/blob/main/fundamental/modulo-01/aula-01-02/evidencias.pdf)
