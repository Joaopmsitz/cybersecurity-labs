# Atividade 9.9 — Criando uma Carteira Bitcoin com Electrum

## Objetivo

Criar uma carteira Bitcoin utilizando o **Electrum** no Kali Linux, configurando uma carteira padrão e verificando suas informações após a criação.

---

## Ambiente

* **Sistema:** Kali Linux
* **Aplicativo:** Electrum
* **Tipo de carteira:** Standard wallet
* **Nome da carteira:** `default_wallet`

> A seed phrase da carteira é uma informação privada e não deve ser registrada, compartilhada ou publicada. Por segurança, ela foi omitida deste README.

---

## 1. Abrindo o Electrum

O Electrum foi iniciado pelo terminal:

```bash id="g7lq4p"
electrum
```

O aplicativo foi aberto para iniciar o processo de criação da carteira.

---

## 2. Aceitando os termos

Na primeira tela do Electrum, foi selecionada a opção:

```text id="v3n8sx"
I Accept
```

Em seguida, foi selecionado **Next** para continuar.

---

## 3. Definindo o nome da carteira

Na tela de escolha do arquivo da carteira, foi mantido o nome padrão:

```text id="j4p2ka"
default_wallet
```

Depois, foi selecionado **Next**.

---

## 4. Selecionando o tipo de carteira

Na tela de configuração do tipo de carteira, foi selecionada:

```text id="m8w5de"
Standard wallet
```

Em seguida, foi selecionado **Next**.

---

## 5. Criando uma nova seed

Na tela seguinte, foi selecionada a opção:

```text id="r2c9hf"
Create a new seed
```

Depois, foi selecionado **Next**.

O Electrum apresentou uma **seed phrase** em inglês para a carteira.

Essa sequência é utilizada para recuperar a carteira caso o arquivo local seja perdido. A seed foi anotada para utilização na atividade seguinte.

> **Importante:** a seed phrase é equivalente a uma credencial de controle da carteira. Ela não deve ser colocada no GitHub, README, prints públicos ou compartilhada com terceiros.

---

## 6. Confirmação da seed

Após a geração, o Electrum solicitou que a seed phrase fosse informada novamente para confirmar que ela havia sido anotada corretamente.

A sequência foi digitada no campo solicitado e foi selecionado:

```text id="a6u1pz"
Next
```

A seed utilizada nesta atividade não é reproduzida neste documento.

---

## 7. Configuração da senha

O Electrum apresentou a opção de definir uma senha para proteger a carteira local.

Conforme solicitado no laboratório, não foi configurada uma senha adicional.

Em seguida, foi selecionado:

```text id="k9s3qw"
Finish
```

A carteira foi criada.

---

## 8. Finalização da criação da carteira

Após a conclusão da configuração, o Electrum carregou a carteira:

```text id="p6d4xm"
default_wallet
```

A carteira estava disponível para utilização no aplicativo.

---

## 9. Notificações de atualização

O Electrum apresentou uma opção relacionada às notificações de atualização.

Foi selecionada:

```text id="h5v7rc"
No
```

para não receber essas notificações durante o laboratório.

---

## 10. Visualização das informações da carteira

No menu superior do Electrum, foi acessado:

```text id="q8z2nb"
Wallet → Information
```

A janela de informações apresentou os dados associados à carteira criada.

Essa tela permite consultar informações da carteira sem precisar expor a seed phrase utilizada durante sua criação.

---

## Evidência — Passo 10

**Frase obrigatória antes do print:**

> **Print da atividade 9.9:** janela `Wallet → Information` do Electrum, demonstrando as informações da carteira criada durante a atividade.

[**Evidências — Módulo 9 / Aulas 35 e 36**](../evidencias.pdf)

> **Atenção:** a seed phrase não deve aparecer no print nem ser registrada no repositório. Caso alguma informação sensível seja exibida na evidência, ela deve ser ocultada antes de publicar o material no GitHub.

---

## 11. Encerramento

Após a realização da evidência, o Electrum foi fechado juntamente com o terminal.

---

## Fluxo da atividade

| Etapa       | Resultado                                        |
| ----------- | ------------------------------------------------ |
| Electrum    | Aplicativo iniciado                              |
| Carteira    | `default_wallet` criada                          |
| Tipo        | `Standard wallet`                                |
| Recuperação | Seed phrase gerada e armazenada de forma privada |
| Verificação | `Wallet → Information`                           |

## Resultado

Uma carteira Bitcoin padrão foi criada com sucesso no Electrum e suas informações foram consultadas pela opção **Wallet → Information**.

A seed phrase foi mantida fora da documentação para preservar a segurança da carteira.
