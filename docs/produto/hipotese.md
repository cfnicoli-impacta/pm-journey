# Hipótese de valor

> **Origem:** grill do problema do checkpoint 01 (P4), a partir das decisões P1 a P3.
> **Status:** a validar. As linhas de base vêm das entrevistas com PMs no checkpoint 02.

> **Acreditamos que** uma tela única com a próxima melhor ação gerada por IA, que prioriza as RRs em risco e explica o motivo de cada recomendação,
> **para** Gerentes de Projetos (PM) e Gerentes de Recursos (RM) que acompanham RRs de parceiros e internas,
> **vai gerar** menos esforço e reação mais rápida para destravar RRs antes da data de início.
> **Saberemos que é verdade quando** o número de cliques para identificar e executar a ação necessária cair de 10 a 12 para 2 a 3, e o tempo de reação diminuir em relação à linha de base das entrevistas.

## Como cada parte se conecta

| Parte | Decisão | Artefato |
|---|---|---|
| Solução: priorizar e explicar | P1: a IA combina sinais e justifica | [Lean Canvas](lean-canvas.md#3-proposta-de-valor-única) |
| Solução: só recomendar | P2: o PM executa, a IA não | [PRD](prd.md#3-requisitos-funcionais) |
| Métricas | P3: cliques (principal) e tempo de reação (complementar) | [PRD](prd.md#6-métricas-de-sucesso) |

**Ordem de validação (P9):** primeiro com o PM, persona do MVP; depois com o RM, quando a visão do RM (RF8 do PRD) for construída.

## Como invalidar

A hipótese é **falsa** se, no teste do protótipo (checkpoint 03) ou do MVP (checkpoint 05):

- o fluxo continuar exigindo mais de 3 cliques para a ação mais comum; ou
- os PMs ignorarem a ordem sugerida pela IA e voltarem a montar a prioridade sozinhos, o que indicaria que a priorização não gera confiança.
