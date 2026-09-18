# Atividade 8.7 — Computando Hash SHA-1, SHA-2 e SHA-3

## Objetivo

Calcular o **hash** de um arquivo utilizando diferentes algoritmos da família SHA no Kali Linux:

* SHA-1;
* SHA-2 de 512 bits;
* SHA-3 de 512 bits.

A atividade demonstra a utilização de diferentes ferramentas para gerar resumos criptográficos e permite comparar os tamanhos e valores produzidos pelos algoritmos.

---

## Ambiente

* **Sistema:** Kali Linux
* **Ferramentas:** `sha1sum`, `sha512sum` e `sha3sum`
* **Diretório de trabalho:** `/home/aluno/Documentos/Arquivos`
* **Arquivo analisado:** `mensagem.txt`
* **Conteúdo:** `Hackers do bem!`

> As credenciais utilizadas para acesso ao ambiente de laboratório não são registradas neste README.

---

## 1. Acesso como root

Inicialmente, foi obtido acesso administrativo ao Kali Linux:

```bash
sudo -i
```

---

## 2. Acesso ao diretório e verificação do arquivo

Foi acessado o diretório utilizado na atividade:

```bash
cd /home/aluno/Documentos/Arquivos
```

Em seguida, foi verificada a presença do arquivo `mensagem.txt`:

```bash
ls
```

Saída:

```text
mensagem.txt
```

O mesmo arquivo utilizado na atividade anterior foi utilizado para calcular os hashes da família SHA.

---

## 3. Cálculo do SHA-1

Foi utilizado o comando `sha1sum`:

```bash
sha1sum mensagem.txt
```

Saída:

```text
287f168af5acf44b3b06a07fb6f3a4e882a9baab  mensagem.txt
```

O SHA-1 produz um resumo de **160 bits**, representado por **40 caracteres hexadecimais**.

Apesar de ainda aparecer em ferramentas e sistemas legados, o SHA-1 não é recomendado para novos usos que dependam de resistência a colisões.

---

## 4. Cálculo do SHA-2 de 512 bits

Para calcular o SHA-2 de 512 bits, foi utilizado:

```bash
sha512sum mensagem.txt
```

Saída:

```text
d0774282912bf4b5479165a9b316f23fea1f9ae3f620f400618813347a13c8d1e297fb51196def065dafe0aa21239d719f51a8cf58410bac22fc4b40b29efeab  mensagem.txt
```

O SHA-512 produz um resumo de **512 bits**, representado por **128 caracteres hexadecimais**.

---

## 5. Cálculo do SHA-3 de 512 bits

Por fim, foi utilizado o `sha3sum` para calcular o SHA-3 de 512 bits:

```bash
sha3sum -b -a 512 mensagem.txt
```

Saída:

```text
07ad8830012228703f01d1961a759c907214a617c2c42fade253af6bf42bf4500a54038f1fb960165e6cb4985fed141ed90b949f7915d2379c7a67d5484930f1 *mensagem.txt
```

Nesse comando:

* `-b` indica a utilização do modo binário;
* `-a 512` seleciona a variante SHA-3 com saída de 512 bits.

O resultado possui **128 caracteres hexadecimais**, correspondentes a 512 bits.

### Evidência solicitada

A evidência da atividade corresponde ao **passo 5**, referente ao cálculo do SHA-3 de 512 bits:

```text
┌──(root㉿kali)-[/home/aluno/Documentos/Arquivos]
└─# sha3sum -b -a 512 mensagem.txt                    
07ad8830012228703f01d1961a759c907214a617c2c42fade253af6bf42bf4500a54038f1fb960165e6cb4985fed141ed90b949f7915d2379c7a67d5484930f1 *mensagem.txt
```

[**Evidências — Módulo 8 / Aulas 31 e 32**](../evidencias.pdf)

---

## Comparação dos resultados

| Algoritmo        | Tamanho do resumo | Hash obtido                                                                                                                        |
| ---------------- | ----------------: | ---------------------------------------------------------------------------------------------------------------------------------- |
| SHA-1            |          160 bits | `287f168af5acf44b3b06a07fb6f3a4e882a9baab`                                                                                         |
| SHA-2 / SHA-512  |          512 bits | `d0774282912bf4b5479165a9b316f23fea1f9ae3f620f400618813347a13c8d1e297fb51196def065dafe0aa21239d719f51a8cf58410bac22fc4b40b29efeab` |
| SHA-3 / SHA3-512 |          512 bits | `07ad8830012228703f01d1961a759c907214a617c2c42fade253af6bf42bf4500a54038f1fb960165e6cb4985fed141ed90b949f7915d2379c7a67d5484930f1` |

Os três algoritmos produziram resumos distintos para o mesmo arquivo.

O SHA-1 possui limitações conhecidas relacionadas à resistência a colisões, enquanto SHA-2 e SHA-3 fazem parte de famílias mais modernas de funções de hash criptográfico.

---

## Resultado

A atividade demonstrou como calcular hashes utilizando diferentes gerações da família SHA. Os valores obtidos podem ser utilizados para verificar a integridade de arquivos, comparando o resumo calculado em momentos diferentes para identificar alterações no conteúdo.
