# Atividade 4.4 — John the Ripper: Ataque de Dicionário

## Objetivo

Utilizar o **John the Ripper** para realizar uma auditoria offline de uma credencial em ambiente controlado, utilizando um hash de senha armazenado no sistema e um ataque baseado em dicionário.

A atividade demonstra como senhas fracas podem ser recuperadas quando um atacante obtém acesso aos hashes armazenados, sem necessidade de realizar tentativas diretamente contra o serviço de autenticação.

---

## Ambiente

* **Sistema:** Kali Linux
* **Ferramentas:** John the Ripper, OpenSSL
* **Arquivo de teste:** `credencial.txt`
* **Arquivo do sistema analisado:** `/etc/shadow`
* **Tipo de hash utilizado no laboratório:** `crypt`
* **Método:** ataque de dicionário

> Todo o procedimento foi realizado exclusivamente com uma conta criada para o laboratório.

---

## 1. Acesso ao `/etc/shadow`

Inicialmente, foi obtido acesso administrativo:

```bash id="p7k2ma"
sudo -i
```

Em seguida, o arquivo `/etc/shadow` foi consultado:

```bash id="r3x8vc"
cat /etc/shadow
```

O `/etc/shadow` contém informações relacionadas às credenciais das contas locais, incluindo hashes de senha e parâmetros de envelhecimento das credenciais.

No laboratório, a saída continha entradas para diferentes usuários do sistema.

Por segurança, os hashes reais do ambiente não são reproduzidos neste README.

Uma entrada possui uma estrutura semelhante a:

```text id="k6n1zw"
usuario:<hash>:...
```

O arquivo é protegido porque o acesso aos hashes permite a realização de ataques offline de quebra de senha.

---

## 2. Criação de um usuário de teste

Foi criado um usuário exclusivamente para a atividade utilizando `useradd` e `openssl`:

```bash id="v9c4qt"
useradd -p $(openssl passwd -1 [senha-de-teste]) teste1
```

No laboratório, a opção `-1` do OpenSSL foi utilizada para gerar um hash no formato **MD5-crypt**, identificado pelo prefixo `$1$`.

> A senha de teste utilizada pelo roteiro não é reproduzida neste README.

Após a criação, a conta `teste1` passou a possuir uma entrada correspondente no `/etc/shadow`.

---

## 3. Identificação da entrada da conta de teste

Foi consultado novamente o arquivo:

```bash id="n5w2df"
cat /etc/shadow
```

A entrada correspondente ao usuário criado apresentava um formato semelhante a:

```text id="x4q8pb"
teste1:<hash-do-laboratório>:...
```

O objetivo dessa etapa foi identificar somente a linha correspondente à conta de teste.

O hash foi utilizado como entrada para o processo de auditoria offline.

---

## 4. Criação do arquivo de credencial

A linha correspondente ao usuário `teste1` foi copiada para um arquivo separado:

```text id="f1y6kc"
credencial.txt
```

Esse arquivo contém o material necessário para que o John the Ripper tente identificar a senha correspondente ao hash.

A separação do hash em um arquivo próprio evita trabalhar diretamente sobre o `/etc/shadow` durante a atividade.

---

## 5. Execução do John the Ripper

Com o arquivo de teste preparado, foi executado:

```bash id="q8s4nv"
john -format=crypt credencial.txt
```

O John identificou o hash e iniciou a tentativa de recuperação utilizando suas regras e a wordlist padrão.

Saída observada:

```text id="d2v7rx"
Created directory: /root/.john
Using default input encoding: UTF-8
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Cost 1 (algorithm [1:descrypt 2:md5crypt 3:sunmd5 4:bcrypt 5:sha256crypt 6:sha512crypt]) is 2 for all loaded hashes
Cost 2 (algorithm specific iterations) is 1 for all loaded hashes
Will run 2 OpenMP threads
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
Almost done: Processing the remaining buffered candidate passwords, if any.
Proceeding with wordlist:/usr/share/john/password.lst
[senha recuperada no laboratório]          (teste1)
1g 0:00:00:00 DONE 2/3 (2024-04-25 18:54) 1.960g/s 8364p/s 8364c/s 8364C/s Alexis..bigred
Use the "--show" option to display all of the cracked passwords reliably
Session completed.
```

