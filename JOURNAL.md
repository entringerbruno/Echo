# Linha do Tempo de Marcos — Jornada Técnica

> **Legenda de Status**
> - **Implementado** — código/execução realizada e verificada
> - **Testado** — executado com validação de saída esperada
> - **Planejado** — definido, aguarda execução ou aprovação
> - **Relatado** — informado pelo autor, sem verificação independente
> - **Não verificado** — mencionado, mas sem confirmação independente

---

## Marcos — Datas Verificáveis

- **Relatado:** Estruturação do ambiente local privado com memórias operacionais (`ESTADO.md`, `DECISOES.md`, `SESSOES.md`).
- **Relatado:** Início do uso de Graphify para extração de grafo de conhecimento a partir de documentos locais.
- **Relatado:** Configuração de ambiente de desenvolvimento local com PowerShell, ferramentas CLI e integração com provedores de IA via SDK.
- **Implementado:** Autenticação inicial do Google Workspace CLI (`gws`) — escopo concedido não inspecionado.
- **Testado:** Consulta de rótulos do Gmail via `gws gmail users labels list` — retorno JSON validado (INBOX, SENT, STARRED, IMPORTANT, etc.) — documentado no estudo de caso 01.
- **Planejado:** Ampliação de escopo para `gmail.modify` para operações de escrita futura.
- **Relatado:** Autorização concedida para escopo `gmail.modify` via fluxo OAuth do navegador; concessão não inspecionada.
- **Relatado:** Confirmação de conta ativa e escopos concedidos via resposta da API; detalhes não registrados.
- **Planejado:** Desenho da automação de triagem e limpeza diária do Gmail (script PowerShell, rótulos customizados, agendador de tarefas do sistema às 03:00 BRT, limite 10 msgs/execução).
- **Planejado:** Criação dos rótulos `"Atenção verificar"` e `"Manter"` no Gmail.
- **Planejado:** Script `gmail-cleanup.ps1` com modo simulação (`-DryRun`) e envio de resumo de reprovações por e-mail.
- **Planejado:** Registro da tarefa agendada (ex.: `<ambiente-privado>\Gmail-Daily-Cleanup`) no agendador de tarefas do sistema.
- **Implementado:** Estruturação inicial do portfólio técnico local publicada como Echo (commit `b30257f`).
- **Testado:** Verificação de ausência de identificadores pessoais e segredos nos arquivos gerados — triagem por padrões, não prova de ausência absoluta (2026-11-06).
- **Concluído:** Revisão e aprovação dos 5 arquivos iniciais; `git init`, commit e push realizados (2026-11-06).

---

## Próximos Marcos (Sujeitos a Aprovação)

1. Inventário completo de agentes, skills e integrações MCP (acesso a definições locais autorizado).
2. Verificação de `gmail.modify` — teste de escrita controlada com aprovação.
3. Instalação de hooks de segredos (`detect-secrets` + `pre-commit`).
4. Publicação de `docs/architecture.md` e `docs/decisions.md`.
5. Estudo de caso #2: ambiente seguro / diagnóstico de gateways (dados sintéticos).

---

## 2026-11-06 — Publicação Inicial do Echo (commit b30257f)

**Objetivo:** Estabelecer repositório público do portfólio Echo com estrutura base, política de segurança e primeiro estudo de caso.

**Mudança realizada:**
- Criados 5 arquivos iniciais: `.gitignore`, `JOURNAL.md`, `README.md`, `SECURITY_POLICY.md`, `case-studies/01-gws-cli-oauth.md`
- Revisão por padrões de segurança prévia: referências a nomes internos de ambiente privado, caminhos absolutos e referências a agendador específico substituídas por placeholders genéricos
- A verificação por padrões é uma triagem, não prova de ausência absoluta de segredos

**Integrações envolvidas na publicação:**
- `gh` CLI — autenticação, credential helper para git (validado para push HTTPS)
- `git` — commit e push via HTTPS

