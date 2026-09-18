# Atividade 2.6 — Explorando a criptografia de dados com Ccrypt no Kali Linux

## Objetivo

Explorar a ferramenta **Ccrypt** no Kali Linux para compreender, de forma prática, o processo de criptografia e descriptografia de um arquivo.

A atividade teve como objetivo demonstrar como um arquivo de texto pode ser protegido por uma chave de criptografia, deixando seu conteúdo ilegível enquanto estiver cifrado, e posteriormente recuperado utilizando a chave correta.

> **Aviso:** a atividade foi realizada exclusivamente para fins acadêmicos e em ambiente de laboratório. A senha utilizada foi criada somente para o exercício.

## Ambiente

* Kali Linux
* Terminal
* Ccrypt
* Nano
* Sistema virtualizado de laboratório

## Procedimento

### 1. Consulta sobre o Ccrypt

Antes de iniciar a prática no Kali Linux, foi consultado o site oficial do projeto Ccrypt para conhecer suas características e finalidade:

```text
https://ccrypt.sourceforge.net/
```

O Ccrypt é uma ferramenta de linha de comando destinada à criptografia e descriptografia de arquivos e fluxos de dados.

### 2. Acesso ao modo administrador

O Terminal do Kali Linux foi aberto e o modo superusuário foi acessado utilizando:

```bash
sudo -i
```

### 3. Acesso ao diretório de documentos

Em seguida, foi acessado o diretório `Documentos` do usuário:

```bash
cd /home/aluno/Documentos/
```

O conteúdo do diretório foi verificado com:

```bash
ls
```

### 4. Criação do arquivo de texto

Foi utilizado o editor de texto `nano` para criar o arquivo:

```bash
nano mensagem.txt
```

Dentro do arquivo foi inserida a mensagem:

```text
Hackers do bem!
```

O arquivo foi salvo utilizando `Ctrl + X`, seguido da confirmação solicitada pelo editor.

### 5. Verificação do arquivo criado

Após salvar o arquivo, o conteúdo do diretório foi novamente listado:

```bash
ls
```

A saída observada foi:

```text
mensagem.txt
```

A presença de `mensagem.txt` confirmou que o arquivo havia sido criado corretamente.

Nesse momento, o arquivo ainda estava em texto simples e seu conteúdo podia ser lido normalmente.

### 6. Consulta das opções do Ccrypt

Antes de realizar a criptografia, foram consultadas as opções disponíveis na ferramenta:

```bash
ccrypt -h
```

A saída apresentada foi:

```text
ccrypt 1.11. Secure encryption and decryption of files and streams.

Usage: ccrypt [mode] [options] [file...]
       ccencrypt [options] [file...]
       ccdecrypt [options] [file...]
       ccat [options] file...

Modes:
    -e, --encrypt         encrypt
    -d, --decrypt         decrypt
    -c, --cat             cat; decrypt files to stdout
    -x, --keychange       change key
    -u, --unixcrypt       decrypt old unix crypt files

Options:
    -h, --help            print this help message and exit
    -V, --version         print version info and exit
    -L, --license         print license info and exit
    -v, --verbose         print progress information to stderr
    -q, --quiet            run quietly; suppress warnings
    -f, --force            overwrite existing files without asking
    -m, --mismatch        allow decryption with non-matching key
    -E, --envvar var      read keyword from environment variable (unsafe)
    -K, --key key         give keyword on command line (unsafe)
    -k, --keyfile file    read keyword(s) as first line(s) from file
    -P, --prompt prompt   use this prompt instead of default
    -S, --suffix .suf     use suffix .suf instead of default .cpt
    -s, --strictsuffix    refuse to encrypt files which already have suffix
    -F, --envvar2 var     as -E for second keyword (for keychange mode)
    -H, --key2 key        as -K for second keyword (for keychange mode)
    -Q, --prompt2 prompt  as -P for second keyword
    -t, --timid           prompt twice for encryption keys (default)
    -b, --brave           prompt only once for encryption keys
    -y, --keyref file     encryption key must match this encrypted file
    -r, --recursive       recurse through directories
    -R, --rec-symlinks    follow symbolic links as subdirectories
    -l, --symlinks        dereference symbolic links
    -T, --tmpfiles        use temporary files instead of overwriting (unsafe)
    --                    end of options, filenames follow
```

Entre as opções observadas, destacam-se:

| Opção | Função                                              |
| ----- | --------------------------------------------------- |
| `-e`  | Criptografar um arquivo                             |
| `-d`  | Descriptografar um arquivo                          |
| `-c`  | Descriptografar e exibir o conteúdo na saída padrão |
| `-x`  | Alterar a chave de criptografia                     |
| `-h`  | Exibir a ajuda da ferramenta                        |
| `-V`  | Exibir informações da versão                        |
| `-v`  | Exibir informações de progresso                     |
| `-r`  | Processar diretórios recursivamente                 |

### 7. Criptografia do arquivo

Com o arquivo `mensagem.txt` criado, foi utilizado o parâmetro `-e` para realizar a criptografia:

```bash
ccrypt -e mensagem.txt
```

O Ccrypt solicitou a chave de criptografia:

```text
Enter encryption key:
Enter encryption key: (repeat)
```

Foi utilizada uma senha criada especificamente para o laboratório.

O parâmetro `-e` indica que a operação realizada é de **encryption**, ou seja, criptografia.

O arquivo especificado foi:

```text
mensagem.txt
```

Após a conclusão da operação, o arquivo original foi convertido para uma versão criptografada com a extensão `.cpt`.

