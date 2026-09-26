---
description: Diretrizes comportamentais permanentes para produção de material didático universitário, integridade de arquivos e governança de segurança do Git.
trigger: always_on
---

# Regras Comportamentais Permanentes - ENE0025 (PTR)

Esta regra é de aplicação permanente (`trigger: always_on`) em qualquer interação do agente dentro deste repositório.

## 1. Postura Pedagógica e Produção Didática

- **Qualidade Universitária:** Produzir materiais didáticos claros, aprofundados e tecnicamente precisos, adequados para estudantes de engenharia e pós-graduação.
- **Vedação a Resumos Indevidos:** Nunca sintetizar ou encurtar excessivamente roteiros de aula, explicações teóricas ou comandos práticos, a menos que solicitado expressamente pelo usuário. Manter o nível de detalhamento necessário para reprodução autônoma pelo estudante.
- **Progressão Pedagógica:** Respeitar a sequência de aprendizado: fundamentação teórica prévia $\rightarrow$ arquitetura e funcionamento do protocolo $\rightarrow$ configuração passo a passo $\rightarrow$ verificação e análise de pacotes $\rightarrow$ diagnóstico e segurança.
- **Consistência Terminológica:** Empregar terminologia canônica de redes (conforme RFCs da IETF e padrões IEEE). Manter coerência de nomes de interfaces, nós e endereçamentos ao longo de todo o documento.
- **Validação de Sintaxe Markdown:** Todo documento gerado deve aderir estritamente ao GitHub Flavored Markdown (GFM), com blocos de código tipados, tabelas alinhadas e diagramas Mermaid válidos.
- **Revisão Prévia:** Revisar internamente a coerência de comandos, endereços IPs e diagramas antes de persistir alterações em disco.

## 2. Preservação do Repositório e Não Intrusividade

- **Modificação Estrita:** Não alterar arquivos, roteiros de laboratório ou pastas que não tenham sido explicitamente solicitados pelo usuário.
- **Integridade de Estrutura:** Preservar nomes de arquivos, convenções de maiúsculas/minúsculas e arquitetura de diretórios existente.
- **Não Reorganização:** É expressamente proibido renomear, mover arquivos em lote ou reestruturar diretórios sem pedido prévio e autorização expressa.
- **Resolução de Conflitos:** Havendo conflito entre uma nova instrução e uma configuração já existente, manter o arquivo original e reportar a divergência ao usuário antes de tomar qualquer medida destrutiva.

## 3. Segurança Crítica em Operações Git

O agente atua em um repositório acadêmico que pode coexistir com anotações de aula locais, rascunhos em preparação e dados sensíveis. Por conseguinte:

### Comandos Terminantemente Proibidos
```bash
# NUNCA EXECUTAR:
git add .
git add -A
git commit -a
```

### Fluxo Obrigatório de Versionamento
Antes de qualquer operação de commit:
1. Executar `git status` e examinar detalhadamente a lista de arquivos alterados e não rastreados (*untracked*).
2. Confrontar a lista contra as regras do [.gitignore](file:///e:/Downloads/OneDrive%20-%20unb.br/ENE0025%20-%20PROTOCOLOS%20DE%20TRANSPORTE%20E%20ROTEAMENTO%20-%2060H/.gitignore).
3. Confirmar a ausência de pastas locais (`aulas/`, `rascunhos/`, `privado/`, etc.) ou arquivos sensíveis (notas, gabaritos, credenciais, temporários de Office).
4. Adicionar **individual e explicitamente** apenas os arquivos concluídos e destinados à publicação no GitHub (ex.: `git add labs/lab02.md`).
5. Inspecionar o *staging area* executando:
   ```bash
   git diff --cached
   ```
6. Executar o commit apenas com mensagem semântica e objetiva.

### Delimitação de Ações do Agente
- Criar, editar ou corrigir um arquivo **NÃO AUTORIZA** o agente a executar commit, push, tag ou abertura de pull request.
- O comando `git push` **SOMENTE** pode ser executado mediante solicitação pontual, literal e inequívoca do usuário.
