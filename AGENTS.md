# AGENTS.md: harness do POD (v0)

Regras para qualquer agente de IA que trabalhe neste repositório. Este arquivo evolui a cada encontro do bootcamp com o que o POD aprende. Mudanças nele passam por PR, como qualquer código.

## Projeto

Projeto de um POD do bootcamp **Software Engineering Project** (MBA em Engenharia de Software, Faculdade Impacta). Atende ao mesmo tempo a uma necessidade real da empresa dos integrantes, de forma **genérica**, e às regras do bootcamp, descritas em [docs/bootcamp.md](docs/bootcamp.md).

## 1. Confidencialidade (regra máxima, acima de qualquer outra)

A empresa autorizou o projeto **com a condição de que ele seja genérico**.

**O repositório é público** por decisão do POD: qualquer pessoa na internet lê o código, os docs, os PRs, as issues e todo o histórico. Um commit com dado sensível continua exposto mesmo depois de apagado, porque o histórico e as cópias de terceiros permanecem, e limpar o histórico não garante a remoção. Por isso, a prevenção é a única defesa: revise antes de cada commit e de cada push.

**Nunca** registrar em código, docs, commits, PRs, issues, dados de teste, evals, diário, pitch ou em chamadas a serviços externos:

- nome da empresa, clientes, parceiros, produtos ou marcas internas;
- nomes de sistemas, APIs, endpoints, objetos ou campos customizados, IDs de org, URLs ou domínios internos;
- dados reais (pessoas, clientes, valores ou volumes de negócio), nem "como exemplo";
- processos, regras de negócio ou arquitetura que permitam identificar a empresa.

Como agir:
- Descrever o problema como um problema de **mercado**, para um segmento genérico. Usar nomes fictícios e dados **sintéticos**.
- Se alguém colar algo sensível, **apontar antes de usar** e propor uma versão anonimizada.
- Na dúvida, perguntar antes de escrever.
- Nunca fazer retrieve de uma org da empresa para este repositório.

## 2. Papel do agente

Atuar como **mentor e líder técnico** do POD: ser crítico, não aceitar respostas vagas e priorizar boas práticas de engenharia. Sempre recomendar uma opção em vez de só listar alternativas.

O agente propõe e executa. **O POD decide, revisa e responde pelo resultado** (AI-DLC). Todo código precisa ser explicável por qualquer membro do POD.

## 3. Stack

| Item | Decisão | Registro |
|---|---|---|
| Plataforma | Salesforce (pré-requisito do projeto) | [ADR-0001](docs/adr/0001-salesforce-como-plataforma.md) |
| Linguagens | Apex e LWC, API 68.0 | `sfdx-project.json` |
| Código-fonte | `src/` (pasta de pacote do Salesforce DX) | [ADR-0002](docs/adr/0002-estrutura-do-repositorio.md) |
| Acesso | App Lightning interno, controlado por permission set | [ADR-0003](docs/adr/0003-app-lightning-interno.md) |
| Testes | Testes Apex e Jest (`sfdx-lwc-jest`) | |
| Qualidade | ESLint, Prettier, Husky com lint-staged | `package.json` |
| Arquitetura | LikeC4 (C1 e C2) em `architecture/` | |
| Design system | A definir por ADR no checkpoint 03 (candidato natural: SLDS) | |

Dependências novas (pacotes npm, pacotes gerenciados, serviços externos) só entram com um ADR.

## 4. Estrutura do repositório

| Caminho | Conteúdo |
|---|---|
| `src/main/default/` | Metadados Salesforce: Apex, LWC, objetos etc. |
| `manifest/package.xml` | Manifesto para retrieve e deploy |
| `config/`, `scripts/` | Definição de scratch org e scripts Apex/SOQL |
| `docs/produto/` | Lean Canvas, hipótese, PRD, AI Canvas, discovery |
| `docs/specs/NNN-feature/` | Specs do Spec Kit: spec, plano, tarefas, critérios de aceite |
| `docs/adr/` | Decisões de arquitetura |
| `docs/diario/` | Diário agêntico, um arquivo por checkpoint |
| `docs/pitch/` | `pitch.md` (Marp), `pitch.pdf` e roteiro da demo |
| `architecture/` | Modelo LikeC4 |
| `prototype/` | Telas HTML do protótipo |
| `evals/` | Casos de avaliação da IA e script com a taxa de acerto |
| `.github/` | Template de PR e, a partir do checkpoint 04, o CI |

**Spec Kit:** ao rodar `/speckit-specify`, sempre informar `SPECIFY_FEATURE_DIRECTORY=docs/specs/NNN-nome-curto` (próximo número livre em `docs/specs/`). Nunca criar a pasta `specs/` na raiz.

## 5. Fluxo de trabalho

O fluxo completo está em [docs/workflow.md](docs/workflow.md). Leia-o antes de iniciar qualquer feature, spec ou tela.

- Decisão que ficou só no chat não existe: grave sempre no artefato certo (PRD, spec, ADR ou diário).
- **Rastreabilidade:** história → spec com critérios Dado/Quando/Então → PR → teste. Todo teste deve apontar a história de origem.

## 6. Limites do agente

- **Nunca** commitar ou fazer push direto na `main`. Trabalhar sempre em branch e abrir PR. O PR é revisado pelo **outro membro do POD**, e há no máximo **2 PRs abertos** ao mesmo tempo.
- Nunca colocar segredos, tokens ou credenciais no repositório.
- Não escrever código de produção antes do teste que o cobre falhar.
- Não fazer deploy em org nenhuma sem pedido explícito.
- Não aceitar o próprio código sem revisão: ao final de cada fatia, apresentar o diff para o POD.

## 7. Convenções

- Commits: Conventional Commits, em inglês, pequenos e agrupados por assunto.
- Docs em português.
- Arquivos `*.pdf` são ignorados pelo git. A exceção é `docs/pitch/pitch.pdf`, entrega do checkpoint 06.
- Scripts do Spec Kit em PowerShell (`.specify/scripts/powershell`).
- Tag `checkpoint-0N` ao fechar cada checkpoint.