A execução apresentou:

```text id="n4s8jq"
Loaded 1 password hash
```

indicando que um hash foi carregado para análise.

Também foi utilizada a wordlist padrão:

```text id="z7c2mx"
/usr/share/john/password.lst
```

O resultado:

```text id="v1h9sk"
1g 0:00:00:00 DONE
```

indica que uma credencial foi recuperada durante a execução.

O plaintext recuperado foi omitido do README porque corresponde à senha utilizada pelo laboratório.

---

## 6. Interpretação do resultado

O resultado demonstra a diferença entre **autenticação online** e **ataque offline**.

Neste exercício, o John the Ripper não precisou realizar tentativas contra uma tela de login. Ele recebeu diretamente o hash da senha e trabalhou localmente para encontrar uma entrada compatível.

O processo pode ser representado de forma simplificada:

```text
Senha de teste
      │
      ▼
Hash armazenado no /etc/shadow
      │
      ▼
Cópia do hash → credencial.txt
      │
      ▼
John the Ripper
      │
      ▼
Wordlist / regras de candidatos
      │
      ▼
Comparação com o hash
      │
      ▼
Senha recuperada
```

Isso evidencia por que a proteção do `/etc/shadow` é importante: obter os hashes pode permitir tentativas de quebra offline sem gerar tentativas de login no serviço original.

---

## 7. Limpeza do arquivo de teste

Após concluir o exercício, foi verificado o conteúdo do diretório:

```bash id="w6k3px"
ls
```

O arquivo criado para a atividade foi removido:

```bash id="a9m4rz"
rm credencial.txt
```

A limpeza evita deixar uma cópia desnecessária do hash utilizado durante o exercício.

---

## Conceitos praticados

### `/etc/shadow`

Arquivo utilizado pelo Linux para armazenar hashes de senhas e informações relacionadas ao envelhecimento das credenciais.

Diferentemente de uma senha em texto puro, o sistema não precisa armazenar a senha diretamente para realizar a autenticação.

### Hash de senha

É o resultado de uma função utilizada para representar uma senha de forma que o valor original não fique armazenado diretamente.

Entretanto, hashes de algoritmos antigos ou senhas fracas podem ser vulneráveis a ataques de recuperação offline.

### MD5-crypt

O laboratório utilizou:

```bash id="j5t8wb"
openssl passwd -1
```

A opção `-1` gera hashes no formato **MD5-crypt**, identificado pelo prefixo `$1$`.

Esse algoritmo é considerado legado e não deve ser utilizado como referência para sistemas modernos de armazenamento de senhas.

### John the Ripper

Ferramenta de auditoria de senhas capaz de testar candidatos contra hashes conhecidos.

Ela pode utilizar diferentes estratégias, incluindo:

* wordlists;
* regras de transformação;
* diferentes formatos de hash;
* combinações de candidatos.

### Ataque offline

Nesse modelo, o atacante trabalha sobre uma cópia do material de autenticação, como hashes, sem precisar enviar cada tentativa ao serviço que originalmente autentica o usuário.

---

## Resultado

A atividade demonstrou, em um ambiente controlado, como o John the Ripper pode ser utilizado para auditar uma credencial a partir de seu hash.

Foi possível:

* analisar a finalidade do `/etc/shadow`;
* criar uma conta específica para o laboratório;
* gerar uma credencial de teste;
* separar o hash em `credencial.txt`;
* identificar o formato `crypt`;
* executar o John the Ripper;
* utilizar a wordlist padrão;
* recuperar a senha de teste;
* remover o arquivo temporário após a atividade.

O exercício reforça a importância de utilizar algoritmos modernos para armazenamento de senhas, aplicar políticas de senhas adequadas e restringir o acesso aos arquivos que armazenam material de autenticação.

---

## Evidência

[**Evidências — Módulo 4 / Aulas 1 e 2**](../evidencias.pdf)

**Print registrado:** etapa 7 da atividade, conforme solicitado pelo roteiro, mostrando a execução do John the Ripper e a recuperação da credencial de teste.
