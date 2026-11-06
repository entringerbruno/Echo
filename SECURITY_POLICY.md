# Política de Segurança e Privacidade

## Objetivo
Garantir que nenhum dado sensível, credencial, identificador pessoal ou informação de terceiros seja exposto neste repositório.

---

## Controles de Redução de Risco

| Controle | Descrição | Limitação |
|----------|-----------|-----------|
| Separação física de diretórios | Portfólio em `<diretório-do-portfólio>`, fora do ambiente local privado | Erro humano pode copiar arquivo errado |
| Lista explícita de arquivos | Apenas arquivos listados no README entram no repositório | Exige disciplina manual a cada adição |
| Revisão humana antes de commit | Autor aprova conteúdo e destino de cada arquivo | Não automatizado; depende de processo |
| `.gitignore` defensivo | Bloqueia `.env`, `*.log`, `keyring/`, `tokens/`, `credentials/`, `*.key`, `*.pem`, `*.p12`, `*.pfx` | Não impede commit de segredo dentro de arquivo permitido |
| Scan de segredos pré-commit | `detect-secrets` ou `git-secrets` no hook local | Falsos positivos/negativos possíveis; não substitui revisão |
| Dados sintéticos obrigatórios | Exemplos usam `user@example.com`, `Empresa X`, `AKIA...EXAMPLE` | Requer verificação manual de cada valor |

> **Não há promessa de "risco zero".** Os controles acima reduzem a superfície de exposição, mas a revisão humana continua sendo a barreira principal.

---

## Dados Proibidos em Qualquer Arquivo do Repositório

- Chaves de API, tokens OAuth, segredos de qualquer provedor
- Credenciais do `gws`, Google, GitHub, provedores de IA
- Arquivos `.env`, sessões, configurações privadas
- Logs com dados sensíveis
- Conteúdo de e-mails, candidaturas, documentos pessoais
- Dados de clientes, empregadores ou terceiros
- Capturas de tela com identificadores ou informações sensíveis
- Nomes de usuário locais, caminhos pessoais, e-mails reais

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

- **Área privada de trabalho:** `<diretório-privado-local>` — não versionada publicamente.
- **Área publicável:** `<diretório-do-portfólio>` — construída do zero, apenas com arquivos aprovados.

---

## Verificação Antes de Publicação

1. `git diff` completo revisado pelo autor.
2. Scan de segredos executado (`detect-secrets scan` ou equivalente).
3. Inspeção manual de imagens, PDFs e arquivos não-textuais.
4. Confirmação de que nenhum arquivo da lista proibida está staged.
5. Aprovação final do autor para `git push`.

---

## Atualizações desta Política

Quaisquer alterações nesta política exigem aprovação explícita do autor antes de entrarem em vigor.