**Decisão e justificativa:**
- Separar fisicamente vault privado (memórias operacionais, identidades profissionais, configurações MCP) do portfólio público
- Lista explícita de arquivos publicáveis — sem `git add .` — para controle total
- Credential helper via `gh auth setup-git` usa token no keyring do SO; evita gestão de chaves SSH

**Teste/Evidência:**
- `git status` → clean
- `git log --oneline -1` → `b30257f docs: commit inicial — estrutura do portfólio Echo`
- `git push origin master` → Sucesso após `gh auth setup-git`
- `gh auth status` → Logged in as `entringerbruno` (keyring), escopos `repo`, `gist`, `read:org`

**Resultado:** Repositório público operacional em `https://github.com/entringerbruno/Echo`.

**Limitações:**
- Escopo `gmail.modify` relatado como aprovado no fluxo OAuth; concessão não inspecionada programaticamente
- Hooks de segredos (`detect-secrets`/`git-secrets`) mencionados na política mas não instalados
- Agentes customizados não encontrados; 86 diretórios de skills encontrados; execução das skills não comprovada pelas fontes consultadas
- MCP Obsidian: `ECONNREFUSED` observado — não operacional
- Verificação de segredos por padrões: triagem, não prova de ausência absoluta

**Próximo passo:** Inventário completo de capacidades (agentes, skills, integrações MCP) com autorização para acessar definições locais.

**Referência:** Commit `b30257f8014bf0da7957fa9b455031320c65d220`

---

## 2026-11-06 — Inventário Limitado de Capacidades (Esta Sessão)

**Objetivo:** Mapear agentes, skills, integrações e memória para fundamentar a estrutura editorial do Echo.

**Mudança realizada:**
- Leitura de definições locais: 86 diretórios de skills em `.claude/skills/` (graphify, gws-*, persona-*, recipe-*, competitive-ads-extractor); arquivos de definição não inspecionados individualmente; nenhum diretório de agentes customizados encontrado
- Leitura de `.mcp.json`: 2 servidores configurados (Obsidian HTTP local, Supabase HTTP remoto)
- Leitura de memória operacional: registros privados de estado, decisões e sessões, regra de retomada `verify-working-dir-before-concluding`
- Classificação por estados separados: mencionado, definição encontrada, instalado, configurado, autenticado, executado, validado para operação específica, não verificado, falha observada

**Integrações consultadas (somente leitura):**
- Sistema de arquivos local (definições de skills, configuração MCP, memória)
- Git/GitHub (estado do repositório, credential helper)

**Decisão e justificativa:**
- Usar estados granulares para evitar confundir instalação com execução ou validação
- Registrar apenas operações com evidência direta (ex.: `gws gmail labels list` documentado no estudo de caso anterior, não reexecutado)
- Não testar conexões MCP nem inspecionar tokens nesta etapa

**Resultado:** Inventário parcial documentado; base para `docs/capability-inventory.md`.

**Limitações:**
- Acesso apenas a diretórios autorizados; agentes podem existir em outros locais não consultados
- Skills `superpowers:*` referenciadas mas sem definição local visível
- Conexões MCP não testadas; status baseado apenas em configuração e falha observada anterior

**Próximo passo:** Publicar `docs/capability-inventory.md` com tabela viva rastreável.

---

## 2026-11-06 — Reestruturação Editorial do Echo (Esta Sessão)

**Objetivo:** Implementar estrutura editorial aprovada: README enxuto, diário atualizado, política corrigida, estudo de caso ajustado, três documentos técnicos novos.

**Mudança realizada:**
- README reescrito: foco em problema/estado/evidência; catálogo movido para inventário
- JOURNAL atualizado: marcos corrigidos, entradas datadas separadas por publicação/inventário/editorial
- SECURITY_POLICY: "Scan de segredos pré-commit" alterado para "planejado — não instalado"; linguagem de certeza substituída por controles observados + limitações
- Estudo de caso 01: "Confirmado: escopo modify concedido" → "Relatado: aprovação OAuth; concessão não inspecionada"; referência ambígua a vault generalizada
- Criados: `docs/architecture.md`, `docs/capability-inventory.md`, `docs/decisions.md`
- Memória privada `echo-private-memory.md` criada/atualizada fora do repositório

