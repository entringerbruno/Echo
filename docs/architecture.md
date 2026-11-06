# Arquitetura do Echo

## Visão Geral

O Echo é um portfólio público que documenta a construção de soluções com IA. A arquitetura separa fisicamente o ambiente privado de trabalho (vault) do portfólio público, com controles processuais de publicação.

---

## Componentes

### Ambiente Privado (Não Publicado)
- **Memória operacional em Markdown:** estado, decisões, sessões
- **Identidades profissionais:** Documentos de posicionamento
- **Configurações MCP:** Arquivo local com credenciais
- **Definições de skills/agentes:** Diretórios locais

### Portfólio Público (Echo / `portfolio-tech/`)
- **Documentação:** `README.md`, `JOURNAL.md`, `SECURITY_POLICY.md`
- **Estudos de caso:** `case-studies/`
- **Documentos técnicos:** `docs/architecture.md`, `docs/capability-inventory.md`, `docs/decisions.md`
- **Configuração de publicação:** `.gitignore`, repositório Git

### Ferramentas CLI (Operacionais)
| Ferramenta | Função | Estado |
|------------|--------|--------|
| `git` | Versionamento, push | Documentado; push HTTPS funcionou |
| `gh` (GitHub CLI) | Autenticação, credential helper, operações GitHub | Autenticado; push HTTPS funcionou |
| `gws` (Google Workspace CLI) | Operações Gmail/Workspace | Consulta de rótulos documentada; `gmail.modify` não verificado |

### Servidores MCP (Configurados)
| Servidor | Transporte | Finalidade | Estado |
|----------|------------|------------|--------|
| Obsidian | HTTP (localhost:27123) | Acesso a notas | Configurado; falha observada (ECONNREFUSED) |
| Supabase | HTTP (mcp.supabase.com) | Database, docs (parâmetro read-only) | Configurado; conexão não verificada |

### Skills (Diretórios Encontrados)
86 diretórios em `.claude/skills/` agrupados em:
- `graphify` (1) — Knowledge graph
- `gws-*` (38) — Google Workspace CLI
- `persona-*` (8) — Workflows de personas
- `recipe-*` (38) — Receitas operacionais
- `competitive-ads-extractor` (1) — Extração de anúncios

**Nota:** Diretório encontrado ≠ definição inspecionada ≠ execução ≠ validação. Ver `docs/capability-inventory.md` para estados detalhados.

---

## Fronteiras de Confiança

```
┌─────────────────────────────────────────────────────────────┐
│                    AMBIENTE PRIVADO                         │
│  memória operacional  |  Identidades  |  .mcp.json  |  .claude/      │
│  (credenciais, caminhos absolutos, nomes internos)          │
└──────────────────────────┬──────────────────────────────────┘
                           │ Publicação controlada
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                    PORTFÓLIO PÚBLICO (Echo)                 │
│  README  |  JOURNAL  |  SECURITY  |  CASES  |  DOCS  | Git │
│  (dados sintéticos, placeholders, lista explícita)          │
└─────────────────────────────────────────────────────────────┘
```

**Controles de fronteira:**
1. Separação física de diretórios
2. Lista explícita de arquivos publicáveis (`git add` individual)
3. Dados sintéticos obrigatórios
4. Revisão humana antes de commit
5. Scan de segredos (planejado — hook não instalado; triagem manual por padrões)
6. Credential helper via `gh` (token no keyring do sistema operacional)

---

## Fluxos Principais

### Publicação
```
Editar arquivos autorizados
    │
    ▼
git add <arquivo1> <arquivo2> ...  (individual)
    │
    ▼
git commit -m "mensagem descritiva"
    │
    ▼
git push origin master  (via HTTPS + gh credential helper)
    │
    ▼
Verificação: git status clean + git log + remote sync
```

### Consulta Gmail (Documentada)
```
gws gmail users labels list --params '{"userId": "me"}'
    │
    ▼
OAuth → Keyring do SO
    │
    ▼
Gmail API → Retorno JSON (INBOX, SENT, STARRED, IMPORTANT...)
```

### Retomada de Sessão
```
Iniciar sessão no Echo
    │
    ▼
Ler memória privada (echo-private-memory.md)
    │
    ▼
Ler JOURNAL.md + git status + git log
    │
    ▼
Confirmar: último marco, diretório correto, pendências
    │
    ▼
Definir próxima ação
```

---

## Decisões Arquiteturais

Referência: [`docs/decisions.md`](decisions.md)

1. Separação física de diretórios (vault ↔ portfolio)
2. Lista explícita — sem `git add .`
3. Credential helper via `gh` (HTTPS + keyring do SO)
4. Dados sintéticos obrigatórios
5. Memória operacional em Markdown
6. Estados granulares para capacidades (9 categorias)

---

## Componentes Planejados (Não Implementados)

- Hooks `detect-secrets` + `pre-commit`
- Agentes customizados em `.claude/agents/`
- Estudo de caso #2 (ambiente seguro / diagnóstico gateways)
- `examples/` com demonstrações reproduzíveis
- Rotina de atualização/consulta do Graphify