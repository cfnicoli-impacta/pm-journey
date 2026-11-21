# Lean Canvas

> **Enquadramento:** intraempreendedorismo (ver [README](../../README.md)). O cliente é interno e "receita" significa valor para o negócio.
> **Origem:** grill do problema do checkpoint 01 (P1 a P11), a partir do [roteiro](roteiro-grill.md). Valores atuais são estimativas do POD, a validar nas entrevistas do checkpoint 02.
> **Confidencialidade:** descrição genérica de mercado (AGENTS.md, seção 1).

Ordem de preenchimento (slide 30 da Aula 01): problema → segmentos → proposta de valor → solução e demais blocos.

## 1. Problema

Em empresas de serviços profissionais de tecnologia, o Gerente de Projetos (PM) abre Requisições de Recurso (RRs) para ter pessoas no início de cada projeto e não consegue saber, de forma confiável, quais estão em risco e o que fazer primeiro.

1. **Visibilidade fragmentada:** não há uma visão única do estado de todas as RRs do PM.
2. **Problemas descobertos tarde:** rejeições, bloqueios de configuração e viagens pendentes aparecem perto da data de início.
3. **Automação falha em silêncio:** RRs ficam paradas por falta de pré-requisito, sem aviso.
4. **Cobrança manual:** o PM persegue parceiros e aprovadores.
5. **Risco de começar o projeto sem recurso**, com impacto no cliente.

**Alternativas atuais:**
- Relatórios e listas em telas separadas, com o PM juntando os dados e deduzindo a ação.
- Cobrança manual de parceiros e aprovadores por e-mail e chat corporativo.

## 2. Segmentos de clientes

- **Usuário principal:** Gerente de Projetos (PM) que depende de RRs de parceiro e internas.
- **Usuário secundário:** Gerente de Recursos (RM), que também gerencia RRs e recursos e recebe as escalações do PM.
- **Early adopters:** os 1 ou 2 PMs entrevistados no checkpoint 02, que também testam o protótipo no checkpoint 03.

## 3. Proposta de valor única

**PM Journey: a próxima ação certa para cada requisição de recurso, explicada pela IA e a até 3 cliques.** (P5)

O diferencial da IA, decidido no grill (P1):
- **Combina sinais** (tipo da RR, dias até o início, histórico do parceiro, SLA, viagem e pré-requisitos) numa **prioridade única de risco** da carteira do PM, algo que regras com pesos fixos não fazem bem.
- **Justifica em linguagem natural** por que cada ação vem antes das outras, para o PM agir com confiança.
- **Antecipar** problemas antes do alerta disparar fica como evolução, porque depende de padrões de histórico difíceis de provar com dados sintéticos.

## 4. Solução

- Uma tela única com as RRs em risco da carteira do PM.
- A próxima melhor ação para cada RR, priorizada e explicada pela IA.
- A ação executada a partir da própria tela, em até 3 cliques. A IA recomenda; o PM executa.

## 5. Canais

- App Lightning dentro da plataforma que o PM já usa, liberado por permission set ([ADR-0003](../adr/0003-app-lightning-interno.md)).
- Adoção começa pelos early adopters e se espalha por indicação entre PMs.

## 6. Valor para o negócio (no lugar de receitas)

- Horas de PM e RM economizadas em navegação e cobrança.
- Menos projetos começando sem recurso, com menos impacto no cliente.
- Problemas descobertos antes da data de início, não perto dela.

## 7. Custos

- Horas do POD para construir e manter.
- Custo de cada chamada à IA por recomendação.
- Licenças da plataforma que já existem, sem custo novo de ferramenta.

## 8. Métricas-chave

| Nível | Métrica | Hoje | Meta |
|---|---|---|---|
| **Principal** | Cliques para o PM ou RM identificar e executar a ação necessária sobre uma RR | 10 a 12 | 2 a 3 |
| Complementar | Tempo de reação: da RR entrar em risco até a primeira ação do PM | _(linha de base nas entrevistas)_ | _(definir no CP02)_ |
| Resultado | % de RRs confirmadas até a data de início | _(linha de base nas entrevistas)_ | _(definir no CP02)_ |

Os valores atuais são uma estimativa declarada pelo POD, a validar nas entrevistas com PMs (checkpoint 02).

## 9. Vantagem injusta

- **Lacuna real:** nem a solução de PSA nem o que já existe implementado oferecem uma tela unificada nativa com essas funcionalidades.
- **Conhecimento de domínio:** o POD vive o processo no dia a dia e conhece as dores reais.
- **Roda onde os dados já estão:** sem integração nem ferramenta nova para o PM aprender.
