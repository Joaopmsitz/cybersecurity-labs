# 🔄 Synced — Starting Point (Very Easy)

🔗 Prova de conclusão:
https://labs.hackthebox.com/achievement/machine/2578759/515

## ✔ O que foi praticado
- Enumeração inicial com Nmap, identificando a porta rsync (873) aberta
- Verificação de módulos expostos no serviço com `rsync --list-only`
- Acesso anônimo ao módulo configurado sem autenticação
- Listagem dos arquivos disponíveis dentro do módulo rsync
- Download do arquivo contendo a flag usando rsync
- Identificação de falha de configuração (rsync permitindo acesso anônimo)
- Compreensão do risco de exposição de arquivos por serviços de sincronização mal configurados
