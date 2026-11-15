# Activity 4.1 — Getting Started with CyberChef

## Objective

Use CyberChef to decode a hexadecimal string protected by a single-byte XOR operation. The exercise introduces CyberChef recipes and demonstrates how brute-force analysis can recover data when part of the expected plaintext is known.

## Tool

- [CyberChef — GCHQ](https://gchq.github.io/CyberChef/)

CyberChef is a web-based tool for encoding, decoding, encryption, data transformation, and analysis. Operations are arranged in sequence in a recipe, allowing multiple transformations to be applied to the same input.

## Procedure

### 1. Enter the hexadecimal input

Open CyberChef and insert the following value into the Input panel:

    01160439247629711d242e76251d2472301d36713136732c253f

### 2. Convert hexadecimal data into bytes

Search for the **From Hex** operation and add it to the recipe.

Configuration:

| Parameter | Value |
|---|---|
| Delimiter | Auto |

This operation interprets the input as hexadecimal data and converts it into the corresponding byte sequence. It is required because the XOR operation must work on the decoded bytes rather than on the visible hexadecimal characters.

### 3. Apply XOR Brute Force

Search for **XOR Brute Force** and add it after **From Hex**.

Configuration used in the exercise:

| Parameter | Value |
|---|---|
| Key length | 1 |
| Sample length | 100 |
| Sample offset | 0 |
| Scheme | Standard |
| Crib / known plaintext | `CTF{` |

The key length of 1 instructs the operation to test a single-byte XOR key. The known plaintext, also called a crib, gives the operation a recognizable sequence expected to appear in the decoded result.

The operation evaluates candidate keys and displays the output that matches the supplied known plaintext.

### 4. Analyze the result

The result reported by the activity was:

    Key = 42: CTF{f4k3_fl4g_f0r_t3st1ng}

The recovered text is a test flag supplied by the training exercise. It demonstrates successful recovery of a short message protected by a repeating one-byte XOR key.

## Technical notes

XOR combines each plaintext byte with a key byte. Applying the same key again reverses the operation:

    Plaintext XOR Key = Ciphertext
    Ciphertext XOR Key = Plaintext

A short or predictable plaintext prefix can make brute-force analysis easier. In this activity, `CTF{` was used as the known plaintext to identify the candidate output.

The result is a controlled training example. Recovering this test flag does not imply that arbitrary XOR-protected data can always be decoded without additional information.

## Result

The CyberChef recipe successfully identified the candidate key and recovered:

`CTF{f4k3_fl4g_f0r_t3st1ng}`

## Evidence

[View Universal Class Evidence PDF — Page 1](../evidences.pdf)
