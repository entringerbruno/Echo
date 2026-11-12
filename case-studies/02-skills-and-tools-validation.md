# Estudo de Caso #2: Validação de Skills e Ferramentas — Lotes 1, 2 e 3

**Data:** 2026-11-11  
**Autor:** Bruno Entringer  
**Status:** Concluído — aguarda commit e push  
**Referência:** `docs/setup/skills-and-tools.md`, `docs/capability-inventory.md`, `JOURNAL.md`

---

## Objetivo

Instalar, configurar e validar um conjunto de skills (Claude Code) e ferramentas CLI em ambiente isolado, registrando evidência concreta de execução para cada item. Separar claramente instalação de validação, e registrar alertas/pendências sem ocultá-los.

---

## Escopo

| Lote | Tipo | Itens |
|------|------|-------|
| 1 | Skills | using-agent-skills, humanizer, find-skills, caveman-compress |
| 2 | Skills | ui-ux-pro-max, emil-design-eng, impeccable, design-taste-frontend |
| 3 | Ferramentas | Puppeteer, FFmpeg/ffprobe, HyperFrames |

**Fora do escopo:** Conexão a contas reais, chamadas pagas, serviços cloud, configuração de MCP remoto.

---

## Metodologia

1. **Instalação rastreável:** Usar gerenciadores oficiais (`skills` CLI via npm, `winget` para FFmpeg, `npm` para Puppeteer/HyperFrames).
2. **Ambiente isolado:** Cada ferramenta testada em diretório temporário próprio (`/tmp/...`), sem contaminação do workspace principal.
3. **Validação com evidência:** Todo teste deve produzir saída verificável (arquivo, stdout, ffprobe, screenshot).
4. **Registro honesto:** Estado granular (instalado ≠ executado ≠ validado). Alertas de instalação documentados e testes suspensos até resolução.
5. **Sem bypass:** Não desativar sandbox, não usar credenciais reais, não chamar APIs pagas.

---

## Execução por Lote

### Lote 1 — Skills Básicas (2026-11-06)

| Skill | Instalação | Teste | Resultado | Evidência |
|-------|------------|-------|-----------|-----------|
| using-agent-skills | `skills add addyosmani/agent-skills@using-agent-skills` | Identificar skill para CSV→JSON Python | `incremental-implementation` identificado | Skill invocada; fluxo mapeado |
| humanizer | `skills add blader/humanizer@humanizer` | Reescrever parágrafo com tells de IA | 11 tells removidos (§1,§2,§3,§4,§12,§13,§16) | Texto antes/depois |
| find-skills | `skills add vercel-labs/skills@find-skills` | `npx skills find python csv` | Resultados retornados sem instalar | Lista: xlsx, markitdown, etc. |
| caveman-compress | `skills add juliusbrussee/caveman@caveman-compress` | Comprimir test-caveman.md (Python) | Compressão relatada; **não valida concisão de saída** | test-caveman.md processado |

**Pendência Lote 1:** Caveman-compress — autorização apenas para concisão de respostas; execuções de compressão de arquivo suspensas.

---

### Lote 2 — Skills de Design/Review (2026-11-06)

| Skill | Instalação | Teste | Resultado | Evidência |
|-------|------------|-------|-----------|-----------|
| ui-ux-pro-max | `skills add ui-ux-pro-max@ui-ux-pro-max` | Busca `--design-system` / `--domain ux` | Tabela de revisão gerada | Tabela de revisão |
| emil-design-eng | `skills add emilkowalski/skills@emil-design-eng` | Review CSS botão | Tabela Before/After produzida | Tabela Before/After |
| impeccable | `skills add impeccable@impeccable` | **Não executado** | **Socket alert** no instalador | — |
| design-taste-frontend | `skills add design-taste-frontend@design-taste-frontend` | **Não executado** | **Critical Risk** no instalador | — |

**Pendência Lote 2:** Impeccable e design-taste-frontend — alertas de instalação ("Socket" / "Critical Risk") sem causa identificada; testes suspensos.

---

### Lote 3 — Ferramentas de Browser/Vídeo (2026-11-11)

#### Puppeteer
- **Instalação:** `npm install puppeteer` em `/tmp/puppeteer-test`
- **Teste:** HTML sintético com título "Puppeteer Synthetic Test" → screenshot fullPage
- **Comando:** `node test-no-sandbox.js` (sem `--no-sandbox`)
- **Resultado:** `screenshot.png` gerado; título confirmado via `page.title()`
- **Evidência:** Arquivo PNG + log de execução

