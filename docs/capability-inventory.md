# Inventário de Capacidades — Echo

Tabela viva e rastreável. Atualizar quando o estado de uma capacidade mudar. Evidência obrigatória para estados "executado" e "validado para operação específica".

**Legenda de Estados:**
- **mencionado** — referenciado em documentação
- **definição encontrada** — arquivo/diretório de definição localizado
- **instalado** — disponível no ambiente
- **configurado** — parâmetros definidos (ex.: MCP, OAuth)
- **autenticado** — credenciais validadas pelo provedor
- **executado** — comando/operação rodou
- **validado para operação específica** — saída esperada confirmada
- **não verificado** — mencionado mas sem confirmação independente
- **falha observada** — teste/conexão falhou com contexto e data

---

## Agentes

| Nome | Finalidade | Estado | Operação Validada | Evidência | Data | Limitações | Público |
|------|------------|--------|-------------------|-----------|------|------------|---------|
| *Nenhum encontrado* | — | não verificado | — | Busca em `.claude/agents/` e `~/.claude/agents/` (diretórios inexistentes) | 2026-11-06 | Podem existir em outros locais não consultados | Não |

---

## Skills

| Nome | Finalidade | Estado | Operação Validada | Evidência | Data | Limitações | Público |
|------|------------|--------|-------------------|-----------|------|------------|---------|
| graphify | Knowledge graph de codebases/docs | definição encontrada; instalada | — | Diretório `.claude/skills/graphify/` existe; referenciado em CLAUDE.md | 2026-11-06 | Backend histórico não confirmado; execução não verificada | Sim |
| gws-admin-reports | Audit logs e usage reports | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-calendar | Gerenciar calendários/eventos | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-calendar-agenda | Próximos eventos | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-calendar-insert | Criar evento | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-chat | Gerenciar Chat spaces/mensagens | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-chat-send | Enviar mensagem | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-classroom | Gerenciar classes/rosters | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-docs | Ler/escrever Google Docs | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-docs-write | Anexar texto a Doc | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-drive | Gerenciar Drive | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-drive-upload | Upload com metadata | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-events | Subscrever eventos Workspace | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-events-renew | Renovar subscrições | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-events-subscribe | Subscrever/stream eventos | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-forms | Ler/escrever Forms | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-gmail | Gmail: send, read, manage | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado diretamente | Sim |
| gws-gmail-forward | Forward message | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-gmail-read | Ler mensagem | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-gmail-reply | Responder (threading) | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-gmail-reply-all | Reply-all (threading) | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-gmail-send | Enviar email | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-gmail-triage | Resumo inbox não lido | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-gmail-watch | Watch novos emails | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-keep | Gerenciar Keep notes | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-meet | Gerenciar Meet | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-modelarmor | Filtrar conteúdo | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-modelarmor-create-template | Criar template Model Armor | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-modelarmor-sanitize-prompt | Sanitizar prompt | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-modelarmor-sanitize-response | Sanitizar resposta | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-people | Gerenciar contatos/perfis | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-script | Gerenciar Apps Script | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-script-push | Upload para Apps Script | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-shared | Padrões compartilhados gws | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-sheets | Ler/escrever Sheets | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-sheets-append | Anexar linha | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-sheets-read | Ler valores | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-slides | Ler/escrever Slides | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-tasks | Gerenciar Tasks | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-workflow | Workflows cross-service | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-workflow-email-to-task | Gmail → Task | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-workflow-file-announce | Drive → Chat | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-workflow-meeting-prep | Prep reunião | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-workflow-standup-report | Standup summary | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| gws-workflow-weekly-digest | Weekly summary | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| persona-content-creator | Criar/distribuir conteúdo | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| persona-customer-support | Gerenciar suporte | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| persona-event-coordinator | Planejar eventos | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| persona-exec-assistant | Agenda/executivo | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| persona-hr-coordinator | Workflows RH | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| persona-it-admin | Admin IT | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| persona-project-manager | Coordenar projetos | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| persona-researcher | Organizar pesquisa | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| persona-sales-ops | Workflows vendas | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| persona-team-lead | Liderar equipe | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-backup-sheet-as-csv | Export Sheet → CSV | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-batch-invite-to-event | Convidar em lote | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-block-focus-time | Blocos de foco | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-bulk-download-folder | Download pasta Drive | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-collect-form-responses | Coletar respostas Form | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-compare-sheet-tabs | Comparar abas Sheet | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-copy-sheet-for-new-month | Duplicar aba p/ mês | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-create-classroom-course | Criar curso Classroom | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-create-doc-from-template | Doc de template | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-create-events-from-sheet | Sheet → Calendar | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-create-expense-tracker | Tracker despesas | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-create-feedback-form | Criar Form feedback | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-create-gmail-filter | Criar filtro Gmail | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-create-meet-space | Criar Meet space | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-create-presentation | Criar Slides | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-create-shared-drive | Criar Shared Drive | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-create-task-list | Criar lista Tasks | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-create-vacation-responder | Out-of-office Gmail | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-draft-email-from-doc | Doc → email body | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-email-drive-link | Compartilhar Drive + email | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-find-free-time | Free/busy Calendar | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-find-large-files | Arquivos grandes Drive | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-forward-labeled-emails | Forward por label | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-generate-report-from-sheet | Sheet → Doc report | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-label-and-archive-emails | Label + archive | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-log-deal-update | Log deal no Sheet | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-organize-drive-folder | Organizar Drive | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-plan-weekly-schedule | Planejar semana | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-post-mortem-setup | Post-mortem setup | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-reschedule-meeting | Remarcar + notificar | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-review-meet-participants | Review participantes | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-review-overdue-tasks | Tasks vencidas | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-save-email-attachments | Salvar anexos Drive | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-save-email-to-doc | Email → Doc | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-schedule-recurring-event | Evento recorrente | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-send-team-announcement | Anúncio Gmail + Chat | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-share-doc-and-notify | Share Doc + notify | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-share-event-materials | Share Drive p/ attendees | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-share-folder-with-team | Share folder + team | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-sync-contacts-to-sheet | Contacts → Sheet | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| recipe-watch-drive-changes | Watch mudanças Drive | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| competitive-ads-extractor | Extrair anúncios concorrentes | definição encontrada; instalada | — | Diretório existe | 2026-11-06 | Não executado | Sim |
| using-agent-skills | Meta-skill: descobrir/invocar skills | instalada; executada | Identificação de skill para tarefa Python CSV→JSON | Skill invocada; fluxo incremental-implementation identificado | 2026-11-06 | Meta-skill; 79 agentes mapeados | Sim |
| humanizer | Reescrever texto removendo padrões IA | instalada; executada | Reescrita de parágrafo sintético com tells de IA | Tells identificados/removidos: §1,§2,§3,§4,§12,§13,§16 | 2026-11-06 | Processo manual guiado por skill | Sim |
| find-skills | Buscar skills sem instalar | instalada; executada | `npx skills find python csv` → resultados | Resultados retornados (xlsx, markitdown, etc.) sem instalação | 2026-11-06 | Busca apenas; não instala | Sim |
| caveman-compress | Comprimir arquivos markdown | instalada; executada | Compressão de test-caveman.md | Código/comandos/termos preservados; linguagem natural comprimida | 2026-11-06 | Backup em diretório out-of-tree; dados saem da máquina | Sim |
| superpowers:brainstorming | Exploração estruturada | mencionado em documentação | — | CLAUDE.md do projeto | 2026-11-06 | Definição local não encontrada | Sim |
| superpowers:systematic-debugging | Diagnóstico rigoroso | mencionado em documentação | — | CLAUDE.md do projeto | 2026-11-06 | Definição local não encontrada | Sim |
| superpowers:verification-before-completion | Evidência antes de concluir | mencionado em documentação | — | CLAUDE.md do projeto | 2026-11-06 | Definição local não encontrada | Sim |
| superpowers:using-superpowers | Como usar skills | mencionado em documentação | — | CLAUDE.md do projeto | 2026-11-06 | Definição local não encontrada | Sim |
| superpowers:writing-plans | Planejar antes de codar | mencionado em documentação | — | CLAUDE.md do projeto | 2026-11-06 | Definição local não encontrada | Sim |
| superpowers:executing-plans | Executar planos | mencionado em documentação | — | CLAUDE.md do projeto | 2026-11-06 | Definição local não encontrada | Sim |
| superpowers:receiving-code-review | Receber code review | mencionado em documentação | — | CLAUDE.md do projeto | 2026-11-06 | Definição local não encontrada | Sim |
| superpowers:requesting-code-review | Pedir code review | mencionado em documentação | — | CLAUDE.md do projeto | 2026-11-06 | Definição local não encontrada | Sim |
| superpowers:subagent-driven-development | Dev com subagents | mencionado em documentação | — | CLAUDE.md do projeto | 2026-11-06 | Definição local não encontrada | Sim |
| superpowers:dispatching-parallel-agents | Paralelismo | mencionado em documentação | — | CLAUDE.md do projeto | 2026-11-06 | Definição local não encontrada | Sim |
| superpowers:using-git-worktrees | Git worktrees | mencionado em documentação | — | CLAUDE.md do projeto | 2026-11-06 | Definição local não encontrada | Sim |
| superpowers:finishing-a-development-branch | Finalizar branch | mencionado em documentação | — | CLAUDE.md do projeto | 2026-11-06 | Definição local não encontrada | Sim |
| superpowers:test-driven-development | TDD | mencionado em documentação | — | CLAUDE.md do projeto | 2026-11-06 | Definição local não encontrada | Sim |
| superpowers:brainstorming | (duplicata) | mencionado em documentação | — | CLAUDE.md do projeto | 2026-11-06 | Definição local não encontrada | Sim |
| superpowers:diagnosing-superpowers | Debug superpowers | mencionado em documentação | — | CLAUDE.md do projeto | 2026-11-06 | Definição local não encontrada | Sim |
| superpowers:writing-skills | Criar/editar skills | mencionado em documentação | — | CLAUDE.md do projeto | 2026-11-06 | Definição local não encontrada | Sim |
| superpowers:loop | Recorrência | mencionado em documentação | — | CLAUDE.md do projeto | 2026-11-06 | Definição local não encontrada | Sim |
| superpowers:fewer-permission-prompts | Reduzir prompts | mencionado em documentação | — | CLAUDE.md do projeto | 2026-11-06 | Definição local não encontrada | Sim |

