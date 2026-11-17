# ADR-0001: Salesforce como plataforma

- **Status:** Aceito
- **Data:** 2026-11-16

## Contexto

O projeto nasce de uma necessidade real da empresa dos integrantes do POD, tratada de forma genérica. Essa necessidade só faz sentido dentro do ecossistema Salesforce, então a plataforma é um **pré-requisito**, não uma escolha entre alternativas. O uso de Salesforce foi alinhado com o professor da disciplina.

O bootcamp sugere stacks web comuns (React, shadcn/ui etc.) e exige:
- MVP numa **URL pública**, com o fluxo principal de ponta a ponta;
- CI com testes e eval da IA;
- C1 e C2 em LikeC4 condizentes com o que está rodando.

## Decisão

Construir o MVP em Salesforce, com Apex e LWC (API 68.0), usando o Salesforce DX como formato de código-fonte.

## Consequências

- **URL pública:** vai exigir um site público (Experience Cloud ou Salesforce Sites) ou outra forma de expor o fluxo principal. A decisão fica para um ADR próprio até o checkpoint 04.
- **CI:** testes Jest de LWC rodam sem org. Testes Apex exigem uma org (scratch org com Dev Hub ou org de desenvolvimento) e credenciais no CI guardadas como segredo. A decisão fica para um ADR próprio no checkpoint 04.
- **Design system:** o candidato natural é o SLDS, no lugar das sugestões do bootcamp. A decisão será registrada em ADR no checkpoint 03.
- **IA no produto:** as opções de IA (Einstein/Agentforce, chamadas a LLM externo via Apex etc.) precisam ser avaliadas no AI Canvas, considerando custo e licenças disponíveis numa org de desenvolvimento.
- **Confidencialidade:** usar só orgs de desenvolvimento ou scratch orgs com dados sintéticos, nunca orgs da empresa.