**Decisão e justificativa:**
- Seguir aprovação condicionada: sem inventário de tudo que existe na máquina, apenas itens pertinentes ao Echo
- Separar conceito público de configuração privada nos documentos técnicos
- Manter histórico real; não apagar pendências concluídas

**Teste/Evidência:**
- Verificação de Markdown: links relativos, tabelas padrão, blocos fechados, Mermaid válido
- Triagem de segredos: nenhum padrão sensível detectado nos 7 arquivos
- Memória privada não incluída no conjunto público

**Limitações:**
- Inventário de skills baseado em nomes de diretórios; arquivos de definição não inspecionados individualmente; execução das skills não comprovada pelas fontes consultadas
- MCP Supabase: parâmetro read-only na URL não garante acesso efetivo
- Retomada entre sessões depende de carregamento explícito da memória privada (mecanismo não automático universal)

**Próximo passo:** Revisão humana dos 7 arquivos; autorização para commit e push.

**Referência:** Pendente — aguarda commit.

---

## 2026-11-06 — Lote 1: Instalação e Validação de Skills (Esta Sessão)

**Objetivo:** Instalar e testar 4 skills do catálogo: Agent Skills (Addy Osmani), Humanizer, find-skills (vercel-labs), Caveman (concisão).

**Mudança realizada:**
- `npm install -g skills` → CLI instalado
- `skills add addyosmani/agent-skills@using-agent-skills` → meta-skill instalada
- `skills add blader/humanizer@humanizer` → skill de reescrita instalada
- `skills add vercel-labs/skills@find-skills` → skill de busca instalada
- `skills add juliusbrussee/caveman@caveman-compress` → skill de compressão instalada
- Cada skill testada com tarefa mínima e evidência registrada

**Testes executados:**
| Item | Versão/Revisão | Método/Escopo | Teste | Resultado | Pendência |
|------|----------------|---------------|-------|-----------|-----------|
| Agent Skills | addyosmani/agent-skills@using-agent-skills | skills add | Identificar skill para tarefa Python CSV→JSON | incremental-implementation identificado | — |
| Humanizer | v3.1.0 (blader/humanizer) | skills add | Reescrever parágrafo sintético com tells IA | 11 tells removidos (§1,§2,§3,§4,§12,§13,§16) | — |
| find-skills | vercel-labs/skills@find-skills | skills add | `npx skills find python csv` | Resultados retornados (xlsx, markitdown, etc.) sem instalar | — |
| Caveman compress | juliusbrussee/caveman@caveman-compress | skills add | Comprimir test-caveman.md | Código/comandos/termos preservados; linguagem comprimida | — |

**Integrações envolvidas:**
- `skills` CLI (npm) — instalação e gerenciamento
- GitHub (source dos repositórios de skills)
- Python 3.11.9 — execução do script de compressão do Caveman

**Decisão e justificativa:**
- Usar skills CLI oficial para instalação rastreável
- Testar cada skill com tarefa mínima antes de considerar "instalada"
- Documentar evidência concreta, não apenas instalação

**Resultado:** 4 skills instaladas e validadas; `docs/capability-inventory.md` atualizado com 4 novas entradas (total 90).

**Limitações:**
- Agent Skills é meta-skill; não executa código diretamente
- Humanizer requer aplicação manual das regras (não automatizado)
- find-skills apenas busca; não instala resultados
- Caveman-compress envia dados ao provedor de modelo (claude); backup out-of-tree

**Próximo passo:** Lote 2 — UI UX Pro Max, emilkowalski/skills, Impeccable, design-taste-frontend (Leonxlnx).

**Referência:** Commits pendentes — aguarda revisão e push.