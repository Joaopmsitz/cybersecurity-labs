# 💃 Dancing — Starting Point (Very Easy)

🔗 Prova de conclusão:
https://labs.hackthebox.com/achievement/machine/2578759/395

## ✔ O que foi praticado
- Enumeração inicial com Nmap, identificando portas SMB abertas (135, 139, 445)
- Identificação do serviço SMB ativo na máquina
- Enumeração de compartilhamentos SMB usando `smbclient -L`
- Verificação de acesso anônimo habilitado
- Acesso ao compartilhamento WorkShares sem autenticação
- Navegação pelos diretórios dos usuários dentro do share
- Download do arquivo contendo a flag usando `get`
- Identificação de falha de configuração (SMB com permissões anônimas)
- Compreensão do risco de exposição de arquivos sem controle de acesso
