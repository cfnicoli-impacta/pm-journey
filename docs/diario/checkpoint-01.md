# Diário agêntico: checkpoint 01 (Times e desafio)

**Período:** 2026-11-16 a 2026-11-21
**Fase AI-DLC:** Inception
**Entrega mínima:** POD e papéis no README, Lean Canvas, hipótese, esqueleto do PRD e AGENTS.md v0

> Este diário registra o que o agente fez, onde errou e onde o POD interveio. Cada membro completa as seções marcadas com _(POD)_ com o que viveu. O agente não inventa intervenções.

## 1. O que o agente fez

| Data | Entrega | PR |
|---|---|---|
| 2026-11-16 | Estrutura do projeto Salesforce DX (`src/`), ferramentas de lint, formatação e testes, e manifesto | #1 |
| 2026-11-16 | Spec Kit v1.4.1 com skills do Claude Code | #1 |
| 2026-11-16 | AGENTS.md v0, CLAUDE.md, contexto do bootcamp e fluxo de trabalho (`docs/workflow.md`) | #1 |
| 2026-11-16 | ADR-0001 (Salesforce como plataforma) e ADR-0002 (estrutura do repositório) | #1 |
| 2026-11-16 | Regra de confidencialidade atualizada com a decisão de repositório público | #1 |
| 2026-11-16 | Proteção da `main` configurada via GitHub CLI, a pedido da Nicoli: PR obrigatório com 1 aprovação, válida também para administradores, último push aprovado por outra pessoa, sem force push | — (configuração do repositório) |
| 2026-11-20 | Mock de referência anonimizado e roteiro para o grill do problema | #2 |
| 2026-11-20 | ADR-0003 (app Lightning interno como modelo de acesso) | #2 |
| 2026-11-21 | Análise do PDF da Aula 01 contra o repositório, levantando o que faltava para o checkpoint | #3 |
| 2026-11-21 | Enquadramento do projeto como intraempreendedorismo no README e criação deste diário | #3 |
| 2026-11-21 | Grill do problema (11 perguntas, uma por vez, com recomendação) e preenchimento de Lean Canvas, hipótese, esqueleto do PRD e README a cada ramo fechado | #3 |

## 2. Decisões do POD

| Decisão | Onde está registrada |
|---|---|
| Salesforce como plataforma | [ADR-0001](../adr/0001-salesforce-como-plataforma.md) |
| Repositório público, com a prevenção como única defesa de confidencialidade | [AGENTS.md](../../AGENTS.md), seção 1 |
| Acesso por app Lightning interno, controlado por permission set | [ADR-0003](../adr/0003-app-lightning-interno.md) |
| Projeto enquadrado como intraempreendedorismo, não como startup | [README](../../README.md) |
| POD de 2 pessoas, aceito pelo professor como exceção à regra de 3 | este diário |

## 3. Onde o agente errou

