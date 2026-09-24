# 💯 Two Million — Starting Point (Easy)

🔗 Prova de conclusão:  
https://labs.hackthebox.com/achievement/machine/2578759/547

## ✔ O que foi praticado
- Enumeração inicial com Nmap, identificando portas 22 (SSH), 80 (HTTP) e 443 (HTTPS)
- Acesso ao serviço HTTP e análise do conteúdo da página inicial
- Identificação de uma aplicação web simples utilizando **PHP** e **MySQL**
- Exploração de vulnerabilidade **SQL Injection** na aplicação de login
- Uso de **SQLmap** para automatizar a exploração da SQLi
- Obtenção de credenciais de login através da SQL Injection
- Acesso via SSH utilizando as credenciais obtidas
- Navegação pelo sistema comprometido até encontrar a flag
- Compreensão do risco de **SQL Injection** e sua capacidade de permitir o controle total da base de dados e do sistema
