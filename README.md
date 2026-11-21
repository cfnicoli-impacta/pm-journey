# pm-journey

> **A próxima ação certa para cada requisição de recurso, explicada pela IA e a até 3 cliques.**

Iniciativa de intraempreendedorismo para Gerentes de Projetos e Gerentes de Recursos de empresas de serviços profissionais de tecnologia. Ver [Lean Canvas](docs/produto/lean-canvas.md), [hipótese](docs/produto/hipotese.md) e [PRD](docs/produto/prd.md).

Projeto do bootcamp **Software Engineering Project** do MBA em Engenharia de Software da Faculdade Impacta, desenvolvido com IA seguindo o método AI-DLC.

## Intraempreendedorismo, não startup

O bootcamp pede uma "startup com IA". Este POD aplica a mesma regra como **iniciativa de intraempreendedorismo**: não há empresa nova. Somos colaboradores que identificaram uma oportunidade de melhorar um processo dentro da empresa onde trabalhamos.

O que muda em relação a uma startup:

- **Cliente:** áreas e pessoas internas, não um mercado externo. A persona é real e acessível.
- **Receita:** é substituída por **valor para o negócio** (tempo economizado, retrabalho evitado, prazo cumprido). O Lean Canvas e o pitch usam essa lente.
- **Confidencialidade:** o produto é descrito de forma genérica, como um problema de mercado (ver seção 1 do [AGENTS.md](AGENTS.md)).

As outras regras do bootcamp continuam iguais: problema real, IA como parte da proposta de valor e MVP rodando.

## POD

POD de 2 pessoas, aceito pelo professor como exceção à regra de 3.

| Membro | Papel | Responde por | Revisa |
|---|---|---|---|
| Matheus | Product Owner | PRD, histórias, entrevistas e validação com usuários | CI, testes e deploy |
| Nicoli | Tech Lead · Quality & Ops | AGENTS.md, arquitetura C1/C2, CI, testes, deploy e métricas | PRD e histórias |

Os dois operam agentes e revisam PRs. O papel define quem responde pelo artefato.

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
