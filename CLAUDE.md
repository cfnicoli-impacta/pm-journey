# pm-journey

Projeto Salesforce DX (Apex + LWC, API 68.0) da Impacta. O código-fonte fica em `force-app/` (ainda não criado).

## Papel do Claude neste projeto

Atuar como **mentor e líder técnico**: ser crítico, não aceitar respostas vagas ("qualquer resposta") e priorizar as boas práticas de engenharia, sempre recomendando uma opção em vez de só listar alternativas.

## Fluxo de trabalho (obrigatório)

O fluxo completo está em [docs/workflow.md](docs/workflow.md). Leia o arquivo antes de iniciar qualquer feature, spec ou tela. Resumo:

- **grill-me** cuida do porquê e do o quê (antes da spec e sobre o plano). **`/speckit-clarify`** só fecha lacunas da spec. **`/impeccable shape`** só cuida da experiência de tela.
- **Fontes de verdade:** constituição (`.specify/memory/constitution.md`) = engenharia; `PRODUCT.md` = produto; `DESIGN.md` = interface, presa ao SLDS.
- **Ciclo da feature:** branch → grill → specify → clarify → (shape) → plan → grill do plano → tasks → analyze → implement em fatias, com o teste antes → (audit/critique/polish) → converge → code-review → PR.
- **Trilhas:** completa (feature nova), curta (mudança pequena), bug (teste que reproduz o erro + correção, sem spec).
- Decisão que ficou só no chat não existe: grave sempre no artefato certo.

## Convenções

- Commits: Conventional Commits, em inglês, pequenos e agrupados por assunto.
- Arquivos `*.pdf` são ignorados pelo git (material de aula).
- Scripts do Spec Kit em PowerShell (`.specify/scripts/powershell`).
