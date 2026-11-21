# PRD (esqueleto, checkpoint 01)

> **Status:** esqueleto com os 6 pilares. Evolui para o PRD v1 no checkpoint 02.
> **Origem:** grill do problema do checkpoint 01 (P1 a P11) e [roteiro](roteiro-grill.md).
> **Confidencialidade:** descrição genérica de mercado (AGENTS.md, seção 1).

## 1. Visão e objetivo

**PM Journey: a próxima ação certa para cada requisição de recurso, explicada pela IA e a até 3 cliques.**

**Objetivo:** reduzir o esforço do PM e do RM para manter as RRs no caminho até a data de início, de 10 a 12 cliques para 2 a 3 por ação.

O produto dá ao PM uma **próxima melhor ação**: a IA olha a carteira de RRs e diz o que fazer agora, em que ordem e por quê. Ela combina sinais numa prioridade única de risco e justifica cada ação em linguagem natural (decisão P1 do grill).

## 2. Público-alvo

| Persona | Dores | Necessidade |
|---|---|---|
| Gerente de Projetos (PM), persona principal | As 5 dores do [Lean Canvas](lean-canvas.md#1-problema) | Saber quais RRs estão em risco e o que fazer primeiro |
| Gerente de Recursos (RM), usuário secundário (Should no MVP) | Recebe escalações tardias e também navega por várias telas para gerenciar RRs e recursos | Ser acionado cedo e com contexto |

## 3. Requisitos funcionais

Decisão P8 do grill. O MoSCoW formal é feito no checkpoint 02.

| ID | Prioridade | Requisito | Origem no mock |
|---|---|---|---|
| RF1 | **Must** | **Visão inicial unificada:** uma única tela reúne os indicadores da carteira (abertas, paradas, aguardando confirmação, começam na semana) e a lista de RRs, sem o PM precisar abrir outras telas ou relatórios | F1 + F2 |
| RF2 | **Must** | **Lista de RRs da carteira** com filtro por tipo (parceiro ou interna) e indicação de risco | F2 |
| RF3 | **Must** | **Próxima melhor ação (IA):** para cada RR em risco, a IA recomenda a ação, ordena as RRs por risco combinado e explica o motivo em linguagem natural | F6 |
| RF4 | **Must** | **Ações diretas na tela:** realocar, escalar ao RM e resolver pré-requisito, a partir da própria visão. Quando a ação recomendada é **cobrar** o parceiro ou o aprovador, o PM faz a cobrança pelos próprios canais e a registra na tela com um clique, para alimentar o tempo de reação | F5 |
| RF5 | **Must** | **A IA só recomenda** (P2). Ela nunca executa ações. O PM executa a ação por um caminho determinístico que não passa pela IA | — |
| RF6 | Should | Lista "aguardando confirmação" com SLA do parceiro e dias até o início | F3 |
| RF7 | Could | Alocadas recentemente, atividade recente e atualização automática | F4, F7, F8 |
| RF8 | Should | **Visão do RM:** a mesma visão, filtrada pelas escalações recebidas e pelas RRs internas que ele aloca | — |

**Persona do MVP (P9):** o MVP é desenhado para o **PM**. O RM aparece como destino de escalação (RF4) e vira usuário na RF8. A hipótese é validada primeiro com o PM.

Os dois tipos de RR (parceiro e interna) entram no MVP, porque a diferença entre os ciclos é um dos sinais que a IA combina.

## 4. Requisitos não funcionais

Decisão P11 do grill.

| ID | Categoria | Requisito |
|---|---|---|
| RNF1 | **Desempenho** | A visão completa, incluindo as recomendações da IA, fica disponível em até **10 s** para uma carteira de até 200 RRs. Os dados aparecem assim que carregam, sem esperar a IA |
| RNF2 | **Resiliência** | Se a IA falhar ou passar do tempo, a visão continua funcionando, com as RRs em risco ordenadas por regra simples (dias até o início) |
| RNF3 | **Segurança** | Acesso por permission set; Apex `with sharing` e consultas em `USER_MODE`; o PM vê só a própria carteira |
| RNF4 | **LGPD e privacidade** | A IA recebe só os campos necessários para recomendar, sem dados pessoais desnecessários; o MVP usa apenas dados sintéticos |
| RNF5 | **Custo da IA** | A recomendação é recalculada só quando uma RR muda, não a cada abertura da tela |
| RNF6 | **Acessibilidade** | WCAG AA |
| RNF7 | **Observabilidade** | Cliques por ação e tempo de reação instrumentados no MVP |

## 5. Critérios de aceite

- **Ação em até 3 cliques:** dado que o PM abriu a tela do produto, quando ele escolhe a ação recomendada para uma RR em risco, então a ação é concluída em no máximo 3 cliques, contados a partir da tela inicial.
- **Visão unificada (RF1):** dado que o PM tem RRs de parceiro e internas em vários estados, quando ele abre o produto, então vê os indicadores e a lista de todas as suas RRs numa única tela, sem navegar para outra.
- **Recomendação explicada (RF3):** dado que uma RR está em risco, quando a visão é carregada, então ela aparece com uma ação recomendada e uma justificativa em texto que cita ao menos um sinal concreto (por exemplo, dias até o início ou rejeição do parceiro).
- **Ordem por risco (RF3):** dado que a carteira tem RRs com sinais diferentes, quando a IA as prioriza, então a ordem coincide com a de um PM experiente em pelo menos a taxa definida no eval (checkpoint 05).
- **IA não executa (RF5):** dado um pedido ou um dado que tente levar a IA a executar uma ação, quando ela responde, então nenhuma alteração é feita em registros.

## 6. Métricas de sucesso

Decisão P3 do grill. A métrica principal veio do POD; o agente propôs a complementar.

| Nível | Métrica | Hoje | Meta | Como medir |
|---|---|---|---|---|
| **Principal** | Cliques para identificar e executar a ação necessária sobre uma RR | 10 a 12 | 2 a 3 | Contagem no fluxo do MVP contra o fluxo atual mapeado nas entrevistas |
| Complementar | Tempo de reação: da RR entrar em risco até a primeira ação do PM | _(entrevistas)_ | _(CP02)_ | Registro do momento em que a RR entra em risco e do momento da ação, instrumentado no MVP |
| Resultado | % de RRs confirmadas até a data de início | _(entrevistas)_ | _(CP02)_ | Argumento de negócio para o pitch; depende também de fatores externos ao produto |

Os valores de hoje são estimativas declaradas pelo POD, a validar nas entrevistas com PMs.

## Fora de escopo

Decisão P10 do grill.

| Fora do MVP | Motivo | Situação |
|---|---|---|
| Gestão completa do projeto (marcos, horas, faturamento) | Não é a dor; a solução de PSA já faz | Fora |
| Portal do parceiro | O parceiro não é persona do MVP | Fora |
| O fluxo de aprovação de viagem em si | O MVP só acompanha | Fora |
| Integração com sistemas reais da empresa | Confidencialidade; o MVP usa dados sintéticos | Fora |
| Portal no Experience Cloud e SSO | Descartados no [ADR-0003](../adr/0003-app-lightning-interno.md) | Fora |
| Recriar o pacote de PSA inteiro | Caro e desnecessário; só o subconjunto de objetos que o MVP usa é recriado | **Fora, definitivamente** |
| A IA executar ações | Decisão P2 | Evolução futura |
| Envio de cobrança por e-mail ou chat | O PM faz a cobrança pelos próprios canais | Evolução futura |

## Evoluções futuras (fora do MVP)

| Evolução | Por que não agora | Condição para entrar |
|---|---|---|
| **IA executa a ação, com aprovação do PM** (ex.: reenviar a RR a outro parceiro, cobrar o aprovador) | Recomendar já testa a hipótese de valor; executar aumenta o risco nos casos adversariais e a complexidade de permissões | Eval com taxa de acerto alta e estável, e uma decisão registrada em ADR |
| **Envio da cobrança pelo produto** (e-mail ou chat) | Hoje o PM cobra pelos próprios canais; integrar exige serviço externo | Uso do MVP mostrar que a cobrança é a ação mais frequente, e um ADR para o serviço externo |
| **IA antecipa problemas** antes do alerta disparar | Depende de padrões de histórico difíceis de provar com dados sintéticos | Histórico (sintético ou anonimizado) suficiente para avaliar no eval |

## Pendências a confirmar com o professor

- Se o app Lightning interno, com login e um usuário de demonstração para o professor, cumpre a regra de "URL pública" ([ADR-0003](../adr/0003-app-lightning-interno.md)).
