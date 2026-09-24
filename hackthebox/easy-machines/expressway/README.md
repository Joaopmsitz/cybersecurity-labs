# 🚇 ExpressWay — Starting Point (Easy)

🔗 Prova de conclusão:  
https://labs.hackthebox.com/achievement/machine/2578759/736

## ✔ O que foi praticado
- Enumeração inicial com Nmap, identificando portas 80 (HTTP) e 4380 (alternativa HTTP)
- Identificação de aplicação web rodando Express.js
- Uso do **Wappalyzer / WhatWeb** para confirmar tecnologias backend
- Exploração de uma **vulnerabilidade de SSTI (Server-Side Template Injection)** na aplicação
- Testes iniciais com payloads básicos de SSTI para confirmar a falha
- Execução de comandos através da injeção de template
- Obtenção de uma shell reversa na máquina alvo
- Navegação pelo sistema comprometido para coleta da flag
- Entendimento do risco crítico de SSTI permitindo execução remota de código (RCE)
