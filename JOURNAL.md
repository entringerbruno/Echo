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

**Objetivo:** Instalar e testar 4 skills do catálogo: Agent Skills (Addy Osmani), Humanizer, find-skills (vercel-labs), Caveman (compressão de arquivos Markdown).

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
| Caveman compress | juliusbrussee/caveman@caveman-compress | skills add | Comprimir test-caveman.md | Compressão relatada; arquivo de entrada não confirmado; não valida skill de concisão solicitada | Novas execuções de compressão suspensas |

**Integrações envolvidas:**
- `skills` CLI (npm) — instalação e gerenciamento
- GitHub (source dos repositórios de skills)
- Python 3.11.9 — execução do script de compressão do Caveman

**Decisão e justificativa:**
- Usar skills CLI oficial para instalação rastreável
- Testar cada skill com tarefa mínima antes de considerar "instalada"
- Documentar evidência concreta, não apenas instalação
- Caveman: finalidade compressão de arquivos Markdown; instalada; teste de compressão relatado; arquivo de entrada não confirmado; não valida skill de concisão solicitada; novas execuções suspensas

**Resultado:** 4 skills instaladas; 3 validadas para objetivo solicitado; `docs/capability-inventory.md` atualizado com 4 novas entradas (total 90).

**Limitações:**
- Agent Skills é meta-skill; não executa código diretamente
- Humanizer requer aplicação manual das regras (não automatizado)
- find-skills apenas busca; não instala resultados
- Caveman-compress: teste de compressão de arquivo sintético executado (test-caveman.md, Python 3.11.9); backup out-of-tree; dados saem da máquina; autorização só para concisão de saída — novas execuções de compressão suspensas

**Próximo passo:** Lote 2 — UI UX Pro Max, emilkowalski/skills, Impeccable, design-taste-frontend (Leonxlnx).

**Referência:** Commits pendentes — aguarda revisão e push.

---

## 2026-11-06 — Lote 2: Instalação de Skills (Esta Sessão)

**Objetivo:** Instalar 4 skills do catálogo: UI UX Pro Max, emil-design-eng (emilkowalski/skills), Impeccable, design-taste-frontend.

**Mudança realizada:**
- `skills add emilkowalski/skills@emil-design-eng` → skill instalada
- `skills add ui-ux-pro-max@ui-ux-pro-max` → skill instalada
- `skills add impeccable@impeccable` → skill instalada (alerta "Socket")
- `skills add design-taste-frontend@design-taste-frontend` → skill instalada (alerta "Critical Risk")

**Testes executados:**
| Item | Versão/Revisão | Método/Escopo | Teste | Resultado | Pendência |
|------|----------------|---------------|-------|-----------|-----------|
| UI UX Pro Max | tasteskill local | skills add | Busca `--design-system` / `--domain ux` | Resultado gerado com tabela de revisão | — |
| emil-design-eng | emilkowalski/skills | skills add | Review de CSS de botão | Orientação produzida (tabela Before/After) | — |
| Impeccable | impeccable | skills add | Não executado | Socket alert relatado no instalador | Identificar causa do alerta |
| design-taste-frontend | tasteskill 2.5.0 | skills add | Não executado | Critical Risk relatado no instalador | Identificar causa do alerta |

**Integrações envolvidas:**
- `skills` CLI (npm) — instalação e gerenciamento
- GitHub (source dos repositórios de skills)

**Decisão e justificativa:**
- Usar skills CLI oficial para instalação rastreável
- Testar skills independentes (UI UX Pro Max, emil-design-eng) com tarefas mínimas
- Suspender teste de Impeccable e design-taste-frontend até esclarecer alertas de instalação (alertas com rótulos diferentes; causas não identificadas)
- Corrigir registro do caveman-compress: finalidade compressão de arquivos Markdown; não valida concisão de respostas

**Resultado:** 4 skills instaladas; 2 testadas com evidência; 2 com teste suspenso por alerta; `docs/capability-inventory.md` atualizado com 4 novas entradas (total 94).

