# pm-journey

> Nome da iniciativa e proposta de valor: **a definir** no Lean Canvas (checkpoint 01).

Projeto do bootcamp **Software Engineering Project** do MBA em Engenharia de Software da Faculdade Impacta, desenvolvido com IA seguindo o método AI-DLC.

## Intraempreendedorismo, não startup

O bootcamp pede uma "startup com IA". Este POD aplica a mesma regra como **iniciativa de intraempreendedorismo**: não há empresa nova. Somos colaboradores que identificaram uma oportunidade de melhorar um processo dentro da empresa onde trabalhamos.

O que muda em relação a uma startup:

- **Cliente:** áreas e pessoas internas, não um mercado externo. A persona é real e acessível.
- **Receita:** é substituída por **valor para o negócio** (tempo economizado, retrabalho evitado, prazo cumprido). O Lean Canvas e o pitch usam essa lente.
- **Confidencialidade:** o produto é descrito de forma genérica, como um problema de mercado (ver seção 1 do [AGENTS.md](AGENTS.md)).

As outras regras do bootcamp continuam iguais: problema real, IA como parte da proposta de valor e MVP rodando.

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
