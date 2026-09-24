# 📦 Included — Starting Point (Very Easy)

🔗 Prova de conclusão:
https://labs.hackthebox.com/achievement/machine/2578759/292

## ✔ O que foi praticado
- Enumeração inicial com Nmap, identificando serviço HTTP na porta 80
- Análise da aplicação web para localizar endpoints vulneráveis
- Identificação de LFI (Local File Inclusion) por meio de parâmetro sem validação
- Exploração do LFI para ler arquivos internos e obter informações sensíveis
- Descoberta de credenciais ou caminhos importantes através de arquivos do sistema
- Uso das informações obtidas para estabelecer acesso inicial ao servidor
- Enumeração pós-exploração no Linux para encontrar vetor de escalonamento
- Exploração de serviço ou binário vulnerável para elevar privilégios até root
- Coleta das duas flags: user.txt e root.txt
- Entendimento do fluxo completo: LFI → foothold → privesc → root