**Total de entradas de skills:** 90 (86 originais + 4 Lote 1). **Não equivale a 90 capacidades operacionais.** Diretório encontrado ≠ definição inspecionada ≠ execução ≠ validação. Execução das skills não comprovada pelas fontes consultadas.

---

## Integrações

| Nome | Tipo | Finalidade | Estado | Operação Validada | Evidência | Data | Limitações | Público |
|------|------|------------|--------|-------------------|-----------|------|------------|---------|
| gh CLI | CLI + API | GitHub ops, auth, credential helper | autenticado; executado; push HTTPS funcionou | `git push origin master` | commit b30257f; `gh auth status` | 2026-11-06 | Token no keyring; helper via `gh auth setup-git` | Sim |
| gws CLI | CLI + OAuth | Google Workspace (Gmail) | autenticado; executado; consulta de rótulos documentada | `gws gmail users labels list` | Estudo de caso 01 | 2026-11-06 | `gmail.modify` não verificado; outros serviços não testados | Sim |
| git | CLI | Versionamento | executado; push funcionou | commit + push | Histórico Git | 2026-11-06 | Dependente de gh credential helper | Sim |

---

## Memória

O projeto utiliza memória operacional em arquivos Markdown para continuidade entre sessões: estado atual, decisões técnicas e resumos de sessão. O mecanismo de carregamento é explícito (não automático) e a memória reside fora do repositório público.

---

## Automações

| Nome | Problema | Solução | Estado | Evidência | Resultado | Próximo Teste | Público |
|------|----------|---------|--------|-----------|-----------|---------------|---------|
| Publicação Echo | Publicar portfólio controlado | git add individual + commit + push via gh | implementada; validada | commit b30257f + push | Repo público operacional | Próxima publicação | Sim |
| Limpeza Gmail | Triagem diária inbox | Script PS + labels custom + agendador | planejada | JOURNAL.md | — | Criar labels; script -DryRun; Task Scheduler | Não |

---

## Notas de Atualização

- **2026-11-06:** Inventário inicial criado a partir de leitura autorizada de definições locais, `.mcp.json` e memória de projeto.
- **2026-11-06:** Lote 1 concluído — 4 skills instaladas e testadas: using-agent-skills (meta-skill), humanizer (reescrita), find-skills (busca), caveman-compress (compressão). Todas executadas com evidência.
- Próxima atualização: após verificação de `gmail.modify`, instalação de hooks, ou Lote 2.