# 🍃 Mongod — Starting Point (Very Easy)

🔗 Prova de conclusão:
https://labs.hackthebox.com/achievement/machine/2578759/501

## ✔ O que foi praticado
- Enumeração inicial com Nmap, identificando a porta MongoDB (27017) aberta
- Verificação do acesso ao serviço MongoDB sem autenticação
- Conexão ao banco utilizando o cliente `mongo` diretamente na porta exposta
- Enumeração dos bancos de dados com `show dbs`
- Acesso ao banco contendo a flag
- Listagem de coleções e recuperação do documento com `db.flag.find()`
- Identificação de falha de configuração (MongoDB exposto sem senha)
- Compreensão do risco de bancos NoSQL acessíveis publicamente sem controle de acesso
