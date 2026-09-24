# 🏛️ Archetype — Starting Point (Very Easy)

🔗 Prova de conclusão:
https://labs.hackthebox.com/achievement/machine/2578759/287

## ✔ O que foi praticado
- Enumeração inicial com Nmap, identificando serviços SMB e SQL Server na máquina
- Enumeração de compartilhamentos SMB para localizar arquivos acessíveis publicamente
- Download e análise de arquivos de configuração contendo credenciais do banco
- Conexão ao Microsoft SQL Server utilizando as credenciais encontradas
- Execução de comandos via SQL utilizando `xp_cmdshell` para obter um shell inicial
- Criação de payload e uso de reverse shell para ganhar acesso ao sistema
- Enumeração pós-exploração no Windows para identificar caminhos de escalonamento
- Escalonamento de privilégios para Administrator
- Coleta das duas flags: user.txt e root.txt
- Compreensão de um fluxo completo de ataque: enumeração → credenciais → RCE → shell → privesc → flags
