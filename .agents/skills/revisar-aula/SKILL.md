---
name: revisar-aula
description: >-
  Auditoria e revisão criteriosa de aulas teóricas, roteiros de laboratório e documentação Markdown no repositório ENE0025.
  Use quando o usuário solicitar revisar uma aula, auditar precisão técnica, verificar conformidade didática, checar diagramas Mermaid ou preparar material para publicação.
---

# Procedimento de Revisão Criteriosa de Aulas e Documentação

Este procedimento estabelece uma lista de checagem estruturada em 10 dimensões para validar e aprimorar a qualidade de materiais didáticos da disciplina **ENE0025 - Protocolos de Transporte e Roteamento (UnB)**.

---

## 1. As 10 Dimensões de Avaliação

O revisor deve avaliar o documento ponto a ponto:

| Dimensão | Critérios de Avaliação |
| :--- | :--- |
| **1. Correção Técnica** | Aderência estrita a RFCs da IETF, documentação de fabricantes (Cisco IOS, Linux, FRR) e conceitos acadêmicos consolidados. Conferir se não há alucinações técnicas ou comandos inventados. |
| **2. Didática e Clareza** | Progressão lógica do conteúdo (*Conceito $\rightarrow$ Funcionamento $\rightarrow$ Exemplo $\rightarrow$ Aplicação Prática*). Linguagem fluida, objetiva e adequada para nível universitário (graduação e pós). |
| **3. Estrutura Markdown** | Títulos hierárquicos sem saltos (H1 único, seguido de H2, H3), listas com indentação correta, tabelas alinhadas e ausência de HTML desnecessário. Formatação estrita em UTF-8. |
| **4. Consistência Terminológica** | Siglas explicadas na primeira menção, padronização de nomenclatura (ex.: interface `FastEthernet0/0` vs `Fa0/0`, consistência de nomes de nós `R1`, `SW1`, `PC1`). |
| **5. Qualidade dos Exemplos** | Cenários representativos, cálculos de sub-rede precisos, máscaras de rede consistentes e sem conflito de endereçamento. |
| **6. Diagramas Mermaid** | Sintaxe Mermaid válida sem erros de renderização, rótulos claros entre aspas quando contiverem caracteres especiais ou quebras de linha (`<br>`), legibilidade em tema claro e escuro. |
| **7. Comandos e Saídas** | Blocos de código com linguagem indicada (`cisco`, `bash`, `text`). Comandos funcionais e saídas condizentes com o comportamento real do software/emulador. |
| **8. Links e Referências** | URLs válidas para RFCs e materiais de apoio, links relativos corretos para arquivos do repositório (ex.: `images/` ou outros laboratórios). |
| **9. Triagem de Conteúdo Privado** | Verificar se há notas, gabaritos confidenciais, dados pessoais (LGPD), senhas reais ou credenciais que não deveriam estar expostas no material público. |
| **10. Prontidão para Publicação** | Remoção de quaisquer resquícios de rascunhos, anotações de aula inacabadas (`TODO`, `FIXME`) e eliminação de tom conversacional de chatbot. |

---

## 2. Diretrizes de Correção e Modificação

1. **Correções Seguras e Diretas:**
   - Corrigir diretamente erros ortográficos, concordância gramatical, quebras de sintaxe Markdown, nós desconectados no Mermaid e inconsistências de numeração.
2. **Dúvidas Técnicas e Pontos Ambíguos:**
   - **NÃO** alterar silenciosamente aspectos conceituais ou escolhas de arquitetura deliberadas pelo professor.
   - Quando houver ambiguidade técnica (ex.: escolha de parâmetro de temporização no OSPF ou métrica específica de BGP), documentar o ponto e consultar o usuário antes de alterar.
3. **Preservação de Conteúdo:**
   - Nunca encurtar ou remover explicações didáticas sem instrução expressa. Preservar o detalhamento necessário para a autonomia dos estudantes.
