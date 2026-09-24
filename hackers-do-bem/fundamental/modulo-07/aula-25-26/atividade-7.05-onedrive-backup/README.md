# Atividade 7.5 — Backup Síncrono com OneDrive

## Objetivo

Configurar o OneDrive em um cliente Windows Server 2022 para realizar o backup e a sincronização de pastas do sistema com o armazenamento em nuvem.

---

## 1. Acesso ao Windows Server

A atividade foi realizada no cliente Windows Server 2022 por meio de RDP.

Após o acesso, foi utilizado o Explorador de Arquivos para acessar:

```text
C:\curso
```

Dentro desse diretório estava disponível o instalador:

```text
OneDriveSetup
```

A instalação foi iniciada utilizando as permissões administrativas necessárias.

> Credenciais utilizadas durante o laboratório não são registradas neste README.

---

## 2. Configuração das Opções da Internet

Após a instalação, foi realizada uma configuração no Windows para adicionar o serviço utilizado pelo OneDrive aos sites confiáveis.

No menu de pesquisa do Windows, foi pesquisado:

```text
Internet Options
```

Na janela **Internet Properties**, foi acessada a aba:

```text
Security
```

Em seguida, foi selecionada a opção:

```text
Trusted Sites
```

e acessado:

```text
Sites
```

Foi adicionado o endereço:

```text
https://odc.officeapps.live.com
```

Depois, as alterações foram confirmadas utilizando **Close** e **OK**.

---

## 3. Autenticação no OneDrive

Após a configuração, foi realizada uma busca pelo aplicativo **OneDrive** no Windows.

O aplicativo foi iniciado e foi realizada a autenticação utilizando uma conta Microsoft.

Após o login, o assistente de configuração do OneDrive foi apresentado.

---

## 4. Configuração da pasta do OneDrive

No assistente de configuração, foi selecionada a opção referente à pasta do OneDrive.

O procedimento foi avançado utilizando **Next**, mantendo a configuração apresentada pelo assistente.

---

## 5. Configuração do backup das pastas

Na etapa **Back up folders on this PC**, foram apresentadas as pastas disponíveis para backup.

Para o laboratório, foi selecionada somente a pasta:

```text
Desktop
```

Em seguida, foi selecionado:

```text
Start backup
```

O assistente continuou pelas etapas seguintes utilizando **Next**.

---

## 6. Finalização da configuração

Após avançar pelas etapas do assistente, foi apresentada a opção relacionada ao aplicativo móvel do OneDrive.

Foi selecionado:

```text
Later
```

para finalizar essa etapa sem configurar o aplicativo móvel.

---

## 7. Verificação da sincronização

Para verificar o resultado da configuração, foi selecionada a opção:

```text
Open my OneDrive folder
```

O Explorador de Arquivos foi aberto mostrando a pasta sincronizada do OneDrive.

Essa etapa permitiu verificar visualmente que o OneDrive estava configurado no Windows Server e que a pasta estava disponível para sincronização com a nuvem.

---

## Evidência

[**Evidências — Módulo 7 / Aulas 1 e 2**](../evidencias.pdf)
