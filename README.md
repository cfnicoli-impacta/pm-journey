# pm-journey

> Nome da startup e proposta de valor: **a definir** no Lean Canvas (checkpoint 01).

Projeto do bootcamp **Software Engineering Project** do MBA em Engenharia de Software da Faculdade Impacta, desenvolvido com IA seguindo o método AI-DLC.

## POD

| Membro | Papéis |
|---|---|
| Nicoli | Product Owner · Tech Lead · Quality & Ops |
| Matheus | Product Owner · Tech Lead · Quality & Ops |

## MVP

- **URL pública:** a definir (checkpoint 05)
- **Plataforma:** Salesforce (Apex + LWC). Ver [ADR-0001](docs/adr/0001-salesforce-como-plataforma.md).

## Como navegar

| Para | Veja |
|---|---|
| Regras para agentes de IA | [AGENTS.md](AGENTS.md) |
| Regras e checkpoints do bootcamp | [docs/bootcamp.md](docs/bootcamp.md) |
| Fluxo de trabalho do POD | [docs/workflow.md](docs/workflow.md) |
| Produto (Lean Canvas, PRD, AI Canvas) | [docs/produto/](docs/produto/) |
| Specs e decisões | [docs/specs/](docs/specs/) · [docs/adr/](docs/adr/) |
| Código Salesforce | [src/](src/) |

## Desenvolvimento

```bash
npm install                 # dependências de lint, formatação e testes
npm run test:unit           # testes Jest de LWC
sf project deploy start     # deploy de src/ para a org padrão
sf project retrieve start -x manifest/package.xml
```

Use apenas orgs de desenvolvimento ou scratch orgs com dados sintéticos.
