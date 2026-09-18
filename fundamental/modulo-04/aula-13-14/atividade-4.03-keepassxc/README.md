# Atividade 4.3 — Gerenciamento de Credenciais com KeePassXC

## Objetivo

Utilizar o **KeePassXC** para criar um banco de dados protegido por senha e armazenar uma credencial de teste.

A atividade teve como objetivo compreender o funcionamento de um gerenciador de senhas, incluindo a criação de um banco de dados no formato `.kdbx`, definição do algoritmo de criptografia e armazenamento de credenciais.

---

## Ambiente

* **Sistema:** Kali Linux
* **Aplicação:** KeePassXC
* **Banco de dados:** `Senhas.kdbx`
* **Local utilizado:** `/home/aluno/Documentos/`
* **Algoritmo selecionado:** AES 256-bit

---

## 1. Inicialização do KeePassXC

A aplicação foi iniciada a partir do terminal:

```bash
keepassxc
```

O KeePassXC foi aberto normalmente com o usuário comum do laboratório.

A atividade não exigiu privilégios administrativos para a utilização do aplicativo.

---

## 2. Criação do banco de dados

Na tela inicial do KeePassXC, foi selecionada a opção para criar um novo banco de dados.

Foi definido:

```text
Nome do banco: Pessoal
```

Durante a configuração avançada da criptografia, foi selecionado o algoritmo:

```text
AES 256-bit
```

O banco de dados foi então protegido por uma senha definida especificamente para o laboratório.

> A senha utilizada durante o exercício não é reproduzida neste README.

O KeePassXC apresentou o aviso relacionado à utilização de uma senha considerada fraca. Como se tratava de um ambiente acadêmico controlado, a credencial definida pelo roteiro foi utilizada apenas para a execução da atividade.

---

## 3. Salvando o banco de dados

O banco de dados foi salvo no diretório:

```text
/home/aluno/Documentos/
```

com o nome:

```text
Senhas.kdbx
```

O formato `.kdbx` é o formato de banco de dados utilizado pelo KeePassXC.

Após a criação, o banco de dados ficou disponível para armazenamento das credenciais.

---

## 4. Criação de uma credencial de teste

Dentro do banco `Pessoal`, foi criada uma nova entrada para representar uma conta de serviço.

Os campos utilizados no laboratório foram:

| Campo   | Valor utilizado           |
| ------- | ------------------------- |
| Título  | `Netflix`                 |
| Usuário | Credencial de teste       |
| Senha   | Credencial de teste       |
| URL     | `https://www.netflix.com` |

A entrada foi salva dentro do banco de dados.

O objetivo foi demonstrar como o KeePassXC organiza diferentes informações de autenticação em uma única base protegida.

As credenciais utilizadas no exercício são de laboratório e não são reproduzidas neste README.

---

## 5. Visualização da credencial armazenada

Após salvar a entrada, ela foi selecionada no KeePassXC para verificar as informações armazenadas.

Nesse momento foi possível visualizar a entrada:

```text
Netflix
```

e seus respectivos campos de autenticação.

A atividade demonstra que o KeePassXC funciona como um repositório centralizado para credenciais, permitindo armazenar usuários, senhas e URLs dentro de um banco de dados protegido.

---

## 6. Exclusão da entrada de teste

Depois da validação, a entrada utilizada no exercício foi excluída do banco de dados.

Essa etapa evita manter uma credencial de teste desnecessária dentro do arquivo da atividade.

O banco de dados foi posteriormente fechado.

---

## 7. Remoção do banco de dados

Com o KeePassXC encerrado, foi acessado o diretório utilizado para salvar o banco:

```bash
cd /home/aluno/Documentos
```

Em seguida, foi verificado o conteúdo do diretório:

```bash
ls
```

O arquivo criado durante a atividade foi identificado:

```text
Senhas.kdbx
```

O arquivo foi então removido:

```bash
rm Senhas.kdbx
```

A remoção foi realizada somente após a conclusão da atividade.

---

## Conceitos praticados

### KeePassXC

O KeePassXC é um gerenciador de senhas que permite armazenar credenciais em um banco de dados protegido.

### Banco KDBX

O `.kdbx` é o formato utilizado pelo KeePassXC para armazenar o banco de dados de credenciais.

### AES-256

O **AES (Advanced Encryption Standard)** é um algoritmo de criptografia simétrica. No laboratório foi selecionada a variante com chave de **256 bits**.

### Gerenciamento de credenciais

Um gerenciador de senhas permite centralizar credenciais em vez de armazená-las em arquivos de texto ou reutilizá-las diretamente em diferentes serviços.

---

## Resultado

A atividade permitiu criar e utilizar um banco de dados de credenciais no KeePassXC.

Foi possível:

* iniciar o KeePassXC;
* criar um banco de dados;
* selecionar o algoritmo AES 256-bit;
* proteger o banco com uma senha;
* criar uma entrada de credencial;
* visualizar os dados armazenados;
* excluir a entrada de teste;
* remover o arquivo `.kdbx` ao final do laboratório.

O exercício demonstrou, na prática, como um gerenciador de senhas pode organizar credenciais de forma centralizada e protegida.

---

## Evidência

[**Evidências — Módulo 4 / Aulas 1 e 2**](../evidencias.pdf)

**Print registrado:** etapa 10 da atividade, conforme solicitado pelo roteiro, mostrando a credencial de teste armazenada no KeePassXC.
