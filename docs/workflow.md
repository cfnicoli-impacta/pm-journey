# Fluxo de trabalho: Spec Kit + grill-me + Impeccable no bootcamp

Este documento define como as três skills se combinam no pm-journey, seguindo o método AI-DLC e os checkpoints do bootcamp ([docs/bootcamp.md](bootcamp.md)).

## 1. Papel de cada skill

| Skill | Papel | Gera | Risco se usada sem critério |
|---|---|---|---|
| **grill-me** (`/grill-me` → skill `grilling`) | Testar ideias: monta uma árvore de decisões e pergunta em rodadas, sempre com uma resposta recomendada. É a "Mob Elaboration" do AI-DLC | Nada em arquivo | As decisões ficam perdidas no chat |
| **Spec Kit** (`/speckit-*`) | Processo e rastreabilidade: constituição → spec → plano → tarefas → código | `docs/specs/NNN-feature/` e `.specify/memory/constitution.md` | Burocracia, specs vagas e um `implement` que gera muito código sem revisão |
| **Impeccable** (`/impeccable <comando>`) | Qualidade de interface, só depois do ADR de design system | Briefs, `DESIGN.md` e relatórios | Puxa para um design autoral, que briga com o SLDS e com o protótipo sem estilo |

### Quem entrevista o quê

- **grill-me** cuida do *porquê* e do *o quê*: problema, escopo, trade-offs e o que fica de fora. Roda antes de existir documento e de novo sobre o plano técnico.
- **`/speckit-clarify`** é só uma checagem de lacunas na spec, com no máximo 5 perguntas.
- **`/impeccable shape`** cuida só da experiência de tela, e só a partir do checkpoint 03.

**Regra:** toda sessão de grill termina com o resultado gravado no artefato certo. Decisão que ficou só no chat não existe.

### Fontes de verdade

| Arquivo | Responde |
|---|---|
| `docs/produto/` (Lean Canvas, PRD, AI Canvas) | Para quem e por quê (produto) |
| `.specify/memory/constitution.md` | Como construímos (engenharia) |
| `docs/adr/` | Por que cada decisão técnica foi tomada |
| `DESIGN.md` (a partir do checkpoint 03) | Como a interface se parece (preso ao design system do ADR) |
| `AGENTS.md` | Regras e limites do agente (harness) |

Os arquivos apontam uns para os outros em vez de copiar conteúdo. Se o Impeccable pedir um `PRODUCT.md`, ele deve ser um resumo derivado do PRD, que continua sendo a fonte.

## 2. Mapa por checkpoint

| CP | Fase AI-DLC | Ferramentas | Entregas |
|---|---|---|---|
| 01 | Inception | **grill-me** sobre o problema | README, Lean Canvas, hipótese, PRD raso, AGENTS.md v0 |
| 02 | Inception | grill-me, `/speckit-constitution`, `/speckit-specify` + `/speckit-clarify` por épico | Discovery, AI Canvas, MoSCoW, histórias com critérios, PRD v1 |
| 03 | Construction | Agente gera `prototype/` em HTML puro a partir das specs; teste com 2+ usuários; ADR de design system; **só então** `/impeccable shape` | Protótipo testado, ADR, diário #1 |
| 04 | Construction | `/speckit-plan` + grill do plano; ADRs (URL pública, CI); LikeC4 | C1/C2, walking skeleton no ar com deploy e CI |
| 05 | Construction → Operation | `/speckit-tasks` → `analyze` → `implement` em fatias; evals; `/impeccable audit` + `critique` → `polish` | URL pública, fluxo de ponta a ponta, testes e eval no CI, diário #2 |
| 06 | Operation | `/speckit-converge`, pitch em Marp | Pitch e demo |

**Ao fechar cada checkpoint:** atualizar o diário (`docs/diario/checkpoint-0N.md`), evoluir o AGENTS.md com o que aprendemos e criar a tag `checkpoint-0N` na `main`.

## 3. Ciclo de cada feature (Unit of Work)

