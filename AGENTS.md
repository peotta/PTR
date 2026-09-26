# Diretrizes do Repositório - ENE0025 (PTR)

Este repositório é destinado à disciplina **ENE0025 - Protocolos de Transporte e Roteamento** do Departamento de Engenharia Elétrica (ENE) da Universidade de Brasília (UnB), sob responsabilidade do Prof. Dr. Laerte Peotta de Melo.

Seu propósito primordial é a **produção, curadoria e publicação de material didático universitário de alto nível** voltado para estudantes de graduação e pós-graduação em Engenharia de Redes de Comunicação, Engenharia Elétrica, Ciência da Computação e áreas correlatas.

---

## 1. Princípios Gerais e Idioma

- **Idioma oficial:** Português do Brasil (pt-BR). Termos técnicos consolidados em inglês (e.g., *handshake*, *jitter*, *throughput*, *forwarding*, *advertisement*) podem ser mantidos no original em itálico quando não houver tradução técnica consagrada, sempre esclarecendo o significado.
- **Tom e Estilo:** Acadêmico, rigoroso, instrutivo, direto e impessoal. O texto final deve parecer ter sido redigido diretamente por um docente ou pesquisador para integrar uma apostila ou repositório de referência.
- **Evitar Vícios de Chatbot:** O conteúdo gerado ou revisado nunca deve conter saudações conversacionais, preâmbulos ou despedidas (e.g., evitar terminantemente "Aqui está...", "Claro!", "Segue abaixo...", "Espero ter ajudado!").

---

## 2. Áreas de Foco Temático

O conteúdo do repositório abrange os seguintes eixos:
1. **Redes de Computadores e Arquitetura TCP/IP:** Fundamentos de comutação, arquitetura em camadas, encapsulamento e modelos de referência.
2. **Protocolos da Camada de Transporte:** TCP (mecanismos de confiabilidade, controle de fluxo, janelas deslizantes, controle de congestionamento, variantes), UDP, SCTP e QUIC.
3. **Protocolos de Roteamento Intra-domínio (IGP):** Roteamento por vetor de distâncias (RIP, RIPng), estado de enlace (OSPFv2, OSPFv3, IS-IS) e EIGRP.
4. **Protocolos de Roteamento Interdomínio (EGP):** BGP-4 e MP-BGP (Sistemas Autônomos, atributos, processo de decisão de rotas, engenharia de tráfego e políticas).
5. **Segurança Cibernética e de Redes:** RPKI, BGPsec, IPSec, TLS/DTLS, autenticação de vizinhança de roteamento, mitigação de spoofing (BCP 38/uRPF), ataques DoS/DDoS e segurança em infraestrutura crítica.
6. **Criptografia Aplicada:** Primitivas criptográficas, funções de hash, assinaturas digitais, certificados X.509 e infraestrutura de chaves públicas.
7. **Sistemas Distribuídos e IoT:** Protocolos leves (CoAP, MQTT), sincronização de tempo (NTP/PTP) e resolução de nomes (DNS, DNSSEC).
8. **Laboratórios Práticos e Emulação:** Práticas orientadas a ambientes de emulação (PNetLab, EVE-NG, GNS3, Containerlab) com imagens Cisco IOS/IOL, Linux Router, FRRouting (FRR) e analisadores de pacotes (Wireshark/tshark/tcpdump).

---

## 3. Diretrizes de Didática e Rigor Técnico

Toda produção didática deve obedecer à seguinte escala de prioridades:
1. **Precisão técnica inegociável:** Informações baseadas em RFCs vigentes da IETF, padrões IEEE e literatura de referência (Kurose & Ross, Tanenbaum, Comer, Doyle, Stevens).
2. **Lógica de progressão didática:** As explicações técnicas devem seguir estruturadamente o fluxo:
   $$\text{Conceito} \longrightarrow \text{Funcionamento Interno} \longrightarrow \text{Exemplo Concreto} \longrightarrow \text{Aplicação Prática / Laboratório}$$
3. **Identificação de Siglas:** Toda sigla deve ser definida por extenso em sua primeira aparição no texto (e.g., *Open Shortest Path First* - OSPF).
4. **Associação de Camadas e Portas:** Quando couber a um protocolo, indicar explicitamente:
   - Camada do Modelo OSI e Camada da Arquitetura TCP/IP;
   - Protocolo de transporte subjacente (TCP, UDP ou encapsulamento direto no IP);
   - Portas reservadas / padrão (e.g., BGP: TCP 179; RIP: UDP 520; OSPF: IP protocolo 89; DNS: UDP/TCP 53).
5. **Comandos e Análise de Saídas:**
   - Comandos de configuração e diagnóstico (CLI Cisco IOS, Linux, etc.) devem ser acompanhados de comentários pontuais.
   - Saídas de comando (`show ip route`, `ip route`, `traceroute`, etc.) devem ser explicadas campo a campo nos trechos mais relevantes para o aprendizado.
6. **Troubleshooting e Diagnóstico:** Apresentar metodologia sistemática de identificação de falhas (verificação de conectividade física/enlace $\rightarrow$ endereçamento e sub-redes $\rightarrow$ adjacências $\rightarrow$ tabelas de roteamento $\rightarrow$ políticas).
7. **Aspectos de Segurança:** Evidenciar potenciais vulnerabilidades inerentes ao protocolo ou à configuração apresentada e as práticas de endurecimento (*hardening*) correspondentes.
8. **Integridade das Informações:** Nunca inventar comandos, parâmetros ou comportamentos RFC inexistentes. Havendo divergência de implementação (ex.: comportamento proprietário vs. RFC), o documento deve assinalar a diferença. Em caso de incerteza, explicitar a condição técnica.

