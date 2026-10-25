# Activity 1.4 — Classical Cryptography with ROT13 and Caesar Cipher

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 01  
> **Class:** 01–02  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Explore basic cryptography concepts by applying the ROT13 substitution cipher and implementing a Caesar cipher in Python.

The activity demonstrates how text can be transformed using a fixed alphabet shift and recovered by applying the inverse shift.

## Environment

- **Operating system:** Kali Linux
- **Terminal:** Linux command line
- **Python:** Python 3
- **Tools:** `rot13`, `nano`

## Procedure

### 1. Test ROT13

The `rot13` command was used to transform a message:

```bash
echo "Hackers do bem - Fundamental" | rot13
```

Output:

```text
Unpxref qb orz - Shaqnzragny
```

The ROT13 transformation was then applied to the encoded text:

```bash
echo "Unpxref qb orz - Shaqnzragny" | rot13
```

Output:

```text
Hackers do bem - Fundamental
```

ROT13 shifts each letter by 13 positions in the alphabet. Since the English alphabet contains 26 letters, applying the transformation twice restores the original text.

### 2. Create the Caesar Cipher Program

A Python file named `cesar_cipher.py` was created in the Documents directory:

```bash
cd /home/aluno/Documentos/
nano cesar_cipher.py
```

The following code was used:

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

The program processes each character and applies the shift specified by the user. Non-letter characters, such as spaces and hyphens, are preserved.

**Implementation note:** The code is designed for basic English letters (`A–Z` and `a–z`). It does not correctly handle all Unicode alphabetic characters, such as accented letters.

### 3. Encrypt a Message

The program was executed using:

```bash
python3 cesar_cipher.py
```

The input message was:

```text
Hackers do bem - Fundamental
```

The shift value was:

```text
10
```

The resulting encrypted text was:

```text
Rkmuobc ny low - Pexnkwoxdkv
```

Each letter was shifted ten positions forward in the alphabet, wrapping around when necessary.

### 4. Decrypt the Message

The program was executed again:

```bash
python3 cesar_cipher.py
```

The encrypted message was entered:

```text
Rkmuobc ny low - Pexnkwoxdkv
```

The inverse shift was applied:

```text
-10
```

The result was:

```text
Hackers do bem - Fundamental
```

This demonstrated that the same function can encrypt and decrypt a message by using an appropriate shift value.

### 5. Clean Up the Environment

After completing the activity, the Python script was removed:

```bash
rm cesar_cipher.py
```

The remaining files were checked using:

```bash
ls
```

## Commands Used

```bash
echo "Hackers do bem - Fundamental" | rot13
echo "Unpxref qb orz - Shaqnzragny" | rot13
cd /home/aluno/Documentos/
nano cesar_cipher.py
python3 cesar_cipher.py
rm cesar_cipher.py
ls
```

## Result

The activity demonstrated how to apply ROT13 to a message and implement a Caesar cipher in Python for both encryption and decryption.

ROT13 restored the original message when applied twice. The Caesar cipher transformed the input using a shift of 10 and recovered the original text when the inverse shift of -10 was applied.

## Concepts Practiced

- Classical cryptography
- ROT13 substitution cipher
- Caesar cipher
- Encryption and decryption
- Alphabetic character shifting
- Python string manipulation
- Use of `ord()` and `chr()`
- Execution of Python scripts on Linux
- Basic command-line file management

**Security note:** ROT13 and the Caesar cipher are historical substitution techniques and should not be used to protect real-world sensitive information. They are included here for educational purposes only.

## Evidence

The activity was documented in the PDF containing the evidence for Classes 01–02.

The evidence shows the execution of the ROT13 commands and the Caesar cipher program, including the transformation and recovery of the message.

[View Evidence — Classes 01–02](../evidencias.pdf)

---

[Back to Classes 01–02](../) · [Back to Module 01](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
