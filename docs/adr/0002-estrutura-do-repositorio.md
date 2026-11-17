# ADR-0002: Estrutura do repositório

- **Status:** Aceito
- **Data:** 2026-11-16

## Contexto

O bootcamp exige um esqueleto de repositório comum a todos os PODs (`/src/`, `/docs/produto/`, `/docs/specs/`, `/docs/adr/`, `/docs/diario/`, `/docs/pitch/`, `/architecture/`, `/prototype/`, `/evals/`, `/.github/` e `/AGENTS.md`). Por padrão, o Salesforce DX usa `force-app/` como pasta de pacote, e o Spec Kit grava as specs em `specs/` na raiz.

O projeto precisa seguir as duas convenções sem quebrar o deploy e o retrieve para a org.

## Decisão

1. **`src/` é a pasta de pacote do Salesforce DX** (`packageDirectories[0].path = "src"` no `sfdx-project.json`). Os metadados ficam em `src/main/default/`. Os comandos `sf project deploy` e `sf project retrieve` continuam funcionando sem mudança, porque leem o caminho do `sfdx-project.json`.
2. **Specs do Spec Kit em `docs/specs/NNN-nome/`**, informando `SPECIFY_FEATURE_DIRECTORY` ao rodar `/speckit-specify`. Os comandos seguintes do Spec Kit leem o caminho de `.specify/feature.json`, então não é preciso alterar os scripts dele.
3. **`AGENTS.md` é o harness único.** O `CLAUDE.md` só o importa e acrescenta o que é específico do Claude Code.
4. As pastas de Salesforce (`manifest/`, `config/`, `scripts/`) continuam na raiz, porque as ferramentas esperam essa localização.
5. Arquivos `.gitkeep`, que mantêm pastas vazias no git, são ignorados no deploy via `.forceignore`.

## Consequências

- Validado com `sf project convert source`: uma classe Apex e um LWC em `src/main/default/` foram reconhecidos, e o `.gitkeep` ficou fora do pacote.
- Os templates internos do Spec Kit citam `specs/` como exemplo. Quem rodar `/speckit-specify` precisa seguir a regra do AGENTS.md, senão a spec vai para o lugar errado.
- Ao atualizar o Spec Kit, conferir se o mecanismo de `SPECIFY_FEATURE_DIRECTORY` continua existindo.
