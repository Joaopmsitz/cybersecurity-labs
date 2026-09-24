# 🐘 Sequel — Starting Point (Very Easy)

🔗 Prova de conclusão:
https://labs.hackthebox.com/achievement/machine/2578759/403

## ✔ O que foi praticado
- Enumeração inicial com Nmap, identificando o serviço MySQL aberto (porta 3306)
- Teste de conexão sem autenticação ao servidor MySQL
- Acesso ao banco diretamente sem senha devido à configuração incorreta
- Enumeração das bases de dados usando comandos SQL básicos
- Identificação da tabela contendo a flag
- Consulta e leitura da flag com `SELECT`
- Identificação de falha de configuração (MySQL sem autenticação)
- Compreensão do impacto de serviços de banco expostos sem controle de acesso
