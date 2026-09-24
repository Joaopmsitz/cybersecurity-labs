# 🔻 Funnel — Starting Point (Very Easy)

🔗 Prova de conclusão:
https://labs.hackthebox.com/achievement/machine/2578759/520

## ✔ O que foi praticado
- Enumeração inicial com Nmap, identificando serviço HTTP na porta 80
- Análise da aplicação web e descoberta de endpoint vulnerável
- Identificação de parâmetro que permitia leitura de arquivos locais
- Exploração de LFI (Local File Inclusion) para acessar arquivos sensíveis
- Leitura do arquivo contendo a flag por meio da vulnerabilidade
- Entendimento da falha causada por falta de sanitização em parâmetros de arquivo
- Compreensão dos riscos de exposição de arquivos internos via LFI
