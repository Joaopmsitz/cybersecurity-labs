# Atividade 9.10 — Recuperando uma Carteira Bitcoin e Gerando QR Code no Electrum

## Objetivo

Simular a perda de uma carteira Bitcoin no Electrum, recuperar a carteira utilizando sua **seed phrase** e gerar uma solicitação de pagamento utilizando um endereço Bitcoin e QR Code.

---

## Ambiente

* **Sistema:** Kali Linux
* **Aplicativo:** Electrum
* **Carteira:** `default_wallet`
* **Tipo:** Standard wallet
* **Valor solicitado:** `1 mBTC` (`0,001 BTC`)
* **Expiração da solicitação:** 1 dia
* **Método:** On-chain

> A seed phrase utilizada para recuperar a carteira é uma informação extremamente sensível e não é registrada neste README. Ela deve permanecer privada e nunca ser publicada no GitHub.

---

## 1. Abrindo o Electrum

O Electrum foi iniciado pelo terminal:

```bash
electrum
```

A aplicação foi aberta para realizar o processo de recuperação da carteira.

---

## 2. Simulando a perda da carteira

Com o Electrum aberto, foi acessado o menu:

```text id="e8s4kp"
File → Delete
```

A exclusão foi confirmada selecionando:

```text id="w6c2ra"
Yes
```

A carteira local foi excluída, simulando uma situação de perda do arquivo da carteira.

---

## 3. Reabrindo o Electrum

Após a exclusão, o Electrum foi iniciado novamente para realizar o processo de recuperação da carteira.

---

## 4. Selecionando a carteira

Na tela inicial, foi mantido o nome:

```text id="n7f3vx"
default_wallet
```

Em seguida, foi selecionado:

```text id="q5k9mb"
Next
```

---

## 5. Selecionando o tipo de carteira

Foi selecionado novamente o tipo:

```text id="r4j8tc"
Standard wallet
```

Depois, foi selecionado **Next**.

---

## 6. Informando que a seed já existe

Na tela de configuração da carteira, foi selecionada a opção:

```text id="u2d6zs"
I already have a seed
```

Essa opção informa ao Electrum que a carteira será recuperada a partir de uma seed existente.

Em seguida, foi selecionado **Next**.

---

## 7. Recuperando a carteira pela seed

O Electrum solicitou a seed phrase utilizada na atividade anterior.

A seed foi digitada no campo correspondente e foi selecionado:

```text id="c9m5hf"
Next
```

> A seed phrase não é reproduzida neste documento. Ela deve ser mantida exclusivamente em local seguro e privado.

---

## 8. Configuração da senha

O Electrum solicitou a configuração da senha da carteira.

Foi utilizada a mesma configuração definida anteriormente. Como a carteira original não possuía senha adicional, o campo permaneceu sem senha.

Em seguida, foi selecionado:

```text id="k3p7yw"
Finish
```

---

## 9. Verificação da recuperação

Após a conclusão do processo, a carteira foi recuperada e carregada novamente no Electrum.

A recuperação demonstra que a **seed phrase** é suficiente para restaurar a carteira e seus dados associados, desde que seja utilizada corretamente.

---

## 10. Acesso à aba Receive

No Electrum, foi acessada a aba:

```text id="m8v2qa"
Receive
```

Essa área permite criar solicitações de pagamento e obter um endereço para recebimento de Bitcoin.

---

## 11. Definindo a descrição

No campo de descrição da solicitação foi inserido um exemplo:

```text id="s5n4jx"
Pagamento de aposta de futebol
```

A descrição serve para identificar a finalidade da solicitação dentro da carteira.

---

## 12. Definindo o valor e a validade

No campo de valor solicitado foi informado:

```text id="t7c1bz"
1 mBTC
```

A conversão utilizada é:

```text
1 mBTC = 0,001 BTC
```

Também foi configurada a expiração da solicitação para:

```text id="y6r3wd"
1 day
```

---

## 13. Selecionando o método On-chain

A opção:

```text id="p4h8nk"
Onchain
```

foi selecionada para utilizar uma transação Bitcoin convencional na rede.

Após a configuração, o Electrum apresentou o endereço correspondente à solicitação.

---

## 14. Copiando o endereço

O campo contendo o endereço Bitcoin foi selecionado para realizar a cópia do endereço.

Esse endereço pode ser fornecido ao responsável pelo pagamento para que ele possa enviar os bitcoins solicitados.

> O endereço Bitcoin não é equivalente à seed phrase. Ainda assim, não é necessário registrar o endereço real no README.

---

## 15. Gerando o QR Code

Na solicitação de pagamento, foi utilizado o ícone de **QR Code** para gerar a representação visual dos dados da solicitação.

O QR Code permite que outra pessoa escaneie as informações da solicitação utilizando uma carteira compatível.

---

## Evidência — QR Code

**Frase obrigatória antes do print:**

> **Print da atividade 9.10:** QR Code gerado pelo Electrum para a solicitação de pagamento de `1 mBTC`, demonstrando a geração da solicitação de recebimento.

[**Evidências — Módulo 9 / Aulas 35 e 36**](../evidencias.pdf)

> **Importante:** nunca registre ou publique a seed phrase. Antes de disponibilizar evidências publicamente, verifique se nenhum dado privado da carteira foi exposto.

---

## 16. Encerramento

Após a geração da evidência, o Electrum foi fechado juntamente com o terminal.

---

## Fluxo da atividade

| Etapa       | Resultado                             |
| ----------- | ------------------------------------- |
| Simulação   | Carteira local excluída               |
| Recuperação | `default_wallet` restaurada pela seed |
| Solicitação | `1 mBTC` / `0,001 BTC`                |
| Validade    | 1 dia                                 |
| Recebimento | Solicitação On-chain com QR Code      |

## Resultado

A carteira Bitcoin foi recuperada com sucesso utilizando a seed phrase e uma nova solicitação de recebimento foi criada no Electrum.

O valor configurado foi de **1 mBTC (0,001 BTC)**, com validade de um dia e geração de um **QR Code** para facilitar o pagamento.
