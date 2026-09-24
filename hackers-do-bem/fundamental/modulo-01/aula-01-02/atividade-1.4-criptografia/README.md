# Atividade 1.4 — Criptografia

## Objetivo

Praticar conceitos básicos de criptografia por meio da cifra ROT13 e da implementação de uma cifra de César em Python.

A atividade demonstra como um texto pode ser transformado utilizando um deslocamento fixo no alfabeto e posteriormente recuperado aplicando o deslocamento inverso.

## Ambiente

* Kali Linux
* Terminal
* Python 3
* `rot13`
* Editor `nano`

## Procedimento

### 1. Teste com ROT13

Primeiro, foi utilizado o comando `rot13` para aplicar a transformação sobre uma mensagem:

```bash
echo "Hackers do bem - Fundamental" | rot13
```

Resultado:

```text
Unpxref qb orz - Shaqnzragny
```

Em seguida, foi aplicado o ROT13 novamente sobre o texto transformado:

```bash
echo "Unpxref qb orz - Shaqnzragny" | rot13
```

Resultado:

```text
Hackers do bem - Fundamental
```

Como o ROT13 utiliza um deslocamento de 13 posições, aplicar a transformação duas vezes retorna o texto original.

### 2. Criação da cifra de César

Foi criado o arquivo `cesar_cipher.py` no diretório `Documentos`:

```bash
cd /home/aluno/Documentos/
nano cesar_cipher.py
```

O código utilizado foi:

```python
def caesar_cipher(text, shift):
    result = ""

    for char in text:
        if char.isalpha():
            shift_amount = shift % 26

            if char.islower():
                shifted = ord(char) + shift_amount

                if shifted > ord("z"):
                    shifted -= 26

                result += chr(shifted)

            else:
                shifted = ord(char) + shift_amount

                if shifted > ord("Z"):
                    shifted -= 26

                result += chr(shifted)
        else:
            result += char

    return result


def main():
    text = input("Digite o texto a ser cifrado/descifrado: ")
    shift = int(input("Digite a quantidade de posições a ser deslocada: "))

    encrypted_text = caesar_cipher(text, shift)

    print("Texto cifrado/descifrado:", encrypted_text)


if __name__ == "__main__":
    main()
```

O programa percorre cada caractere da mensagem e aplica um deslocamento definido pelo usuário. Caracteres que não são letras, como espaços e hífens, são mantidos.

### 3. Cifrando uma mensagem

O programa foi executado com:

```bash
python3 cesar_cipher.py
```

Foi utilizada a mensagem:

```text
Hackers do bem - Fundamental
```

Com deslocamento:

```text
10
```

O resultado foi:

```text
Rkmuobc ny low - Pexnkwoxdkv
```

### 4. Decifrando a mensagem

Para recuperar o texto original, o programa foi executado novamente:

```bash
python3 cesar_cipher.py
```

Foi utilizado o texto cifrado:

```text
Rkmuobc ny low - Pexnkwoxdkv
```

E aplicado o deslocamento inverso:

```text
-10
```

Resultado:

```text
Hackers do bem - Fundamental
```

Isso demonstra que o mesmo algoritmo pode ser utilizado para cifrar e decifrar uma mensagem, desde que o deslocamento correto seja conhecido.

### 5. Limpeza

Após concluir a atividade, o arquivo utilizado no laboratório foi removido:

```bash
rm cesar_cipher.py
```

Em seguida, foi verificado o conteúdo do diretório:

```bash
ls
```

## Comandos utilizados

```bash
sudo -i

echo "Hackers do bem - Fundamental" | rot13

echo "Unpxref qb orz - Shaqnzragny" | rot13

cd /home/aluno/Documentos/

nano cesar_cipher.py

python3 cesar_cipher.py

rm cesar_cipher.py

ls
```

## Resultado

Foi possível aplicar ROT13 em uma mensagem e implementar uma cifra de César em Python, realizando tanto a cifragem quanto a decifragem por meio da alteração do deslocamento no alfabeto.

## Conceitos praticados

* Criptografia clássica
* ROT13
* Cifra de César
* Cifragem e decifragem
* Deslocamento de caracteres
* Manipulação de strings em Python
* Uso de `ord()` e `chr()`
* Execução de scripts Python no Linux

> **Observação:** ROT13 e cifra de César são técnicas criptográficas históricas e não devem ser utilizadas para proteger informações reais. A atividade tem finalidade exclusivamente didática.

## Evidência

A execução da atividade foi registrada no PDF de evidências da Aula 01–02.

[Ver evidências — Aula 01–02](https://github.com/Joaopmsitz/hackers-do-bem-labs/blob/main/fundamental/modulo-01/aula-01-02/evidencias.pdf)
