# 📨 Responder — Starting Point (Very Easy)

🔗 Prova de conclusão:
https://labs.hackthebox.com/achievement/machine/2578759/461

## ✔ O que foi praticado
- Enumeração inicial com Nmap, identificando serviço HTTP rodando na porta 80
- Análise do site para descobrir funcionalidades disponíveis
- Interceptação das requisições enviadas pela aplicação
- Identificação de endpoint vulnerável permitindo acesso a arquivos locais
- Exploração de LFI (Local File Inclusion) para ler arquivos sensíveis do sistema
- Acesso ao arquivo contendo a flag através do LFI
- Identificação da falha de configuração (falta de validação em caminhos fornecidos pelo usuário)
- Compreensão do risco de exposição de arquivos por vulnerabilidades de inclusão local
