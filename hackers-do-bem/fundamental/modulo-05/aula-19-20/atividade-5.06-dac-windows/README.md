# Atividade 5.6 — Implementando o Controle de Acesso Discricionário (DAC) no Windows Server 2022

## Objetivo

Implementar o **Controle de Acesso Discricionário (DAC — Discretionary Access Control)** no Windows Server 2022 cliente por meio das permissões de arquivos e pastas.

Nesta atividade, foi utilizado o usuário de domínio `Nome1` para demonstrar como permissões NTFS podem restringir o próprio proprietário do recurso e, posteriormente, restaurar o acesso.

---

## Ambiente

* Windows Server 2022 — cliente
* Active Directory
* Domínio: `aluno.hacker.com`
* Cliente: `192.168.98.30`
* Usuário de domínio: `ALUNO\nome1`
* Recurso utilizado: pasta `Documents`
* Arquivo: `Arquivo1.txt`

---

## 1. Acessando o Windows Server 2022 cliente

Foi estabelecida uma conexão RDP com o Windows Server 2022 cliente:

```text
192.168.98.30
```

O acesso foi realizado utilizando o usuário de domínio:

```text
ALUNO\nome1
```

As credenciais utilizadas no laboratório não são registradas neste README.

---

## 2. Criando o arquivo de teste

Após o login, foi aberto o **Notepad** através do campo:

```text
Type here to search
```

Foi criado o conteúdo:

```text
Teste
```

O arquivo foi salvo como:

```text
Arquivo1.txt
```

na pasta:

```text
Documents
```

Depois do salvamento, o Notepad foi fechado.

---

## 3. Verificando o arquivo no Explorer

Foi aberto o **File Explorer** e acessada a pasta:

```text
Documents
```

O arquivo:

```text
Arquivo1.txt
```

foi localizado no diretório.

Esse arquivo será utilizado para demonstrar o funcionamento das permissões de acesso.

---

## 4. Acessando as propriedades de segurança

Com o botão direito sobre a pasta:

```text
Documents
```

foi selecionado:

```text
Properties
```

Na janela de propriedades, foi acessada a aba:

```text
Security
```

Foram identificados os principais grupos e usuários com permissões sobre o recurso, incluindo:

```text
SYSTEM
Nome1
Administrators
```

---

## 5. Visualizando as permissões do Administrador

Foi selecionado:

```text
Administrators
```

Na área de permissões, foi possível observar que o grupo possuía permissões marcadas em:

```text
Allow
```

incluindo as permissões necessárias para controle do recurso.

Essa etapa demonstra que o grupo administrativo possui permissões elevadas sobre a pasta.

---

## 6. Tentativa de remoção do grupo Administrators

Foi selecionado o grupo:

```text
Administrators
```

e utilizado o botão:

```text
Remove
```

O Windows apresentou uma mensagem impedindo a remoção.

Foi selecionado:

```text
OK
```

O sistema manteve o grupo administrativo associado ao recurso.

---

## 7. Negando o acesso do usuário Nome1

Em seguida, foi selecionado:

```text
Nome1
```

Na seção de permissões, foi marcada a opção:

```text
Deny
```

para:

```text
Full control
```

Foi selecionado:

```text
Apply
```

e confirmado o aviso através das opções apresentadas pelo Windows, incluindo:

```text
Yes
```

e:

```text
Continue
```

quando solicitado.

A partir desse momento, o usuário `Nome1` passou a ter o acesso negado à pasta `Documents`.

---

## 8. Verificando a restrição de acesso

Foi retornado ao **File Explorer**.

Ao tentar acessar novamente:

```text
Documents
```

o arquivo:

```text
Arquivo1.txt
```

deixou de estar disponível para o usuário.

O acesso à pasta também passou a ser bloqueado devido à permissão de negação aplicada ao usuário.

---

## 9. Confirmando a negação de acesso

No **File Explorer**, foi acessada outra pasta, como:

```text
Downloads
```

e, em seguida, foi tentado novamente o acesso à:

```text
Documents
```

O Windows apresentou uma mensagem indicando que o acesso havia sido negado.

Foi selecionado:

```text
Continue
```

e foram solicitadas credenciais administrativas para prosseguir.

Após a autenticação administrativa, o sistema continuou apresentando a mensagem:

```text
You have been denied permission to access this folder
```

Foi selecionado:

```text
Close
```

Essa etapa demonstra, na prática, o efeito da entrada **Deny** aplicada ao usuário.

---

## 10. Acessando novamente as propriedades

Foi utilizado o botão direito sobre:

```text
Documents
```

e selecionado:

```text
Properties
```

Em seguida, foi acessada novamente a aba:

```text
Security
```

---

## 11. Restaurando as permissões do usuário

Foi selecionado o usuário:

```text
Nome1
```

e removidas as marcações presentes na coluna:

```text
Deny
```

As alterações foram aplicadas através de:

```text
Apply
```

e:

```text
Continue
```

até que os avisos apresentados pelo Windows fossem encerrados.

Com a remoção das regras de negação, o acesso do usuário pôde ser restaurado.

---

## 12. Verificando a recuperação do acesso

Após restaurar as permissões, foi acessada novamente outra pasta no **File Explorer**, como:

```text
Downloads
```

e posteriormente:

```text
Documents
```

O acesso à pasta foi novamente permitido.

O arquivo:

```text
Arquivo1.txt
```

voltou a estar acessível ao usuário.

**Esta é a etapa solicitada como evidência da atividade.**

---

## DAC — Controle de Acesso Discricionário

O **Discretionary Access Control (DAC)** é um modelo de controle de acesso no qual as permissões sobre um recurso são definidas de acordo com usuários e grupos.

No Windows, as permissões podem ser configuradas através das propriedades de segurança de arquivos e diretórios.

Neste laboratório, o controle foi demonstrado diretamente sobre a pasta:

```text
Documents
```

utilizando o usuário:

```text
Nome1
```

---

## Allow x Deny

As permissões do Windows possuem entradas de:

```text
Allow
```

e:

```text
Deny
```

**Allow** concede uma determinada permissão ao usuário ou grupo.

**Deny** bloqueia explicitamente uma permissão.

Nesta atividade, foi configurado:

```text
Nome1
    ↓
Deny
    ↓
Full control
```

Isso impediu o usuário de acessar a pasta, mesmo sendo o usuário utilizado para criar o arquivo.

Posteriormente, a entrada de negação foi removida para restaurar o acesso.

---

## Conceito demonstrado

O laboratório demonstra que o controle de acesso não depende apenas de quem criou o arquivo.

O usuário `Nome1` criou:

```text
Arquivo1.txt
```

mas posteriormente uma regra explícita de:

```text
Deny → Full control
```

foi aplicada ao próprio usuário.

Como resultado, o acesso ao recurso foi bloqueado até que a regra fosse removida.

---

## Resultado

Foi implementado um cenário de **DAC no Windows Server 2022**, utilizando as permissões de segurança da pasta `Documents`.

O acesso do usuário `Nome1` foi inicialmente permitido, posteriormente negado através de:

```text
Deny → Full control
```

e finalmente restaurado após a remoção das permissões de negação.

O teste demonstrou na prática como as ACLs do Windows podem controlar o acesso de usuários a arquivos e diretórios.

---

## Evidências

[**Evidências — Módulo 5 / Aulas 3 e 4**](../evidencias.pdf)

**Evidência registrada:** passo 18 — acesso novamente à pasta `Documents` após a remoção das permissões `Deny`.
