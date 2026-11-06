# Decisões Técnicas — Echo

Formato leve de ADR (Architecture Decision Record). Registrar decisões tomadas e propostas em aberto.

---

## Decisões Históricas (Já Tomadas)

### ADR-001: Separação Física de Diretórios (Vault ↔ Portfolio)
- **Status:** Aceita
- **Data:** 2026-11-06
- **Contexto:** Necessidade de publicar portfólio público sem expor ambiente privado (memórias, identidades, configs, credenciais).
- **Decisão:** Dois diretórios físicos separados: ambiente privado e `portfolio-tech/` (público, publicado como Echo).
- **Alternativas:** Monorepo com `.gitignore` agressivo; subdiretório `public/` dentro do ambiente privado.
- **Trade-offs:** Reduz exposição acidental; exige disciplina manual a cada publicação (lista explícita).
- **Consequências:** Requer `git add` individual; procedimento de publicação documentado.
- **Referência:** Commit `b30257f`; `SECURITY_POLICY.md`; `JOURNAL.md` (2026-11-06).

---

### ADR-002: Lista Explícita de Arquivos — Sem `git add .`
- **Status:** Aceita
- **Data:** 2026-11-06
- **Contexto:** Risco de vazar arquivos privados, credenciais, caminhos absolutos via `git add .` ou `git add -A`.
- **Decisão:** Apenas arquivos listados explicitamente entram no repositório. Cada publicação usa `git add <arquivo1> <arquivo2> ...`.
- **Alternativas:** `git add .` + `.gitignore` abrangente; `git add -u` para modificados.
- **Trade-offs:** Controle do que entra no repositório; mais passos manuais; risco de esquecer arquivo novo.
- **Consequências:** Checklist de publicação; revisão humana obrigatória.
- **Referência:** Commit `b30257f`; `SECURITY_POLICY.md`.

---

### ADR-003: Credential Helper via `gh` (HTTPS + Keyring do SO)
- **Status:** Aceita
- **Data:** 2026-11-06
- **Contexto:** Push via HTTPS falhou com auth por senha; `gh auth setup-git` configurou helper para usar token no keyring do SO.
- **Decisão:** Usar `gh` CLI como credential helper para Git (HTTPS). Token armazenado no keyring do sistema operacional.
- **Alternativas:** SSH keys; Personal Access Token em variável de ambiente; Git Credential Manager standalone.
- **Trade-offs:** Evita chaves SSH separadas; integração nativa com `gh`; depende de `gh` instalado e autenticado.
- **Consequências:** `git push` funciona via HTTPS; `gh auth status` confirma escopos.
- **Referência:** Commit `b30257f`; `JOURNAL.md` (2026-11-06 — resolução de auth).

---

### ADR-004: Dados Sintéticos Obrigatórios
- **Status:** Aceita
- **Data:** 2026-11-06
- **Contexto:** Exemplos reais (emails, paths, IDs) vazam informações sensíveis.
- **Decisão:** Todos os exemplos em documentos públicos devem usar dados sintéticos claramente identificáveis (`user@example.com`, `Empresa X`, `AKIA...EXAMPLE`, `<diretório-privado-local>`).
- **Alternativas:** Anonimização pós-escrita; redacção manual.
- **Trade-offs:** Reduz risco de vazamento por construção; requer disciplina do autor; menos "realista" visualmente.
- **Consequências:** Revisão por padrões antes de publish; placeholders padronizados.
- **Referência:** `SECURITY_POLICY.md`; sanitização pré-commit `b30257f`.

---

### ADR-005: Memória Operacional em Markdown
- **Status:** Aceita
- **Data:** 2026-11-05
- **Contexto:** Necessidade de continuidade entre sessões sem depender de banco de dados ou vector store.
- **Decisão:** Três arquivos Markdown no ambiente privado: estado atual, decisões, resumos de sessão. Sem plugins, hooks ou ferramentas automáticas.
- **Alternativas:** SQLite local; JSON files; Vector DB; Plugin Obsidian.
- **Trade-offs:** Legível, versionável, portável, diffável; sem query semântica nativa; carregamento manual.
- **Consequências:** Procedimento de retomada documentado; regra `verify-working-dir-before-concluding` criada.
- **Referência:** Decisões e sessões registradas.

---