| # | Passo | Bloqueia o avanço se... |
|---|---|---|
| 1 | Criar a branch `NNN-nome` | |
| 2 | `/grill-me` sobre a ideia da feature | o problema ou o critério de sucesso não estiver claro |
| 3 | `/speckit-specify` com `SPECIFY_FEATURE_DIRECTORY=docs/specs/NNN-nome` | |
| 4 | `/speckit-clarify` | sobrar algum `[NEEDS CLARIFICATION]` |
| 5 | *(com interface, a partir do CP03)* `/impeccable shape` → brief em `docs/specs/NNN-nome/ui-brief.md` | |
| 6 | `/speckit-plan` | o plano violar a constituição sem justificativa escrita |
| 7 | **`/grill-me` sobre o plano** (limites de execução do Salesforce, permissões de acesso a dados, processamento em lote) | houver uma decisão de arquitetura sem alternativa considerada, ou se ela não virar ADR |
| 8 | `/speckit-checklist` *(opcional: segurança, acessibilidade, LGPD)* | |
| 9 | `/speckit-tasks` → `/speckit-analyze` | o analyze apontar algo CRITICAL |
| 10 | `/speckit-implement` **em fatias** (um bolt = uma história), escrevendo o teste antes e com um commit por tarefa | o teste não falhar antes da implementação |
| 11 | *(com interface)* `/impeccable audit` + `critique` → `polish` | houver problema de acessibilidade abaixo do padrão WCAG AA |
| 12 | `/speckit-converge` → `/code-review` → PR | sobrar tarefa aberta ou achado de correção |
| 13 | **Revisão do PR pelo outro membro do POD** → merge | o revisor não souber explicar o código, o CI estiver vermelho ou já houver 2 PRs abertos |

### Trilhas por tamanho

| Trilha | Quando | Passos |
|---|---|---|
| **Completa** | Feature nova, ou mudança de modelo de dados ou de arquitetura | Todos os passos acima |
| **Curta** | Mudança pequena e bem entendida | specify → tasks → implement → PR |
| **Bug** | Correção | Teste que reproduz o erro → correção → PR. Sem spec |
| **Docs/infra** | Artefatos de produto, ADR, estrutura | Branch → PR revisado |

## 4. Pontos de atenção

- **Confidencialidade:** cada artefato, inclusive spec, eval e diário, passa pela seção 1 do AGENTS.md. É a primeira linha do checklist do PR.
- **Impeccable com LWC:** o `critique` e o detector precisam ver a tela renderizada. Com LWC, isso exige uma scratch org ou o servidor de desenvolvimento local; sem isso, a análise roda incompleta. Telas internas usam o modo **Operate**.
- **`/speckit-implement` sem rédea** gera código mais rápido do que o POD revisa: é vibecoding com outro nome. O limite de 2 PRs abertos vale para o agente também.
- **Anti-vibecoding:** qualquer membro precisa explicar qualquer trecho de código, de qual história veio e por que foi aceito.
- **Hooks do Impeccable** não estão instalados de propósito. Avaliar no CP03.

## 5. Constituição: ponto de partida

> Ainda é um rascunho. Cada princípio deve ser debatido com o grill antes de entrar na constituição pelo `/speckit-constitution` (CP02).

1. **Spec antes de código.** A exceção é a trilha de bug.
2. **Testes primeiro.** Testes Apex e Jest para LWC. Os 75% de cobertura do Salesforce são o mínimo, não a meta: proposta de ≥ 85%, com asserts reais e testes com 200 registros.
3. **Limites de execução e lote.** Nenhuma consulta SOQL ou gravação DML dentro de loop. Um trigger por objeto, com a lógica numa classe handler.
4. **Segurança por padrão.** `with sharing` sempre, consultas em `WITH USER_MODE` e verificação de permissão de objeto e campo antes de ler ou gravar. Nenhum segredo no repositório.
5. **Declarativo antes de código.** Se um Flow resolve bem, não se escreve Apex. Nada de construir o que ainda não é necessário.
6. **Interface.** Design system definido por ADR (candidato: SLDS) e acessibilidade WCAG AA.
7. **IA com prova.** Toda funcionalidade de IA tem eval com casos comuns, difíceis e adversariais, rodando no CI.
8. **Entrega.** Commits pequenos (Conventional Commits), PR revisado pelo outro membro do POD e no máximo 2 PRs abertos.