**Limitações:**
- Impeccable e design-taste-frontend: alertas de instalador não identificados; execução não validada
- UI UX Pro Max e emil-design-eng: busca/orientação executada; não validação visual de interface real
- Caveman-compress: apenas concisão de saída autorizada; compressão de arquivo não testada nem autorizada

**Próximo passo:** Identificar causa dos alertas "Socket" e "Critical Risk"; Lote 3 — Puppeteer, FFmpeg (se necessário), HyperFrames.

**Referência:** Commits pendentes — aguarda revisão e push.

---

## 2026-11-11 — Lote 3: Instalação e Validação de Ferramentas (Esta Sessão)

**Objetivo:** Instalar e testar 3 ferramentas: Puppeteer (browser automation), FFmpeg/ffprobe (encoding/probing vídeo), HyperFrames (HTML/GSAP → MP4).

**Mudança realizada:**
- `npm install puppeteer` em projeto isolado `/tmp/puppeteer-test`
- `winget install --id Gyan.FFmpeg` → FFmpeg 9.0.2 full build (Gyan)
- `npx hyperframes init hyperframes-test` → projeto HyperFrames v0.9.36 criado
- Composição HTML/GSAP 3s criada em `index.html` (título, subtítulo, barra animada)
- `npx hyperframes render -o hyperframes-3s.mp4` → render MP4

**Testes executados:**
| Item | Versão/Revisão | Método/Escopo | Teste | Resultado | Pendência |
|------|----------------|---------------|-------|-----------|-----------|
| Puppeteer | 23.x (npm) | npm install | Projeto isolado; HTML sintético com título "Puppeteer Synthetic Test"; screenshot fullPage | `screenshot.png` gerado; execução sem `--no-sandbox` | — |
| FFmpeg/ffprobe | 9.0.2 (Gyan) | winget | Clipe sintético 2s (testsrc 640×480@30 + sine 440Hz) → `synthetic-2s.mp4` | ffprobe: vídeo 2,0s 640×480@30; áudio 2,0s 44.1kHz mono | — |
| HyperFrames | 0.9.36 (npm) | npx hyperframes | Init + composição HTML/GSAP 3s (fade/slide/width) → render | `hyperframes-3s.mp4` 1920×1080@30, 3,0s; ffprobe validado | — |

**Integrações envolvidas:**
- `npm` — instalação de Puppeteer e HyperFrames
- `winget` — instalação de FFmpeg (Gyan build)
- FFmpeg/ffprobe — encoding e probing de vídeo
- Chrome headless (via HyperFrames) — captura de frames

**Decisão e justificativa:**
- Puppeteer: projeto isolado para evitar contaminação; execução sem desativar sandbox
- FFmpeg: winget Gyan full build para codecs completos; validação via ffprobe obrigatória
- HyperFrames: composição própria (não testsrc do FFmpeg) para validar a ferramenta real; GSAP para animação de texto e movimento
- Evidência: Puppeteer: título e screenshot. FFmpeg e HyperFrames: arquivos finais inspecionados com ffprobe.

**Resultado:** 3 ferramentas instaladas e validadas; `docs/capability-inventory.md` atualizado com entradas de Puppeteer, FFmpeg/ffprobe, HyperFrames.

**Limitações:**
- Puppeteer: requer Chromium; execução headless
- FFmpeg: PATH precisa ser atualizado no shell após winget; build Gyan 9.0.2 full
- HyperFrames: requer FFmpeg no PATH; Chrome headless; GPU auto-detect; render local
- Impeccable e design-taste-frontend: testes ainda suspensos por alertas de instalação
- Caveman-compress: apenas concisão de saída autorizada; compressão de arquivo suspensa

**Próximo passo:** Lote 4 — inventário de serviços externos, requisitos de conta, autenticação, possível custo e teste futuro.

**Referência:** Commits pendentes — aguarda revisão e push.

---

## 2026-11-11 — Lote 4: Inventário de Serviços Externos (Esta Sessão)