### 8. Verificação do arquivo criptografado

Este foi o **print solicitado pela atividade**.

O diretório foi listado novamente:

```bash
ls
```

A saída observada foi:

```text
mensagem.txt.cpt
```

Em seguida, foi utilizado `cat` para visualizar o conteúdo do arquivo cifrado:

```bash
cat mensagem.txt.cpt
```

O resultado apresentado foi semelhante a:

```text
Z�w�.����K��^������>�I6E9Y�i��8Z;mU�\�;X�
```

O conteúdo deixou de apresentar a mensagem original em texto legível.

Isso demonstra visualmente que o arquivo passou a armazenar dados cifrados.

> **Observação:** caracteres aparentemente aleatórios ou ilegíveis são esperados ao tentar visualizar diretamente um arquivo criptografado como se fosse um arquivo de texto comum.

### 9. Descriptografia do arquivo

Para recuperar o arquivo original, foi utilizado o parâmetro `-d`:

```bash
ccrypt -d mensagem.txt.cpt
```

A ferramenta solicitou novamente a chave:

```text
Enter decryption key:
```

Foi informada a mesma chave utilizada anteriormente na criptografia.

O parâmetro `-d` indica a operação de **decryption**, responsável por descriptografar o arquivo.

O arquivo utilizado como entrada foi:

```text
mensagem.txt.cpt
```

Após a operação, o arquivo original `mensagem.txt` foi recuperado.

### 10. Verificação da recuperação do arquivo

O diretório foi listado novamente:

```bash
ls
```

A saída observada foi:

```text
mensagem.txt
```

Em seguida, o conteúdo do arquivo foi visualizado:

```bash
cat mensagem.txt
```

O resultado foi:

```text
Hackers do bem!
```

A mensagem original foi recuperada corretamente.

Esse resultado confirma que o processo de descriptografia foi realizado com sucesso utilizando a chave correspondente.

### 11. Remoção do arquivo

Após concluir a demonstração, o arquivo de texto foi removido:

```bash
rm mensagem.txt
```

O diretório foi verificado novamente:

```bash
ls
```

O arquivo `mensagem.txt` não estava mais presente.

O Terminal foi encerrado após a conclusão da atividade.

## Comandos utilizados

Os principais comandos executados durante a atividade foram:

```bash
sudo -i
cd /home/aluno/Documentos/
ls
nano mensagem.txt
ccrypt -h
ccrypt -e mensagem.txt
ls
cat mensagem.txt.cpt
ccrypt -d mensagem.txt.cpt
ls
cat mensagem.txt
rm mensagem.txt
ls
```

## Fluxo da atividade

O processo realizado pode ser representado da seguinte forma:

```text
mensagem.txt
     │
     │ ccrypt -e
     ▼
mensagem.txt.cpt
     │
     │ conteúdo cifrado
     ▼
Dados ilegíveis
     │
     │ ccrypt -d
     ▼
mensagem.txt
     │
     ▼
Hackers do bem!
```

## Interpretação

A atividade demonstrou na prática o uso da criptografia para proteger dados armazenados em arquivos.

Inicialmente, o arquivo continha:

```text
Hackers do bem!
```

Após a utilização de:

```bash
ccrypt -e mensagem.txt
```

o arquivo passou a possuir a extensão `.cpt`:

```text
mensagem.txt.cpt
```

Ao tentar visualizar diretamente esse arquivo com `cat`, o conteúdo deixou de ser legível, demonstrando que os dados haviam sido transformados em uma representação cifrada.

Posteriormente, utilizando:

```bash
ccrypt -d mensagem.txt.cpt
```

e fornecendo a chave correta, o arquivo original foi recuperado e seu conteúdo voltou a ser:

```text
Hackers do bem!
```

O experimento demonstra a importância da **confidencialidade dos dados**. A criptografia protege o conteúdo contra leitura direta por quem não possui a chave necessária para realizar a descriptografia.

Também foi possível observar a diferença entre o arquivo original e o arquivo cifrado através da extensão `.cpt`, utilizada pelo Ccrypt para identificar arquivos criptografados.

## Resultado

Foi possível:

* Consultar as funcionalidades do Ccrypt;
* Criar um arquivo de texto no Kali Linux;
* Inserir uma mensagem no arquivo;
* Consultar as opções disponíveis com `ccrypt -h`;
* Criptografar o arquivo utilizando `ccrypt -e`;
* Observar a transformação de `mensagem.txt` em `mensagem.txt.cpt`;
* Verificar que o conteúdo cifrado não era legível diretamente;
* Descriptografar o arquivo utilizando `ccrypt -d`;
* Recuperar o arquivo original;
* Confirmar a recuperação da mensagem;
* Remover o arquivo utilizado no laboratório.

A atividade demonstrou, de forma prática, como a criptografia pode ser utilizada como **controle técnico de proteção da confidencialidade dos dados**.

## Conceitos praticados

* Criptografia
* Descriptografia
* Ccrypt
* Confidencialidade
* Dados em repouso
* Chave de criptografia
* Arquivos cifrados
* Extensão `.cpt`
* Linux
* Linha de comando
* Controle técnico de segurança
* Proteção de dados

## Evidência

A execução da atividade foi registrada no PDF de evidências da Aula 05–06.

[Ver evidências — Aula 05–06](https://github.com/Joaopmsitz/hackers-do-bem-labs/blob/main/fundamental/modulo-02/aula-07-08/evidencias.pdf)

