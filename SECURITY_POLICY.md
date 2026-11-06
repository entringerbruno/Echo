# Política de Segurança e Privacidade

## Objetivo
Garantir que nenhum dado sensível, credencial, identificador pessoal ou informação de terceiros seja exposto neste repositório.

---

## Controles de Redução de Risco

| Controle | Descrição | Limitação |
|----------|-----------|-----------|
| Separação física de diretórios | Portfólio em diretório dedicado, fora do ambiente privado | Erro humano pode copiar arquivo errado; `.gitignore` não isola por si só |
| Lista explícita de arquivos | Apenas arquivos listados entram no repositório | Exige disciplina manual a cada adição |
| Revisão humana antes de commit | Autor aprova conteúdo e destino de cada arquivo | Não automatizado; depende de processo |
| `.gitignore` defensivo | Bloqueia `.env`, `*.log`, `keyring/`, `tokens/`, `credentials/`, `*.key`, `*.pem`, `*.p12`, `*.pfx` | Não impede commit de segredo dentro de arquivo permitido |
| Scan de segredos pré-commit | **Planejado — não instalado** (`detect-secrets` ou `git-secrets` via `pre-commit`) | Falsos positivos/negativos possíveis; não substitui revisão |
| Dados sintéticos obrigatórios | Exemplos usam `user@example.com`, `Empresa X`, `AKIA...EXAMPLE` | Requer verificação manual de cada valor |

> **Não há promessa de "risco zero".** Os controles acima reduzem a superfície de exposição, mas a revisão humana continua sendo a barreira principal. A verificação por padrões é uma triagem, não prova de ausência absoluta de segredos.

---

## Dados Proibidos em Qualquer Arquivo do Repositório

- Chaves de API, tokens OAuth, segredos de qualquer provedor
- Credenciais de CLIs e provedores de IA
- Arquivos `.env`, sessões, configurações privadas
- Logs com dados sensíveis
- Conteúdo de e-mails, candidaturas, documentos pessoais
- Dados de clientes, empregadores ou terceiros
- Capturas de tela com identificadores ou informações sensíveis
- Nomes de usuários locais, caminhos pessoais, e-mails reais
- Nomes de diretórios privados, identificadores de projetos internos
- Valores de autenticação (tokens, headers, variáveis de ambiente sensíveis)

---

## Dados Sintéticos e Exemplos

- E-mails: `user@example.com`, `contato@empresa-x.com`
- Nomes de organizações: `Empresa X`, `Organização Y`
- Chaves/IDs: `AKIAIOSFODNN7EXAMPLE`, `msg-id-sintetico-123`
- Datas: `2024-01-15` (genéricas, não reais)
- Qualquer valor de exemplo deve ser claramente identificável como fictício

---

## Procedimento de Incidente de Segredo

| Situação | Ação |
|----------|------|
| **Segredo real exposto** (token, API key, credencial válida) | Informar **tipo** e **local** (arquivo/linha) **sem reproduzir o valor**; propor revogação/rotação na origem; aguardar aprovação do autor para prosseguir. |
| **Exemplo fictício ou falso positivo** (ex.: `AKIAIOSFODNN7EXAMPLE`) | Revisar juntos; se confirmado fictício, documentar como “exemplo intencional” nesta política. |
| **Nunca** | Revogação/rotação automática sem confirmação explícita do autor. |

---

## Separação de Ambientes

- **Área privada de trabalho:** diretório dedicado — não versionado publicamente.
- **Área publicável:** diretório do portfólio — construída do zero, apenas com arquivos aprovados.

A separação é física (diretórios distintos) e processual (lista explícita, revisão humana). O `.gitignore` é uma camada adicional, não a única barreira.

---

## Verificação Antes de Publicação

1. `git diff` completo revisado pelo autor.
2. Scan de segredos executado (**planejado — hook não instalado**; verificação manual por padrões nesta etapa).
3. Inspeção manual de imagens, PDFs e arquivos não-textuais.
4. Confirmação de que nenhum arquivo da lista proibida está staged.
5. Aprovação final do autor para `git push`.

---

## Credenciais em Configuração Local

Arquivos de configuração local (ex.: `.mcp.json`) podem conter valores de autenticação. Estes são **credenciais armazenadas localmente**, não credenciais publicadas ou exibidas em saída.

- Não copiar arquivos de configuração para o repositório.
- Não exibir valores sensíveis em logs, diffs ou documentação.
- Não foi encontrada evidência de publicação no escopo efetivamente verificado.
- Se houver suspeita de divulgação acidental, registrar pendência privada e propor tratamento separado (revogação/rotação com aprovação).

---

## Atualizações desta Política

Quaisquer alterações nesta política exigem aprovação explícita do autor antes de entrarem em vigor.