| Erro | Como foi percebido | O que mudou |
|---|---|---|
| Na **primeira versão** do [roteiro do grill](../produto/roteiro-grill.md) (20/11), o agente inferiu o processo a partir do mock e errou em pontos centrais: um único ciclo de vida para todas as RRs, aprovação de viagem sempre obrigatória e a persona principal em aberto. | A Nicoli revisou o texto e comparou com o que o POD vive no dia a dia. | No mesmo dia, o roteiro foi corrigido com o POD: **dois tipos de RR**, exclusivos (parceiro e interna, sem envio a terceiros), **aprovação de viagem condicional** ao deslocamento e o **PM como persona principal**. As 5 dores foram confirmadas pelo POD. O roteiro passou a separar o que foi confirmado (✅) do que ainda é hipótese. |
| O agente usou dados e termos técnicos internos da empresa, que poderiam expor dinâmicas que não podem ser públicas. | O POD encontrou esses termos ao revisar o que o agente escreveu, antes do merge. | Os termos foram retirados e trocados por descrições genéricas de mercado. O mock de referência foi reconstruído com dados sintéticos (PR #2). |

> Os termos removidos não são listados aqui de propósito: citá-los neste diário repetiria a exposição (AGENTS.md, seção 1).

## 4. Onde o POD interveio

| Intervenção | Motivo | Resultado |
|---|---|---|
| Revisão de tudo o que o agente escreveu antes de entrar no repositório | O repositório é público, e o agente não distingue sozinho o que é sensível | Nenhum termo interno chegou à `main` |
| Retirada dos termos técnicos internos | Confidencialidade (AGENTS.md, seção 1) | Os artefatos usam apenas linguagem genérica de mercado |
| Revisão da solução proposta pelo agente | A solução partia da primeira versão do problema, que tinha erros de processo | A solução passa a ser validada no grill do problema antes de virar PRD |
| Repositório mantido **público**; o agente tinha recomendado torná-lo privado | No plano gratuito do GitHub, a proteção da `main`, exigida pelo bootcamp, não funciona em repositório privado | Confidencialidade reforçada no AGENTS.md: a prevenção antes de cada commit é a única defesa |
| Entrevistas com **1 ou 2 PMs**; o agente tinha sugerido 2 ou 3 | _(POD: completar o motivo)_ | Os números das entrevistas são tratados como estimativas declaradas, não como medição |
| Grill P3: o POD definiu a métrica principal como **número de cliques** (de 10 a 12 para 2 a 3), em vez da recomendação do agente (tempo de reação) | O POD conhece a dor real: o esforço de navegação para gerenciar RRs, recursos e projetos | Cliques viraram a métrica principal e um critério de aceite; o tempo de reação ficou como métrica complementar |
| Grill P8: o POD exigiu a **visão inicial unificada** (indicadores + lista numa só tela) como Must; o agente tinha deixado os indicadores como Should | A visão única é a resposta à dor de visibilidade fragmentada | Virou o RF1 do PRD, com critério de aceite próprio |
| Grill P11: o POD considerou irreal a meta de carga de 2 s proposta pelo agente e definiu **10 s** | O volume de dados da carteira é grande | RNF1 ficou com 10 s para a visão completa, com os dados aparecendo antes da IA |
| Grill P7: o agente apontou o nome do fornecedor do PSA e da ferramenta de chat antes de gravar, e propôs versões genéricas | Confidencialidade (AGENTS.md, seção 1) | Os dois nomes ficaram fora do Lean Canvas |

## 5. Aprendizados que vão para o AGENTS.md

Aprovadas pelo POD e incluídas no [AGENTS.md](../../AGENTS.md) no PR #3:

- **Problema vem do POD, não do agente** (seção 2). O agente pergunta, registra o que foi confirmado, marca o resto como hipótese e registra no diário as escolhas do POD diferentes da recomendação.
- **Revisão de confidencialidade antes de cada commit** (seção 1). O agente lista os termos que podem ser internos e só grava depois da confirmação do POD.

## 6. Fechamento do checkpoint

Checkpoint fechado em 2026-11-21 com o merge do PR #3 e a tag `checkpoint-01`.

- [x] Grill do problema (`/grill-me` sobre a seção 8 do [roteiro](../produto/roteiro-grill.md)), com 11 perguntas
- [x] [Lean Canvas](../produto/lean-canvas.md) com a lente de intraempreendedorismo
- [x] [Hipótese](../produto/hipotese.md) no formato "Acreditamos que..."
- [x] [Esqueleto do PRD](../produto/prd.md) com os 6 pilares
- [x] Nome da iniciativa, proposta de valor e um dono por papel no README
- [x] Validação da divisão de papéis pela Nicoli: aprovada no PR #3
- [x] Proteção da `main`: ativa desde 2026-11-16 (ver seção 1)
- [x] Tag `checkpoint-01` na `main`: criada em 2026-11-21, no merge do PR #3
