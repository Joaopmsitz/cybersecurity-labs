# 🧩 Oopsie — Starting Point (Very Easy)

🔗 Prova de conclusão:
https://labs.hackthebox.com/achievement/machine/2578759/288

## ✔ O que foi praticado
- Enumeração inicial com Nmap, identificando serviço HTTP ativo na porta 80
- Descoberta de painel administrativo protegido por login
- Identificação de credenciais expostas em endpoint acessível sem autenticação
- Acesso ao painel usando as credenciais encontradas
- Enumeração interna do painel para localizar funcionalidades sensíveis
- Escalonamento horizontal de privilégios através de IDOR (Insecure Direct Object Reference)
- Obtenção de acesso como usuário privilegiado na aplicação
- Upload e execução de web shell para ganhar acesso ao sistema
- Enumeração pós-exploração no Linux para encontrar vetor de privesc
- Escalonamento de privilégios para root e coleta das flags user.txt e root.txt
- Compreensão do fluxo completo de exploração baseado em falhas de controle de acesso e má validação de permissões