### ADR-006: Não Instalar Plugins/Hooks/Ferramentas para Memória
- **Status:** Aceita
- **Data:** 2026-11-05
- **Contexto:** Decisão ADR-005 estabeleceu arquivos Markdown; automatização adicionaria complexidade e superfície de falha.
- **Decisão:** Manter memória como arquivos passivos. Leitura/escrita explícita pelo agente a cada sessão.
- **Alternativas:** Hook `pre-commit` para atualizar `ESTADO.md`; script de sincronização; plugin Obsidian.
- **Trade-offs:** +Simplicidade; +Controle; -Dependência de disciplina humana.
- **Consequências:** Agente deve ler `ESTADO.md` + `JOURNAL.md` + `git status` no início.
- **Referência:** registro privado de decisões.

---

### ADR-007: Estados Granulares para Capacidades (9 Categorias)
- **Status:** Aceita
- **Data:** 2026-11-06
- **Contexto:** Conflar "instalado", "configurado", "autenticado", "executado", "validado" escondia lacunas (ex.: skill instalada ≠ executada).
- **Decisão:** Classificar cada capacidade em: mencionado, definição encontrada, instalado, configurado, autenticado, executado, validado para operação específica, não verificado, falha observada.
- **Alternativas:** Escala única (disponível/validado); binário (sim/não).
- **Trade-offs:** +Precisão; +Rastreabilidade; -Mais verboso.
- **Consequências:** `docs/capability-inventory.md` usa esta taxonomia; atualização obrigatória em mudança de estado.
- **Referência:** `docs/capability-inventory.md`; `JOURNAL.md` (2026-11-06 — inventário).

---

## Propostas em Aberto (Não Decididas)

### PROP-001: Instalar Hooks `detect-secrets` + `pre-commit`
- **Status:** Proposta
- **Data:** 2026-11-06
- **Contexto:** `SECURITY_POLICY.md` menciona scan de segredos pré-commit mas não há hook instalado.
- **Proposta:** Adicionar `detect-secrets` + `pre-commit` ao repositório; validar em commit de teste.
- **Alternativas:** `git-secrets`; scan manual em CI; scan manual local.
- **Trade-offs:** +Automatiza triagem; -Falsos positivos/negativos; -Dependência extra; -Não substitui revisão humana.
- **Próximo passo:** Aprovação para instalar e testar.

---

### PROP-002: Verificar `gmail.modify` via Teste Controlado
- **Status:** Proposta
- **Data:** 2026-11-06
- **Contexto:** Escopo `gmail.modify` relatado como aprovado no fluxo OAuth; concessão não inspecionada.
- **Proposta:** Executar operação de escrita controlada (ex.: aplicar label a uma mensagem de teste) com aprovação prévia; confirmar sucesso.
- **Alternativas:** Inspecionar token OAuth (não autorizado); assumir concedido baseado no relato.
- **Trade-offs:** +Evidência direta; -Requer execução real; -Risco de alteração indesejada (mitigado por mensagem de teste + aprovação).
- **Próximo passo:** Definir mensagem de teste + label temporária; aprovação para executar.

---

### PROP-003: Estudo de Caso #2 — Ambiente Seguro / Diagnóstico Gateways
- **Status:** Proposta
- **Data:** 2026-11-06
- **Contexto:** Próximo marco do roadmap; demonstrar capacidade além de OAuth Gmail.
- **Proposta:** Criar estudo de caso com dados sintéticos documentando arquitetura de ambiente seguro ou diagnóstico de gateways/modelos.
- **Alternativas:** Outro estudo de caso (ex.: automação Drive, Sheets); pular para estudo #3.
- **Trade-offs:** +Demonstra profundidade; -Requer design e execução; -Dados sintéticos bem feitos levam tempo.
- **Próximo passo:** Definir escopo e aprovar.

---

### PROP-004: Mecanismo de Carregamento de Memória Privada
- **Status:** Proposta
- **Data:** 2026-11-06
- **Contexto:** Memória privada `echo-private-memory.md` existe mas carregamento não é automático universal.
- **Proposta:** Adicionar referência no `CLAUDE.md` do projeto (vault) para instruir leitura no início de sessão no Echo.
- **Alternativas:** Skill de carregamento; hook de sessão; instrução manual a cada vez.
- **Trade-offs:** +Reduz esquecimento; -Modifica CLAUDE.md do projeto; -Não garante carregamento em todos os contextos (ex.: sessões sem projeto).
- **Próximo passo:** Aprovação para editar `CLAUDE.md` do vault.

---

## Registro de Substituições

*Nenhuma substituição até o momento. Decisões iniciais mantidas.*