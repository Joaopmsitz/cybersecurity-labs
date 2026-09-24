# Atividade 8.2 — Ofuscando código Python no Kali Linux

## Objetivo

Utilizar o compilador do Python para gerar uma versão em **bytecode otimizado** de um programa e verificar seu comportamento após a alteração da extensão do arquivo compilado.

A atividade demonstra uma forma simples de dificultar a leitura direta do código-fonte, transformando o programa Python em bytecode. O arquivo resultante não mantém a estrutura legível do código-fonte original.

---

## Ambiente

* **Sistema:** Kali Linux
* **Linguagem:** Python
* **Diretório de trabalho:** `/home/aluno/Documentos/Arquivos`
* **Arquivo original:** `arquivo.py`
* **Arquivo compilado:** `arquivo.cpython-313.opt-2.pyc`
* **Arquivo utilizado na execução:** `arquivo_ofuscado.py`

> As credenciais utilizadas no ambiente de laboratório não são registradas neste README.

---

## 1. Acesso como root

Inicialmente, foi obtido acesso administrativo ao Kali Linux:

```bash
sudo -i
```

---

## 2. Criação do arquivo Python

Foi acessado o diretório utilizado nas atividades:

```bash
cd /home/aluno/Documentos/Arquivos
```

Em seguida, foi criado o arquivo Python:

```bash
nano arquivo.py
```

O código utilizado foi:

```python
def somar(a, b):
    return a + b

def subtrair(a, b):
    return a - b

resultado = somar(5, 3)
print(resultado)
```

O programa possui duas funções matemáticas, `somar()` e `subtrair()`. No fluxo executado, a função `somar()` é utilizada para calcular `5 + 3`.

---

## 3. Teste do código original

Antes de realizar a compilação, o código foi executado normalmente:

```bash
python arquivo.py
```

Saída:

```text
8
```

Isso confirma que o código-fonte estava funcionando corretamente antes da transformação em bytecode.

---

## 4. Compilação em bytecode otimizado

Foi utilizado o Python com a opção `-OO` para gerar uma versão otimizada do bytecode:

```bash
python -OO -m py_compile arquivo.py
```

Após a compilação, foi utilizado `ls` para verificar os arquivos:

```bash
ls
```

Saída:

```text
arquivo.py  __pycache__
```

O diretório `__pycache__` foi criado automaticamente pelo Python para armazenar o arquivo compilado.

---

## 5. Acesso ao bytecode e renomeação

O diretório de bytecode foi acessado:

```bash
cd __pycache__
```

Em seguida, foi verificado seu conteúdo:

```bash
ls
```

O arquivo `.pyc` gerado pelo Python foi então renomeado para `arquivo_ofuscado.py`:

```bash
mv arquivo.cpython-313.opt-2.pyc arquivo_ofuscado.py
```

Após a operação, o arquivo presente no diretório passou a ser:

```text
arquivo_ofuscado.py
```

Embora a extensão tenha sido alterada para `.py`, o conteúdo continua sendo **bytecode Python compilado**, e não o código-fonte original.

---

## 6. Visualização do conteúdo compilado

Foi utilizado `cat` para visualizar o conteúdo do arquivo:

```bash
cat arquivo_ofuscado.py
```

A saída apresentada pelo terminal foi semelhante a:

```text
�
y�0ir��2�S▒rS▒r\"SS5r\"\5 g)c�
�X-$�N���a�bs  �
arquivo.py�somarr       �       ��

                                  �5�L�c�
�X-
rrr̵rs  subtrairr
r
���N)r  resultado�printrr
�!�Q�K� ��i�r            <module>rs$����
```

O conteúdo não aparece como um código Python convencional porque o arquivo contém **bytecode**, representado por dados binários.

Renomear o arquivo de `.pyc` para `.py` não converte o bytecode novamente em código-fonte. A extensão é apenas o nome utilizado no arquivo; o formato interno permanece compilado.

---

## 7. Execução do arquivo ofuscado

Mesmo estando em formato de bytecode, o arquivo foi utilizado para executar o programa:

```bash
python arquivo_ofuscado.py
```

O resultado obtido foi:

```text
8
```

Isso demonstra que o programa continuou funcional após a compilação e renomeação do arquivo.

A execução preservou o comportamento do código original, realizando a operação `5 + 3` e exibindo o resultado.

---

## Evidência

A evidência solicitada para a atividade corresponde ao **passo 8**, que demonstra a execução do arquivo ofuscado:

```text
┌──(root㉿kali)-[/home/aluno/Documentos/Arquivos/__pycache__]
└─# python arquivo_ofuscado.py         
8
```

[**Evidências — Módulo 8 / Aulas 29 e 30**](../evidencias.pdf)
