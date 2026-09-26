---
name: aula-markdown
description: >-
  Criação, conversão e estruturação de materiais didáticos, aulas teóricas e roteiros de laboratório em Markdown no padrão do repositório ENE0025 (PTR).
  Use quando o usuário solicitar criar uma aula, converter notas ou apresentações para Markdown, estruturar conteúdo acadêmico, expandir tópicos, criar roteiros de práticas ou produzir documentação técnica educacional.
---

# Procedimento para Elaboração de Aulas e Laboratórios em Markdown

Este guia orienta o fluxo completo para criação, expansão e conversão de conteúdos educacionais no contexto da disciplina **ENE0025 - Protocolos de Transporte e Roteamento (UnB)**.

---

## 1. Fluxo de Trabalho Passo a Passo

1. **Identificação do Escopo e Tema:**
   - Determinar se o documento é uma aula teórica conceitual, um roteiro prático de laboratório (PNetLab / CLI) ou um documento de apoio/comandos.
2. **Contextualização com o Repositório:**
   - Consultar o [README.md](file:///e:/Downloads/OneDrive%20-%20unb.br/ENE0025%20-%20PROTOCOLOS%20DE%20TRANSPORTE%20E%20ROTEAMENTO%20-%2060H/README.md) e os roteiros em [labs/](file:///e:/Downloads/OneDrive%20-%20unb.br/ENE0025%20-%20PROTOCOLOS%20DE%20TRANSPORTE%20E%20ROTEAMENTO%20-%2060H/labs) para manter coerência com a numeração, terminologia, convenções de endereçamento IP e estilos pré-existentes.
3. **Estruturação do Documento:**
   - Incluir o cabeçalho institucional padrão:
     ```markdown
     # Laboratório XX - [Título do Laboratório]
     
     **Disciplina:** ENE0025 - Protocolos de Transporte e Roteamento  
     **Professor responsável:** Prof. Dr. Laerte Peotta de Melo  
     
     ---
     ```
   - Aplicar a hierarquia contínua de títulos (`#`, `##`, `###`), sem saltar níveis.
4. **Ficha Técnica de Protocolos (quando aplicável):**
   - Ao introduzir um protocolo de redes (transporte, roteamento ou aplicação), consolidar seus parâmetros-chave:
     - **Nome oficial e Sigla:** ex.: *Border Gateway Protocol* (BGP-4)
     - **Camadas de Referência:** Camada OSI e Camada da pilha TCP/IP
     - **Transporte Subjacente e Portas:** ex.: TCP porta 179
     - **Tipo de Comunicação e Mensagens:** ex.: Mensagens OPEN, UPDATE, KEEPALIVE, NOTIFICATION
     - **Endereçamento:** Unicast, Multicast reservado (ex.: `224.0.0.5`/`224.0.0.6` no OSPF) ou Broadcast
     - **RFCs Relevantes:** ex.: RFC 4271 (BGP-4), RFC 2328 (OSPFv2)
5. **Diagramação Visual com Mermaid:**
   - Para topologias, máquinas de estado de protocolos ou troca de mensagens (*three-way handshake*, negociações), criar diagramas em Mermaid:
     ```mermaid
     flowchart LR
         R1["📡 Router R1<br>192.168.1.1"] <-->|Enlace Gigabit| R2["📡 Router R2<br>192.168.1.2"]
     ```
6. **Tabela de Endereçamento IP:**
   - Para práticas de laboratório, fornecer sempre a matriz clara com Dispositivo, Interface, Endereço IP, Máscara em notação decimal e CIDR, Gateway e Função.
7. **Comandos e Análise de Saídas:**
   - Sintaxe em blocos de código com linguagem especificada (`cisco`, `bash`, `text`).
   - Apresentar comandos comentados e explicar o significado de parâmetros e flags cruciais.
   - Fornecer amostras realistas de saídas esperadas (`show ip route`, `show ip ospf neighbor`, `tcpdump`, etc.) destacando os campos essenciais.
8. **Troubleshooting Sistemático:**
   - Fornecer tabela ou roteiro de diagnóstico de erros comuns (e.g., mismatch de máscara, MTU inconsistente, timers incompatíveis, falta de rota de retorno).
9. **Aspectos de Segurança:**
   - Apresentar riscos intrínsecos (e.g., injeção de rotas falsas, spoofing, ausência de autenticação) e soluções correspondentes (MD5/SHA-256 HMAC, RPKI ROA, listas de controle de acesso - ACL).
10. **Revisão e Auto-Validação:**
    - Verificar que não há links quebrados, tags HTML dispensáveis ou vícios de conversação de chatbot.
