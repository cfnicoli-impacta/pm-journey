# Fluxo de trabalho: Spec Kit + grill-me + Impeccable

Este documento define como as três skills se combinam no desenvolvimento do pm-journey.

## 1. Papel de cada skill

| Skill | Papel | Gera | Risco se usada sem critério |
|---|---|---|---|
| **grill-me** (`/grill-me` → skill `grilling`) | Testar ideias: monta uma árvore de decisões e pergunta em rodadas, sempre com uma resposta recomendada | Nada em arquivo | As decisões ficam perdidas no chat |
| **Spec Kit** (`/speckit-*`) | Processo e rastreabilidade: constituição → spec → plano → tarefas → código | `specs/NNN-feature/` e `.specify/memory/constitution.md` | Burocracia, specs vagas e um `implement` que gera muito código sem revisão |
| **Impeccable** (`/impeccable <comando>`) | Qualidade de interface: produto, design, revisão e acabamento | `PRODUCT.md`, `DESIGN.md`, briefs e relatórios | Puxa para um design ousado e autoral, o que no Salesforce briga com o SLDS |

### Quem entrevista o quê

- **grill-me** cuida do *porquê* e do *o quê*: problema, escopo, trade-offs e o que fica de fora. Roda antes de existir documento e de novo sobre o plano técnico.
- **`/speckit-clarify`** é só uma checagem de lacunas na spec, com no máximo 5 perguntas. Não é para repensar o produto.
- **`/impeccable shape`** cuida só da experiência de tela, e só em features com interface.

**Regra:** toda sessão de grill termina com o resultado gravado no artefato certo. Decisão que ficou só no chat não existe.

### Fontes de verdade

Cada arquivo responde a uma pergunta, e a constituição *aponta* para os outros dois em vez de copiar o conteúdo.

| Arquivo | Responde |
|---|---|
| `.specify/memory/constitution.md` | Como construímos (engenharia) |
| `PRODUCT.md` | Para quem e por quê (produto) |
| `DESIGN.md` | Como a interface se parece (preso ao SLDS) |

## 2. Fase 0: fundação (uma vez só)

1. **`/grill-me` sobre o produto:** problema, usuários, escopo do MVP e o que o sistema *não* faz.
2. **`/impeccable init`** grava isso no `PRODUCT.md`.
3. **`/speckit-constitution`** define os princípios de engenharia (ponto de partida na seção 5).
4. **`DESIGN.md` preso ao SLDS**, só quando houver a primeira tela. O Impeccable não deve inventar um visual próprio.

## 3. Fase 1: ciclo de cada feature

| # | Passo | Bloqueia o avanço se... |
|---|---|---|
| 1 | Criar a branch `NNN-nome` manualmente (a extensão de git do Spec Kit não está instalada) | |
| 2 | `/grill-me` sobre a ideia da feature | o problema ou o critério de sucesso não estiver claro |
| 3 | `/speckit-specify` usando o resultado do grill | |
| 4 | `/speckit-clarify` | sobrar algum `[NEEDS CLARIFICATION]` |
| 5 | *(só com interface)* `/impeccable shape` → brief salvo em `specs/NNN-feature/ui-brief.md` | |
| 6 | `/speckit-plan` | o plano violar a constituição sem justificativa escrita |
| 7 | **`/grill-me` sobre o plano** (limites de execução do Salesforce, permissões de acesso a dados, processamento em lote) | houver uma decisão de arquitetura sem alternativa considerada |
| 8 | `/speckit-checklist` *(opcional: segurança, acessibilidade)* | |
| 9 | `/speckit-tasks` → `/speckit-analyze` | o analyze apontar algo CRITICAL |
| 10 | `/speckit-implement` **em fatias** (uma user story por vez), escrevendo o teste antes e com um commit por tarefa | o teste não falhar antes da implementação |
| 11 | *(só com interface)* `/impeccable audit` + `/impeccable critique` → `/impeccable polish` | houver problema de acessibilidade abaixo do padrão WCAG AA |
| 12 | `/speckit-converge` → `/code-review` → PR | sobrar tarefa aberta ou achado de correção |

### Trilhas por tamanho

Usar o fluxo inteiro para tudo é tão ruim quanto não ter fluxo.

| Trilha | Quando | Passos |
|---|---|---|
| **Completa** | Feature nova, ou mudança de modelo de dados ou de arquitetura | Todos os passos acima |
| **Curta** | Mudança pequena e bem entendida | specify → tasks → implement → review |
| **Bug** | Correção | Teste que reproduz o erro → correção → review. Sem spec |

## 4. Pontos de atenção

- **Impeccable com LWC:** o `critique` e o detector precisam ver a tela renderizada. Com LWC, isso exige uma scratch org ou o servidor de desenvolvimento local; sem isso, a análise roda incompleta (o relatório avisa no topo). Telas internas usam o modo **Operate**: consistência e precisão, não um visual chamativo.
- **`/speckit-implement` sem rédea** gera muito código de uma vez. Revise o diff ao final de cada fatia, porque código que ninguém revisou não é de ninguém.
- **Hooks do Impeccable** não estão instalados de propósito. Avaliar se vale ligá-los quando houver UI.

## 5. Constituição: ponto de partida

> Ainda é um rascunho. Cada princípio deve ser debatido com o grill antes de entrar na constituição pelo `/speckit-constitution`.

1. **Spec antes de código.** A exceção é a trilha de bug.
2. **Testes primeiro.** Testes Apex e Jest para LWC. Os 75% de cobertura do Salesforce são o mínimo, não a meta: proposta de ≥ 85%, com asserts reais e testes com 200 registros.
3. **Limites de execução e lote.** Nenhuma consulta SOQL ou gravação DML dentro de loop. Um trigger por objeto, com a lógica numa classe handler.
4. **Segurança por padrão.** `with sharing` sempre, consultas em `WITH USER_MODE` e verificação de permissão de objeto e campo antes de ler ou gravar.
5. **Declarativo antes de código.** Se um Flow resolve bem, não se escreve Apex. Nada de construir o que ainda não é necessário.
6. **Interface.** SLDS e componentes base da Lightning, com acessibilidade WCAG AA.
7. **Entrega.** Commits pequenos no padrão Conventional Commits e PR com revisão.
