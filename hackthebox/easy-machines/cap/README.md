# 🧢 Cap — Starting Point (Easy)

🔗 Prova de conclusão:  
https://labs.hackthebox.com/achievement/machine/2578759/351

## ✔ O que foi praticado
- Enumeração inicial com Nmap, identificando portas 21 (FTP), 22 (SSH) e 80 (HTTP)
- Acesso ao serviço HTTP e identificação da funcionalidade de download de arquivos `.pcap`
- Download e análise do arquivo `.pcap` disponível no site
- Uso da ferramenta **Wireshark** para inspecionar o tráfego capturado
- Extração de credenciais em texto claro observadas dentro do pacote de captura
- Login via SSH utilizando as credenciais obtidas
- Acesso ao sistema remoto para captura da flag
- Identificação de falha grave: exposição de dados sensíveis por meio de pacotes de rede
- Compreensão do risco de *Sensitive Data Exposure* em ambientes mal configurados
