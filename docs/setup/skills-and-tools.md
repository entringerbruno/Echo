# Skills e Ferramentas — Registro de Instalação e Validação

Documento técnico de referência para rastrear a instalação, configuração e validação de skills (Claude Code) e ferramentas CLI no ambiente do projeto Echo.

---

## Convenção de Registro

Cada entrada segue o formato:

| Campo | Descrição |
|-------|-----------|
| **Nome** | Nome da skill/ferramenta |
| **Versão/Source** | Versão ou fonte de instalação (npm, winget, etc.) |
| **Comando de Instalação** | Comando exato executado |
| **Data** | Data da instalação (YYYY-MM-DD) |
| **Teste de Validação** | Descrição do teste executado |
| **Resultado** | Saída esperada confirmada / falha / suspenso |
| **Evidência** | Arquivo, saída de comando, ou link para evidência |
| **Status** | `validado` / `suspenso` / `falhou` / `planejado` |
| **Observações** | Limitações, dependências, alertas |

---

## Skills (Claude Code)

### Lote 1 — 2026-11-06

| Nome | Versão/Source | Comando de Instalação | Data | Teste de Validação | Resultado | Evidência | Status | Observações |
|------|---------------|----------------------|------|-------------------|-----------|-----------|--------|-------------|
| using-agent-skills | addyosmani/agent-skills | `skills add addyosmani/agent-skills@using-agent-skills` | 2026-11-06 | Identificar skill para tarefa Python CSV→JSON | `incremental-implementation` identificado | Skill invocada | validado | Meta-skill; 79 agentes mapeados |
| humanizer | blader/humanizer v3.1.0 | `skills add blader/humanizer@humanizer` | 2026-11-06 | Reescrever parágrafo sintético com tells de IA | 11 tells removidos (§1,§2,§3,§4,§12,§13,§16) | Texto reescrito | validado | Processo manual guiado por skill |
| find-skills | vercel-labs/skills | `skills add vercel-labs/skills@find-skills` | 2026-11-06 | `npx skills find python csv` | Resultados retornados (xlsx, markitdown, etc.) sem instalar | Lista de skills | validado | Busca apenas; não instala |
| caveman-compress | juliusbrussee/caveman | `skills add juliusbrussee/caveman@caveman-compress` | 2026-11-06 | Comprimir test-caveman.md (Python) | Compressão relatada; não valida concisão de saída | test-caveman.md comprimido | suspenso | Autorização só para concisão de respostas; execuções de compressão suspensas |

---

### Lote 2 — 2026-11-06

| Nome | Versão/Source | Comando de Instalação | Data | Teste de Validação | Resultado | Evidência | Status | Observações |
|------|---------------|----------------------|------|-------------------|-----------|-----------|--------|-------------|
| ui-ux-pro-max | tasteskill local | `skills add ui-ux-pro-max@ui-ux-pro-max` | 2026-11-06 | Busca `--design-system` / `--domain ux` para botão | Resultado gerado com tabela de revisão | Tabela de revisão | validado | Dados locais; execução = busca, não build |
| emil-design-eng | emilkowalski/skills | `skills add emilkowalski/skills@emil-design-eng` | 2026-11-06 | Review de CSS de botão com tabela Before/After | Orientação produzida | Tabela Before/After | validado | Knowledge-based; não executa código |
| impeccable | impeccable | `skills add impeccable@impeccable` | 2026-11-06 | Não executado | Socket alert relatado no instalador | — | suspenso | Identificar causa do alerta |
| design-taste-frontend | tasteskill 2.5.0 | `skills add design-taste-frontend@design-taste-frontend` | 2026-11-06 | Não executado | Critical Risk relatado no instalador | — | suspenso | Identificar causa do alerta |

---

### Lote 3 — 2026-11-11

| Nome | Versão/Source | Comando de Instalação | Data | Teste de Validação | Resultado | Evidência | Status | Observações |
|------|---------------|----------------------|------|-------------------|-----------|-----------|--------|-------------|
| hyperframes | 0.9.36 (npm) | `npx hyperframes init hyperframes-test` | 2026-11-11 | Init + composição HTML/GSAP 3s + `hyperframes render` | `hyperframes-3s.mp4` 1920×1080@30, 3,0s; ffprobe validado | Arquivo MP4 + ffprobe | validado | Requer FFmpeg no PATH; Chrome headless; GPU auto |

---

## Ferramentas CLI / Bibliotecas

### Lote 3 — 2026-11-11

| Nome | Versão/Source | Comando de Instalação | Data | Teste de Validação | Resultado | Evidência | Status | Observações |
|------|---------------|----------------------|------|-------------------|-----------|-----------|--------|-------------|
| Puppeteer | 23.x (npm) | `npm install puppeteer` (em `/tmp/puppeteer-test`) | 2026-11-11 | Projeto isolado; HTML sintético + screenshot fullPage | `screenshot.png` gerado; execução sem `--no-sandbox` | screenshot.png | validado | Projeto isolado; requer Chromium; headless |
| FFmpeg/ffprobe | 9.0.2 (Gyan full) | `winget install --id Gyan.FFmpeg` | 2026-11-11 | Clipe sintético 2s (testsrc + sine) → ffprobe | Vídeo 2,0s 640×480@30; Áudio 2,0s 44.1kHz mono | synthetic-2s.mp4 + ffprobe | validado | PATH precisa update pós-winget; build full |
| HyperFrames CLI | 0.9.36 (npm) | `npx hyperframes` (já instalado com skill) | 2026-11-11 | Render composição própria 3s | MP4 1920×1080@30, 3,0s; ffprobe validado | hyperframes-3s.mp4 + ffprobe | validado | Requer FFmpeg no PATH; Chrome headless |

---

## Resumo por Lote

| Lote | Data | Skills Instaladas | Ferramentas Instaladas | Validadas | Suspensas | Falharam |
|------|------|-------------------|------------------------|-----------|-----------|----------|
| 1 | 2026-11-06 | 4 | 0 | 3 | 1 | 0 |
| 2 | 2026-11-06 | 4 | 0 | 2 | 2 | 0 |
| 3 | 2026-11-11 | 1 | 3 | 4 | 0 | 0 |
| **Total** | — | **9** | **3** | **9** | **3** | **0** |

---

## Próximos Passos (Lote 4)

- Inventário de serviços externos (APIs, SaaS, cloud)
- Requisitos de conta por serviço
- Métodos de autenticação (OAuth, API key, service account)
- Possíveis custos (free tier, pay-per-use, assinatura)
- Testes futuros planejados (sem execução imediata)
- **Não** conectar contas, criar contas ou fazer chamadas pagas neste lote