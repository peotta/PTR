---
name: publicar-github
description: >-
  Fluxo controlado e seguro de staging, validação, commit e publicação de materiais didáticos no GitHub.
  Use quando o usuário solicitar preparar conteúdo para o GitHub, versionar arquivos, fazer staging, inspecionar diffs, criar commits ou publicar atualizações no repositório.
---

# Fluxo Seguro de Publicação no GitHub - ENE0025 (PTR)

Este procedimento estabelece os passos mandatórios para versionamento seguro, prevenindo a inclusão acidental de arquivos locais de preparação, dados privados, gabaritos e arquivos temporários.

---

## 1. Princípios Inegociáveis

1. **PROIBIÇÃO ABSOLUTA de Adição em Massa:**
   ```bash
   # NUNCA execute:
   git add .
   git add -A
   git commit -a
   ```
2. **Push Estritamente Sob Demanda:**
   - Criar ou editar arquivos **não autoriza** commit nem push.
   - O comando `git push` somente será executado se o usuário solicitar de maneira explícita (e.g., "faça o push das alterações").

---

## 2. Roteiro Operacional de Publicação

### Passo 1: Inspeção de Estado
Executar no terminal:
```bash
git status
```
Avaliar criticamente:
- Quais arquivos foram modificados?
- Quais arquivos aparecem em *Untracked files*?

### Passo 2: Verificação de Filtros e `.gitignore`
- Conferir se os arquivos não rastreados pertencem a pastas locais protegidas:
  - Pastas locais de apoio: `aulas/`, `material-aula/`, `rascunhos/`, `working/`, `temp/`, etc.
  - Avaliações e materiais confidenciais: `provas/`, `gabaritos/`, `notas/`, etc.
  - Temporários de escritório: `~$*.docx`, `~$*.pptx`, `~$*.xlsx`.
  - Credenciais ou chaves privadas.
- Se houver algum arquivo local sendo listado indevidamente no `git status`, atualizar primeiro o [.gitignore](file:///e:/Downloads/OneDrive%20-%20unb.br/ENE0025%20-%20PROTOCOLOS%20DE%20TRANSPORTE%20E%20ROTEAMENTO%20-%2060H/.gitignore) antes de prosseguir.

### Passo 3: Staging Explícito e Nominal
Adicionar **apenas** os arquivos finalizados e deliberadamente destinados ao repositório público do GitHub, nomeando cada caminho:
```bash
# Exemplos:
git add README.md
git add labs/lab14.md
git add images/topologia-bgp.png
```

### Passo 4: Auditoria do Staging (*Pre-Commit Check*)
Inspecionar exatamente o que está preparado para entrar no commit:
```bash
git diff --cached
```
Verificar:
- Nenhum dado pessoal, IP confidencial, chave ou senha exposta;
- Nenhuma alteração acidental em arquivos alheios ao escopo da tarefa;
- Formatação e integridade do Markdown.

### Passo 5: Criação do Commit
Registrar a alteração com mensagem semântica e contextualizada em português:
```bash
git commit -m "docs(labs): adiciona roteiro do Laboratorio 14 sobre BGP multihop"
```

### Passo 6: Publicação Remota (*Push*)
- Executar `git push` **SOMENTE** se o usuário deu autorização ou solicitação direta para publicar no GitHub:
```bash
git push origin main
```
- Reportar ao usuário os arquivos que foram enviados e a hash do commit gerado.