#### FFmpeg/ffprobe
- **Instalação:** `winget install --id Gyan.FFmpeg` → 9.0.2 full build
- **Teste 1:** Clipe sintético 2s — `testsrc` (640×480@30) + `sine` (440Hz) → `synthetic-2s.mp4`
- **Validação:** `ffprobe` → vídeo 2,0s 640×480@30; áudio 2,0s 44.1kHz mono
- **Evidência:** Arquivo MP4 + saída ffprobe CSV

#### HyperFrames
- **Instalação:** `npx hyperframes init hyperframes-test` → v0.9.36 + 6 skills anexadas
- **Composição:** HTML/GSAP 3s — título (fade+slide), subtítulo (fade), barra (width expand), fade out final
- **Render:** `npx hyperframes render -o hyperframes-3s.mp4` (com FFmpeg no PATH)
- **Validação:** `ffprobe` → 1920×1080@30, 3,0s
- **Evidência:** Arquivo MP4 (129.5 KB) + saída ffprobe CSV
- **Nota:** Composição **própria** (não `testsrc` do FFmpeg) — valida HyperFrames real

---

## Resultados Consolidados

| Item | Tipo | Estado Final | Evidência Principal | Pendência |
|------|------|--------------|---------------------|-----------|
| using-agent-skills | Skill | validado | Skill invocada | — |
| humanizer | Skill | validado | 11 tells removidos | — |
| find-skills | Skill | validado | Lista skills retornada | — |
| caveman-compress | Skill | **suspenso** | test-caveman.md | Concisão ≠ compressão; execuções suspensas |
| ui-ux-pro-max | Skill | validado | Tabela revisão | — |
| emil-design-eng | Skill | validado | Tabela Before/After | — |
| impeccable | Skill | **suspenso** | Socket alert | Causa não identificada |
| design-taste-frontend | Skill | **suspenso** | Critical Risk | Causa não identificada |
| Puppeteer | Ferramenta | validado | screenshot.png | — |
| FFmpeg/ffprobe | Ferramenta | validado | synthetic-2s.mp4 + ffprobe | PATH update necessário |
| HyperFrames | Ferramenta | validado | hyperframes-3s.mp4 + ffprobe | Requer FFmpeg + Chrome |

**Total:** 11 itens — 9 validados, 3 suspensos (1 Lote 1 + 2 Lote 2), 0 falharam.

---

## Lições Aprendidas

1. **Instalação ≠ Validação:** 3 skills instaladas no Lote 2 mas 2 com testes suspensos por alertas de instalador. Registrar o alerta e suspender é mais honesto que forçar execução.
2. **Evidência objetiva:** ffprobe para vídeo, arquivo PNG para screenshot, saída de comando para skills — elimina subjetividade.
3. **Isolamento funciona:** Diretórios `/tmp/...` evitam poluição do workspace e facilitam limpeza.
4. **PATH no Windows/winget:** Após `winget install`, o shell atual não vê o novo PATH. Precisa `export PATH=...` ou reiniciar shell.
5. **HyperFrames ≠ FFmpeg:** O `testsrc` do FFmpeg valida FFmpeg, não HyperFrames. Composição HTML/GSAP própria é necessária para validar a ferramenta real.

---

## Próximos Passos (Lote 4)

1. Inventariar serviços externos (APIs, SaaS, cloud) que o projeto pode usar.
2. Para cada serviço: requisitos de conta, métodos de autenticação, custos estimados.
3. Definir testes futuros (sem executar) — ex.: "teste de escrita Gmail com `gmail.modify`", "deploy Lovable em preview".
4. **Não** conectar contas, criar contas, ou fazer chamadas pagas no Lote 4.

---

## Arquivos Atualizados/Criados

- `docs/capability-inventory.md` — entradas de Puppeteer, FFmpeg/ffprobe, HyperFrames nas Integrações; hyperframes nas Skills; notas de atualização
- `JOURNAL.md` — entrada "2026-11-11 — Lote 3: Instalação e Validação de Ferramentas"
- `docs/setup/skills-and-tools.md` — **criado** — registro tabular completo de todos os lotes
- `case-studies/02-skills-and-tools-validation.md` — **criado** — este documento

---

## Verificação de Segurança

- Nenhum segredo, token, credencial ou caminho absoluto privado nos arquivos acima.
- Dados de teste são sintéticos (HTML, vídeo gerado programaticamente).
- Memória operacional privada (`_Memoria/`, `.claude/projects/`) **não** incluída.
- Triagem por padrões executada antes da publicação.

---

## Referência de Commit

Pendente — aguarda `git add` explícito dos 4 arquivos, commit e push via `gh`.