---

## 4. Padrões de Formatação Markdown

Os documentos do repositório devem ser renderizados perfeitamente na interface web do GitHub:
- **Codificação:** UTF-8 estrito.
- **Hierarquia de Cabeçalhos:** Utilizar um único título `#` (H1) por arquivo. A hierarquia subsequente (`##`, `###`, `####`) deve ser rigorosamente contínua, sem saltar níveis (e.g., nunca ir de `##` diretamente para `####`).
- **Listas e Tabelas:** Utilizar listas com parcimônia, apenas quando melhorarem a legibilidade. Tabelas devem ser alinhadas e empregadas para comparações sintéticas, mapeamentos de portas, esquemas de endereçamento ou matrizes de decisão.
- **Blocos de Código:** Sempre utilizar blocos delimitados (*fenced code blocks*) com especificação explícita da linguagem ou sintaxe (e.g., ```` ```bash ````, ```` ```text ````, ```` ```json ````, ```` ```python ````, ```` ```cisco ```` ou ```` ```text ```` para CLIs de roteadores).
- **Diagramas com Mermaid:** Diagramas de topologia, máquinas de estado, sequências de pacotes (*handshake*) e fluxogramas devem ser implementados preferencialmente em sintaxe nativa Mermaid (```` ```mermaid ````).
- **Evitar HTML Supérfluo:** Priorizar a sintaxe pura do Markdown nativo. Tags HTML só são admitidas em casos excepcionais onde o Markdown não atenda (como ajustes específicos de layout em cards com alinhamentos complexos, mantendo parcimônia).

---

## 5. Estrutura Sugerida para Aulas e Roteiros

Para novas aulas ou expansão de conteúdos, sugere-se a adoção da seguinte estrutura modular (adaptando e suprimindo seções conforme o objetivo da prática ou teoria):

```markdown
# Título da Aula ou Roteiro

## Objetivos
(Objetivos de aprendizagem claros e mensuráveis)

## Introdução
(Contextualização no cenário de redes e motivação prática)

## Conceitos Fundamentais
(Definições, terminologia, enquadramento nas camadas e RFCs)

## Funcionamento
(Mecanismos operacionais, máquinas de estado, troca de mensagens)

## Exemplos
(Cenários ilustrativos teóricos e cálculos/análises)

## Aplicação Prática
(Casos de uso em operadoras, provedores de Internet e datacenters)

## Laboratório
(Topologia emulada, pré-requisitos, diagrama Mermaid, tabela de endereçamento)

## Comandos Importantes
(Sintaxe de configuração e comandos de verificação/inspeção comentados)

## Troubleshooting
(Sintomas típicos, causas comuns e comandos de depuração)

## Segurança
(Vulnerabilidades potenciais, vetores de ataque e boas práticas de proteção)

## Perguntas para Fixação
(Questões reflexivas e problemas conceituais)

## Resumo
(Síntese dos pontos-chave abordados)

## Referências
(RFCs da IETF, documentação de fabricantes e livros-texto fundamentais)
```

---

## 6. Governança de Arquivos Locais e Política Crítica de Git

Este repositório possui separação rigorosa entre materiais públicos destinados aos alunos e materiais de uso privado, rascunhos ou controle acadêmico interno do docente.

### Diretórios Locais e Privados (NÃO versionar)
Por convenção padrão, os seguintes diretórios são estritamente locais e não devem ser enviados ao GitHub:
- `aulas/`, `Aulas/`, `aulas-local/`
- `material-aula/`, `materiais-aula/`, `materiais-brutos/`
- `rascunhos/`
- `privado/`, `private/`
- `working/`, `workspace/`
- `temp/`, `tmp/`
- `export/`, `exports/`, `output/`
- Pastas de controle avaliativo: `provas/`, `gabaritos/`, `notas/`, `frequencia/`

### Arquivos com Bloqueio de Publicação
- Provas não aplicadas ou rascunhos de testes;
- Gabaritos privados e critérios de correção restritos;
- Planilhas de notas e listas nominais de frequência;
- Documentos administrativos da universidade e dados pessoais (LGPD);
- Credenciais, senhas, *tokens* de API, chaves criptográficas privadas (`*.key`, `*.pem`, `id_*`);
- Arquivos de trava e temporários de suítes de escritório (`~$*.docx`, `~$*.pptx`, `~$*.xlsx`);
- Backups e arquivos temporários de editores (`*.bak`, `*.tmp`, `*.autosave`, `*~`).

### Procedimento Mandatório de Git
1. **PROIBIDO `git add .` ou `git add -A`:** O agente ou usuário nunca deve adicionar indiscriminadamente todos os arquivos do workspace.
2. **Ciclo de Staging Seguro:**
   - Executar `git status` para inspecionar arquivos modificados e não rastreados.
   - Validar que nenhum arquivo privado, temporário ou sensível está pendente.
   - Adicionar arquivos **nominalmente e individualmente** (exemplo: `git add labs/lab14.md`).
   - Conferir as alterações preparadas via `git diff --cached`.
   - Realizar o commit com mensagem clara e objetiva.
3. **Push sob Demanda Explícita:** Nunca realizar `git push` automaticamente. O envio ao repositório remoto só ocorre sob instrução direta do usuário.
