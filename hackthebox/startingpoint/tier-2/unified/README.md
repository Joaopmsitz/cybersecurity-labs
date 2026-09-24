# 🛰️ Unified — Starting Point (Very Easy)

🔗 Prova de conclusão:
https://labs.hackthebox.com/achievement/machine/2578759/441

## ✔ O que foi praticado
- Enumeração inicial com Nmap, identificando múltiplos serviços ativos (SSH, HTTP e API)
- Análise da interface web e descoberta de endpoints acessíveis publicamente
- Enumeração da API para localizar credenciais expostas ou funcionalidades sensíveis
- Obtenção de acesso inicial explorando falha de autenticação/validação na API
- Upload ou execução de payload para estabelecer acesso ao sistema
- Enumeração pós-exploração no Linux para identificar caminhos de escalonamento
- Descoberta de serviço interno vulnerável permitindo aumento de privilégios
- Escalonamento até root utilizando a vulnerabilidade identificada
- Coleta das duas flags: user.txt e root.txt
- Compreensão do fluxo completo de exploração envolvendo API → foothold → privesc
