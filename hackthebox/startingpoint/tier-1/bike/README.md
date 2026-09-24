# 🚲 Bike — Starting Point (Very Easy)

🔗 Prova de conclusão:
https://labs.hackthebox.com/achievement/machine/2578759/449

## ✔ O que foi praticado
- Enumeração inicial com Nmap, identificando serviço FTP na porta 21
- Teste de autenticação anônima para acesso ao FTP
- Conexão bem-sucedida ao serviço usando login `anonymous`
- Listagem de diretórios e identificação de arquivos disponíveis
- Download do arquivo contendo a flag diretamente pelo FTP
- Identificação da falha de configuração (FTP permitindo acesso anônimo)
- Compreensão do risco de exposição de arquivos em serviços sem autenticação
