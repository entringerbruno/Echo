# Estudo de Caso: Integração com Google Workspace CLI — Escopos OAuth, Validação e Limites da Automação

## Contexto e Problema
Necessidade de operar uma caixa de entrada Gmail via linha de comando para consultar rótulos, listar mensagens e, futuramente, aplicar rótulos e mover mensagens — sem expor credenciais e respeitando o princípio de menor privilégio.

## Papel e Responsabilidades (provisório, pendente de validação)
- Eu defini os requisitos de limpeza, preservação, revisão de itens ambíguos e autorização prévia a alterações.
- O agente auxiliou na formulação e execução dos comandos de consulta.
- Eu acompanhei o fluxo e autorizei a ampliação do escopo de acesso.
- Qualquer outra contribuição técnica ou decisão de implementação está **pendente da minha validação**.

## Restrições
- Não armazenar tokens em arquivos de texto plano.
- Usar apenas o backend do `gws` (keyring do SO) — configuração relatada pelo diagnóstico local.
- Manter a conta pessoal separada de ambientes de teste.

## Ferramenta Utilizada
Foi utilizado o Google Workspace CLI (`gws`). O diagnóstico local relatou armazenamento criptografado de credenciais com backend keyring. Não foi realizada auditoria independente desse mecanismo neste estudo.

## Decisões e Justificativas
- Iniciar com escopo `gmail.readonly` para validar conectividade e listar rótulos/mensagens.
- Ampliar para `gmail.modify` **somente após** autorização explícita, mantendo a separação entre leitura e escrita.
- A proposta de limpeza prevê movimentação por ID individual de mensagem, não por conversa inteira. Criação de rótulos, envio de resumos e ativação do agendamento são operações separadas, sujeitas às respectivas aprovações.

## Implementação e Evidências (sanitizadas)
- Comando de consulta de rótulos: `gws gmail users labels list --params '{"userId": "me"}'` — retornou lista de rótulos do sistema (INBOX, SENT, STARRED, IMPORTANT, etc.).
- Confirmação de conta ativa via resposta JSON da API.
- Solicitação de escopo `gmail.modify` registrada; aprovação concedida via fluxo OAuth do navegador.
- Nas etapas relatadas, a movimentação de mensagens e a instalação da limpeza recorrente **não tiveram execução confirmada**.

## Uso Transparente de IA
- **Sugerido pela IA:** estrutura de comandos `gws`, padrão de validação por escopo, sugestão de separar leitura/escrita.
- **Decisões de requisito e autorização:** definidas por mim (conforme seção "Papel e Responsabilidades").
- **Acompanhamento:** acompanhei os retornos apresentados pelo agente e autorizei a ampliação de acesso. A execução dos comandos e as verificações técnicas foram assistidas pelo agente. Não foi realizada auditoria completa de alterações da conta.

## Resultados e Limitações
- **Confirmado:** consulta de rótulos funciona (`gmail.users.labels.list` validado).
- **Relatado:** aprovação de `gmail.modify` via fluxo OAuth no navegador; concessão de escopo **não inspecionada programaticamente**.
- **Pendente:** automação de triagem/limpeza (script, rótulos customizados, agendador) — ainda não implementada.

## Itens Não Verificados e Fora do Escopo deste Estudo
- Auditoria de segurança, isolamento de rotinas, gerenciamento de estado e memória persistente, ambiente seguro.

## Lições Aprendidas
- Menor privilégio na prática: começar só-leitura evita acidentes e simplifica conferência.
- Separar "autenticar/consultar" de "autorizar alteração" cria checkpoints naturais de decisão.
- CLI com keyring do SO (conforme diagnóstico local) reduz risco de vazamento de token em repositório ou log.