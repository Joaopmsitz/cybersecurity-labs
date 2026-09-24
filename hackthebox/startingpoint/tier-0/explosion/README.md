# 💥 Explosion — Starting Point (Very Easy)

🔗 Prova de conclusão:
https://labs.hackthebox.com/achievement/machine/2578759/396

## ✔ O que foi praticado
- Enumeração inicial com Nmap, identificando a porta SSH (22) e o serviço SMB (445)
- Enumeração de compartilhamentos SMB usando `smbclient -L`
- Acesso ao compartilhamento `backups` sem autenticação
- Download do arquivo de backup contendo informações sensíveis
- Extração dos arquivos do backup para análise
- Localização da flag armazenada dentro dos arquivos extraídos
- Identificação de falha de configuração (SMB com permissões anônimas)
- Compreensão do risco de exposição de dados sensíveis por compartilhamentos sem controle de acesso
