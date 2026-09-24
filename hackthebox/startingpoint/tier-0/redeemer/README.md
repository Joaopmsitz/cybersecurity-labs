# 🛡️ Redeemer — Starting Point (Very Easy)

🔗 Prova de conclusão:
https://labs.hackthebox.com/achievement/machine/2578759/472

## ✔ O que foi praticado
- Enumeração inicial com Nmap, identificando a porta Redis (6379) aberta
- Verificação do acesso ao serviço Redis sem autenticação
- Conexão ao serviço por meio do utilitário `redis-cli`
- Execução de comandos básicos do Redis (`INFO`, `KEYS *`) para explorar o banco
- Identificação da chave contendo a flag armazenada no Redis
- Recuperação do valor da flag com o comando `GET`
- Identificação de falha de configuração (Redis exposto sem senha)
- Compreensão do risco de serviços de banco de dados em memória sem controle de acesso
