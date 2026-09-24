# 🐀 Nibbles — Starting Point (Easy)

🔗 Prova de conclusão:  
https://labs.hackthebox.com/achievement/machine/2578759/121

## ✔ O que foi praticado
- Enumeração inicial com Nmap, identificando portas 22 (SSH) e 80 (HTTP) abertas
- Enumeração web identificando aplicação *NibbleBlog* rodando na porta 80
- Enumeração de diretórios e arquivos escondidos usando *gobuster/dirb*
- Descoberta do diretório `/admin` e identificação da página de login
- Obtenção de credenciais válidas (ex.: `admin:nibbles`) para acessar o painel administrativo
- Upload de uma **PHP reverse shell** através da funcionalidade de upload do NibbleBlog
- Execução da shell e obtenção de acesso ao sistema remoto
- Transferência do **linEnum** para a máquina alvo para auxiliar na enumeração de privilégios
- Execução do linEnum para identificar vetor de escalada
- Identificação de **falha no sudo**, permitindo executar um script como root
- Exploração da configuração de sudo para obter **acesso root**
- Captura da flag como usuário root e conclusão da máquina
