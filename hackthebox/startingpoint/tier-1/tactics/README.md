# 🎯 Tactics — Starting Point (Very Easy)

🔗 Prova de conclusão:
https://labs.hackthebox.com/achievement/machine/2578759/407

## ✔ O que foi praticado
- Enumeração inicial com Nmap, identificando serviço WinRM rodando na porta 5985
- Teste de autenticação utilizando credenciais padrão/óbvias
- Descoberta de credenciais fracas que permitiam acesso via WinRM
- Conexão ao sistema usando `evil-winrm` para obter shell remoto
- Navegação pelo sistema até localizar o diretório do usuário
- Leitura do arquivo contendo a flag através do shell WinRM
- Identificação de falha de segurança (credenciais extremamente fracas)
- Compreensão do risco causado por autenticação inadequada em serviços remotos