**Objetivo:** Inventariar 5 serviços externos (APIs, SaaS, cloud) com requisitos de conta, métodos de autenticação, custos estimados e documentação oficial. **Não criar contas, não executar chamadas pagas.**

**Mudança realizada:**
- Pesquisa e documentação de 5 serviços:
  - **Metricool** — Social media analytics & scheduling; API Key; plano pago para endpoints completos; docs: app.metricool.com/resources/apidocs, help.metricool.com
  - **Higgsfield** — AI video generation (image→video, text→video); Bearer Token; pay-per-generation; docs: docs.higgsfield.ai, open.higgsfield.ai/pricing
  - **Apify** — Web scraping & automation (Actors); API Token; pay-per-actor-run; free tier limitado; docs: docs.apify.com/api/v2, help.apify.com
  - **GPT Image (OpenAI)** — Image generation/editing (gpt-image-1); API Key OpenAI; custo por imagem; org verificada; docs: developers.openai.com/api/docs/models/gpt-image-1, pricing
  - **Nano Banana** — AI image generation (Gemini); API Key Google AI; custo por geração; docs: ai.google.dev/gemini-api/docs
- Atualização de `docs/capability-inventory.md`: 5 entradas na tabela Integrações com estado "não verificado"
- Atualização de `docs/setup/skills-and-tools.md`: tabela Lote 4 com 5 serviços
- Atualização de `case-studies/02-skills-and-tools-validation.md`: seção Lote 4, resultados consolidados, lições aprendidas
- Correções de resíduos nos documentos (Caveman, Alertas separados, evidência granular Lote 3, total integrações removido)

**Testes executados:** Nenhum — apenas inventário documental.

| Serviço | Tipo | Autenticação | Custo | Docs | Status | Teste Futuro Mínimo | Ação Humana Necessária |
|---------|------|--------------|-------|------|--------|---------------------|------------------------|
| Metricool | SaaS API | API Key | Plano pago; free tier limitado | app.metricool.com/resources/apidocs | planejado | GET /me (valida auth) | Criar conta; gerar API key |
| Higgsfield | SaaS API | Bearer Token | Pay-per-generation | docs.higgsfield.ai | planejado | POST /generate (5s, parâmetros mínimos) | Criar conta; org verificada se exigida |
| Apify | SaaS Platform | API Token | Pay-per-actor-run | docs.apify.com/api/v2 | planejado | GET /acts (lista Actors) | Criar conta; gerar API token |
| GPT Image | SaaS API | API Key (OpenAI) | Custo por imagem | developers.openai.com/api/docs/models/gpt-image-1 | planejado | POST /images/generations (1 imagem, prompt mínimo) | Conta OpenAI; org verificada |
| Nano Banana | SaaS API | API Key (Google AI) | Custo por geração | ai.google.dev/gemini-api/docs | planejado | POST /models/generateContent (1 imagem, prompt mínimo) | Conta Google AI; habilitar Gemini API |

**Integrações envolvidas:**
- Web (pesquisa de documentação oficial)
- Sistema de arquivos local (atualização de docs)

**Decisão e justificativa:**
- Separar inventário (documentação de requisitos) de integração (conexão real)
- Registrar apenas informações públicas oficiais; não assumir acesso
- Estado "não verificado" / "planejado" reflete ausência de teste real
- Não misturar serviços externos com ferramentas CLI locais

**Resultado:** 5 serviços inventariados; 4 arquivos atualizados com correções de resíduos dos lotes anteriores.

**Limitações:**
- Nenhuma conta criada, nenhuma chamada paga executada
- Custos baseados em documentação pública; podem variar
- Autenticação documentada mas não testada
- Rate limits e quotas não validados

**Próximo passo:** Lote 5+ — definir testes futuros específicos por serviço; avaliar MCP servers; configurar variáveis de ambiente seguras.

**Referência:** Commit `b2851e9` (Lote 3); próximo commit incluirá Lote 4.