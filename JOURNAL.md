# Linha do Tempo de Marcos — Jornada Técnica

> **Legenda de Status**
> - **Implementado** — código/execução realizada e verificada
> - **Testado** — executado com validação de saída esperada
> - **Planejado** — definido, aguarda execução ou aprovação
> - **Relatado** — informado pelo autor, sem verificação independente

---

## Marcos relatados — datas pendentes de validação

- **Relatado:** Estruturação do ambiente local privado com memórias operacionais (`ESTADO.md`, `DECISOES.md`, `SESSOES.md`).
- **Relatado:** Início do uso de Graphify para extração de grafo de conhecimento a partir de documentos locais.
- **Relatado:** Configuração de ambiente de desenvolvimento local com PowerShell, ferramentas CLI e integração com provedores de IA via SDK.
- **Implementado:** Autenticação inicial do Google Workspace CLI (`gws`) com escopo `gmail.readonly`.
- **Testado:** Consulta de rótulos do Gmail via `gws gmail users labels list` — retorno JSON validado (INBOX, SENT, STARRED, IMPORTANT, etc.).
- **Planejado:** Ampliação de escopo para `gmail.modify` para operações de escrita futura.
- **Implementado:** Autorização concedida para escopo `gmail.modify` via fluxo OAuth do navegador.
- **Testado:** Confirmação de conta ativa e escopos concedidos via resposta da API.
- **Planejado:** Desenho da automação de triagem e limpeza diária do Gmail (script PowerShell, rótulos customizados, agendador de tarefas do sistema às 03:00 BRT, limite 10 msgs/execução).
- **Planejado:** Criação dos rótulos `"Atenção verificar"` e `"Manter"` no Gmail.
- **Planejado:** Script `gmail-cleanup.ps1` com modo simulação (`-DryRun`) e envio de resumo de reprovações por e-mail.
- **Planejado:** Registro da tarefa agendada (ex.: `<ambiente-privado>\Gmail-Daily-Cleanup`) no agendador de tarefas do sistema.
- **Implementado:** Estruturação inicial do portfólio técnico local, aguardando revisão e publicação (`portfolio-tech`) — arquivos criados localmente, aguardando revisão.
- **Testado:** Verificação de ausência de identificadores pessoais e segredos nos arquivos gerados.
- **Planejado:** Revisão e aprovação dos 5 arquivos iniciais antes de qualquer `git init`.

---

## Próximos Marcos (Sujeitos a Aprovação)

1. Validação final dos arquivos do portfólio e `git init` local.
2. Execução simulada (`-DryRun`) do script de limpeza do Gmail.
3. Criação dos rótulos customizados no Gmail mediante aprovação.
4. Registro da tarefa agendada após validação da simulação.
5. Novos estudos de caso: ambiente seguro, diagnóstico de gateways/modelos, outros projetos reais sanitizados.