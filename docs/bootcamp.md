# Contexto do bootcamp

Disciplina **Software Engineering Project – Bootcamp** do MBA em Engenharia de Software da Faculdade Impacta. Fonte: material da Aula 01 (PDF local, fora do git).

## Objetivo

Criar uma **startup com IA** e entregar um **MVP rodando**, trabalhando como um **POD corporativo** e seguindo o método **AI-DLC** (IA orquestra, humanos decidem e respondem pelo resultado). São 24h em 6 encontros, e cada encontro é uma sprint que termina num checkpoint.

## Quatro regras inegociáveis

1. **Startup com IA:** problema real, persona real e IA como parte da proposta de valor. Teste: se tirarmos a IA e o produto ainda resolver a dor, a IA é enfeite.
2. **MVP rodando:** URL pública e fluxo principal de ponta a ponta.
3. **Desenvolvimento agêntico:** seguindo o AI-DLC, com governança humana.
4. **Arquitetura como código:** C1 (contexto) e C2 (containers) modelados em LikeC4, no repositório e condizentes com o que está rodando.

## Checkpoints

A tag `checkpoint-0N` deve ser criada no repositório até as 22h40 de cada encontro.

| # | Encontro | Entrega mínima no repositório |
|---|---|---|
| 01 | Times e desafio | README com startup, POD e papéis; Lean Canvas; hipótese ("Acreditamos que..."); PRD com os 6 pilares (mesmo raso); AGENTS.md v0 |
| 02 | Produto | Evidências de discovery, AI Canvas (`/docs/produto/ai-canvas.md`), MoSCoW do MVP, histórias com critérios de aceite, PRD v1 |
| 03 | Protótipo | Telas HTML testadas com 2+ usuários, design system escolhido (ADR), diário #1 |
| 04 | Design C1/C2 | C1 e C2 em LikeC4, ADRs, walking skeleton no ar com deploy e CI |
| 05 | MVP | URL pública, fluxo principal ponta a ponta, testes e eval da IA no CI, rastreabilidade, diário #2 |
| 06 | Pitch | Pitch ao vivo (10 min) com demo na URL pública e material em `/docs/pitch/` |

**Avaliação:** checkpoints 01–05 valem 40% (8% cada, avaliados pela tag) e o pitch final vale 60%.

## Estrutura obrigatória do repositório

| Caminho | Conteúdo |
|---|---|
| `/README.md` | Startup, POD, papéis e URL do MVP |
| `/AGENTS.md` | Harness do agente: regras, stack e limites (evolui a cada encontro) |
| `/docs/produto/` | Lean Canvas, AI Canvas, PRD e evidências de discovery |
| `/docs/specs/` e `/docs/adr/` | Histórias, critérios de aceite e decisões de arquitetura |
| `/docs/diario/` | Diário agêntico, um arquivo por checkpoint |
| `/docs/pitch/` | `pitch.md` (Marp ou Slidev), `pitch.pdf` exportado dele e roteiro da demo |
| `/architecture/` | Modelo LikeC4 (C1 e C2) |
| `/prototype/` | Telas HTML do protótipo |
| `/evals/` | 10–20 casos de avaliação da IA (comuns, difíceis e adversariais) e script com a taxa de acerto, rodando no CI |
| `/src/` e `/.github/` | Código do MVP e CI com testes e eval |

## Regras do repositório e do POD

- **`main` protegida:** merge só via PR, revisado por **outro membro do POD** e com CI verde.
- **Limite de WIP:** no máximo **2 PRs abertos** ao mesmo tempo.
- **Diário versionado:** o que o agente fez, onde errou e onde o POD interveio.
- **Em aula, trabalho em mob** (operador e navegadores, com rodízio a cada 15–20 min). Entre as aulas, trabalho assíncrono via PRs.
- O professor deve ser colaborador do repositório. **O que não estiver no Git não existe para o checkpoint.**

### Papéis (3 pessoas por POD)

| Papel | Responde por |
|---|---|
| Product Owner | PRD, histórias e validação com usuários |
| Tech Lead | Harness (AGENTS.md) e arquitetura C1/C2 |
| Quality & Ops | CI, testes, deploy e métricas |

Todos operam agentes e revisam PRs.

## Anti-vibecoding

- Em todo checkpoint, o professor sorteia uma pessoa e um trecho de código. Ela precisa explicar o que o código faz, de qual história veio e por que foi aceito. Se ninguém souber explicar, o checkpoint não conta.
- **Teste do bootcamp:** se o código for apagado, ele precisa poder ser regenerado a partir do repositório (specs, harness e ADRs).
- **Rastreabilidade:** história → spec (critérios Dado/Quando/Então) → PR → teste. Quando um teste falha, é preciso mostrar de qual história ele veio.

## Vocabulário AI-DLC e como as nossas ferramentas se encaixam

| AI-DLC | Bootcamp | Nossa ferramenta |
|---|---|---|
| Inception (aulas 01–02) | PRD, histórias, unidades de trabalho | grill-me, `/speckit-constitution`, `/speckit-specify`, `/speckit-clarify` |
| Mob Elaboration | O POD responde às perguntas da IA | grill-me e `/speckit-clarify` |
| Unit of Work | Épico (bloco do MVP) | Uma feature em `docs/specs/NNN-*` |
| Bolt | Ciclo dentro do encontro | Uma fatia de `/speckit-implement` |
| Construction (aulas 03–05) | O agente gera código e testes, o POD revisa | `/speckit-plan` → `tasks` → `implement` → `/code-review` |
| Operation (aulas 05–06) | Deploy, métricas e pitch | CI, evals, `/speckit-converge` |
| Steering files | AGENTS.md | AGENTS.md (CLAUDE.md aponta para ele) |

## Outras diretrizes da disciplina

- **Lean Canvas:** começar pelo problema, depois segmentos e proposta de valor; só então a solução.
- **Hipótese:** "Acreditamos que [solução] para [público] vai gerar [resultado]. Saberemos que é verdade quando [métrica] mudar."
- **PRD (6 pilares):** visão, público-alvo, requisitos funcionais, requisitos não funcionais, critérios de aceite testáveis e métricas de sucesso.
- **Histórias:** "Como [persona], quero [ação], para [benefício]", seguindo o INVEST.
- **Protótipo:** HTML puro e sem estilo, gerado a partir das histórias. Valida o fluxo, não as cores. O design system vem depois, por ADR (sugestões: shadcn/ui, Material Design 3, Carbon).
- **IA no produto:** chat quando a intenção é aberta, interface quando a tarefa é precisa. IA dentro do fluxo vale mais que um chatbot colado.
- **Segurança:** nenhum segredo no repositório, LGPD e casos adversariais no eval.
- **Observabilidade:** a métrica principal instrumentada no MVP.
- **Ferramenta livre, método fixo:** o Spec Kit é explicitamente bem-vindo.
