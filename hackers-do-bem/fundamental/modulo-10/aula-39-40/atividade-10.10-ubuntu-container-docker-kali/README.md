# Atividade 10.10 — Ubuntu em um Container Docker no Kali Linux

## Objetivo

Utilizar o **Docker** no Kali Linux para baixar uma imagem Ubuntu, criar e executar containers, acessar um shell interativo e acompanhar informações de execução utilizando os comandos `docker top` e `docker stats`.

Ao final, o container utilizado na atividade foi parado e os containers inativos foram removidos.

---

## Ambiente

* **Sistema:** Kali GNU/Linux Rolling
* **Container:** Ubuntu
* **Runtime:** Docker
* **Container principal:** `MeuContainer`
* **Terminal:** Bash

---

## 1. Verificando o Docker

Foi obtido acesso administrativo no terminal:

```bash
sudo -i
```

Em seguida, foi executado:

```bash
docker
```

O comando apresentou a tela de ajuda do Docker:

```text
Usage:  docker [OPTIONS] COMMAND

A self-sufficient runtime for containers

Common Commands:
  run         Create and run a new container from an image
  exec        Execute a command in a running container
  ps          List containers
  build       Build an image from a Dockerfile
  pull        Download an image from a registry
  push        Upload an image to a registry
  images      List images
  login       Authenticate to a registry
  logout      Log out from a registry
  search      Search Docker Hub for images
  version     Show the Docker version information
  info        Display system-wide information

Management Commands:
  builder     Manage builds and cache
  buildx*     Manage Docker Buildx
  container   Manage containers
  image       Manage images
  manifest    Manage Docker image manifests and manifest lists
  network     Manage networks
  plugin      Manage plugins
  system      Manage Docker
  trust       Manage trust on Docker images
  volume      Manage volumes

Swarm Commands:
  swarm       Manage Swarm

Commands:
  attach      Attach local standard input, output, and error streams to a running container
  commit      Create new image from a container
  cp          Copy files/folders...
  diff...
  events...
  export...
  history...
  import...
  inspect...
  kill...
  load...
  logs...
  pause...
  port...
  rename...
  restart...
  rm...
  rmi...
  save...
  start...
  stats...
  stop...
  top...
  unpause...
  update...
  wait...

Global Options:
      --config string      Location of client config files (default "/root/.docker")
  -c, --context string     Name of the context...
  -D, --debug...
  -H, --host list...
  -l, --log-level...
      --tls...
...
Run 'docker COMMAND --help' for more information.
```

A saída confirma a disponibilidade dos principais comandos utilizados para gerenciamento de imagens e containers.

---

## 2. Verificando as imagens disponíveis

Foi executado:

```bash
docker images
```

Inicialmente, não havia imagens listadas:

```text
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
```

---

## 3. Baixando a imagem Ubuntu

Foi utilizada a imagem oficial do Ubuntu através do comando:

```bash
docker pull ubuntu
```

A imagem foi baixada do Docker Hub:

```text
Using default tag: latest
latest: Pulling from library/ubuntu
20043066d3d5: Pull complete
Digest: sha256:c35e29c9450151419d9448b0fd75374fec4fff364a27f176fb458d472dfc9e54
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:latest
```

A tag `latest` foi utilizada por padrão.

---

## 4. Verificando a imagem baixada

Foi executado novamente:

```bash
docker images
```

A imagem Ubuntu passou a aparecer na listagem:

```text
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
ubuntu       latest    ca2b0f26964c   10 days ago   77.9MB
```

Dessa forma, a imagem `ubuntu:latest` estava disponível localmente para criação de containers.

---

## 5. Executando um container Ubuntu

Foi executado:

```bash
docker run ubuntu
```

Esse comando cria e inicia um container utilizando a imagem Ubuntu.

Como não foi especificado um processo interativo ou um processo persistente, o container encerra sua execução após concluir o processo padrão.

---

## 6. Criando um container interativo

Para manter um shell interativo, foi utilizado:

```bash
docker run --name MeuContainer -it ubuntu bash
```

O container recebeu o nome:

```text
MeuContainer
```

O terminal passou a apresentar:

```text
root@2c6580444ba4:/#
```

A partir desse momento, os comandos executados nesse terminal estavam sendo executados dentro do ambiente do container Ubuntu.

---

## 7. Explorando o sistema de arquivos do container

Dentro do container, foi executado:

```bash
ls
```

A saída apresentada foi:

```text
bin boot dev etc home lib lib32 lib64 libx32 media mnt opt proc root run sbin srv sys tmp usr var
```

Essa estrutura apresenta os principais diretórios presentes no sistema de arquivos do Ubuntu dentro do container.

---

## 8. Verificando o processo do container

Em um segundo terminal do Kali, foi obtido acesso administrativo:

```bash
sudo -i
```

Em seguida, foi executado:

```bash
docker top MeuContainer
```

A saída apresentou o processo em execução no container:

```text
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
root                40370               40342               0                   16:09               pts/0               00:00:00            bash
```

O comando `docker top` permite visualizar os processos associados a um container em execução.

Nesse caso, o processo principal observado era o `bash`.

---

## 9. Verificando o consumo de recursos

Ainda no segundo terminal, foi executado:

```bash
docker stats
```

A saída apresentada foi:

```text
CONTAINER ID   NAME           CPU %     MEM USAGE / LIMIT   MEM %     NET I/O       BLOCK I/O   PIDS
2c6580444ba4   MeuContainer   0.01%     916KiB / 1.926GiB   0.05%     1.16kB / 0B   0B / 0B     1
```

O comando `docker stats` apresenta métricas de utilização dos containers em execução.

No momento da verificação, o `MeuContainer` apresentava:

* **CPU:** 0.01%;
* **Memória:** 916 KiB de 1.926 GiB;
* **Uso de memória:** 0.05%;
* **PIDs:** 1.

---

## 10. Encerrando o shell do container

Após concluir a verificação, o segundo terminal foi fechado.

No primeiro terminal, dentro do container, foi executado:

```bash
exit
```

A saída foi:

```text
root@2c6580444ba4:/# exit
exit
```

Com isso, o shell interativo foi encerrado.

---

## 11. Parando o container

O container `MeuContainer` foi parado através do comando:

```bash
docker stop MeuContainer
```

O Docker retornou:

```text
docker stop MeuContainer
MeuContainer
```

### Evidência — Passo 12

**Frase obrigatória antes do print:**

> **Print da atividade 10.10:** execução do comando `docker stop MeuContainer`, confirmando a parada do container `MeuContainer`.

[**Evidências — Módulo 10 / Aulas 39 e 40**](../evidencias.pdf)

---

## 12. Removendo containers inativos

Após parar o container, foi executado:

```bash
docker container prune
```

O Docker solicitou confirmação:

```text
WARNING! This will remove all stopped containers.
Are you sure you want to continue? [y/N] y
```

Após a confirmação, os containers parados foram removidos:

```text
Deleted Containers:
2c6580444ba45dcc6ca52159ef009a52f255b63b612cd2a2075ba0a7c1e5f690
fab9028be5b9edd1614c872ee8cb59877b70e51c1dee2c1f28969a08ea24fd81

Total reclaimed space: 8B
```

O comando `docker container prune` remove containers que não estão mais em execução, liberando os recursos associados a eles.

---

## Conceitos

* **Docker:** plataforma para criação e execução de containers.
* **Imagem:** modelo utilizado como base para criar um container.
* **Container:** instância executável de uma imagem.
* **`docker top`:** mostra os processos associados ao container.
* **`docker stats`:** apresenta métricas de utilização de recursos.
* **`docker stop`:** interrompe um container em execução.

## Fluxo da atividade

```text
Verificar Docker
      ↓
Baixar imagem Ubuntu
      ↓
Criar container
      ↓
Acessar shell
      ↓
Verificar processos
      ↓
Verificar recursos
      ↓
Sair do container
      ↓
Parar MeuContainer
      ↓
Remover containers inativos
```

## Resultado

Foi utilizada uma imagem Ubuntu no Docker para criar e executar o container `MeuContainer`. Foram verificados seus processos e consumo de recursos com `docker top` e `docker stats`, seguido da parada e limpeza dos containers inativos.
