# Roteiro para o grill do problema

Insumo para a sessão de `/grill-me` do checkpoint 01. Organiza o que já foi decidido, o que ainda é hipótese e onde estão as decisões em aberto, para que o grill percorra a árvore de decisões sem redescobrir o óbvio.

> **Status:** discovery em andamento. Itens marcados como ✅ foram confirmados pelo POD; itens marcados como **hipótese** ainda precisam de evidência.
> **Confidencialidade:** descrição genérica de mercado, com dados sintéticos (AGENTS.md, seção 1).

**Referência visual:** [mock-referencia.html](mock-referencia.html) (abrir no navegador), a ideia inicial reconstruída com dados sintéticos e em inglês, como a interface original.

## 1. Contexto de mercado

Empresas de **serviços profissionais de tecnologia** (implantação, suporte e consultoria) usam uma solução de **PSA (Professional Services Automation)** sobre o Salesforce para gerir projetos, recursos e horas.

Quando um projeto precisa de gente, o **Gerente de Projetos (PM)** abre uma **Requisição de Recurso (RR)**: papel, período, horas por dia, prioridade, local e se exige deslocamento.

✅ **Há dois tipos de RR, mutuamente exclusivos:**
- **RR de parceiro:** atendida exclusivamente por um prestador terceirizado, que recebe a RR, aceita ou rejeita, e indica quem vai atender.
- **RR interna:** atendida exclusivamente por um profissional da própria empresa, alocado diretamente, sem envio a terceiros.

Uma **automação de alocação** processa as RRs e faz o match usando "pools" de prioridade (cliente prioritário, projeto ativo, mesmo projeto, geral). Ela depende de pré-requisitos de configuração: nível (tier) do projeto, taxa de custo do serviço na região etc. Quando a RR exige deslocamento, há também uma **aprovação de viagem** por um gestor.

## 2. Atores

| Ator | Papel no processo | Objetivo |
|---|---|---|
| ✅ **Gerente de Projetos (PM): persona principal** | Abre e acompanha as RRs dos seus projetos, e decide o que fazer quando algo trava | Ter as pessoas certas no início do projeto |
| **Gerente de Recursos (RM): complemento do PM** | Aloca recursos internos e recebe as escalações do PM | Usar bem a capacidade e cumprir prazos |
| **Parceiro** | Aceita ou rejeita RRs de parceiro e indica o profissional | Receber demandas compatíveis com sua capacidade |
| **Aprovador de viagem** (gestor regional) | Aprova o deslocamento, quando a RR exige | Controlar custo |
| **Automação de alocação** | Processa e faz o match; nas RRs de parceiro, faz o envio | — |
| **Recurso** (interno ou do parceiro) | Executa o trabalho | Saber com antecedência onde e quando atua |

O MVP é desenhado **para o PM**. O RM aparece só como destino de escalação.

## 3. Ciclo de vida da RR ✅

O ciclo depende do tipo da RR. Nos dois tipos, a **aprovação de viagem é condicional**: só acontece se a RR exigir deslocamento.

### RR de parceiro

```
Pronta para alocar ─► Processando ─► Enviada ao parceiro ─► Aceita ─► Alocada ─► [Aprovação de viagem]* ─► Confirmada ─► Iniciada
       │                  │                  │
       ▼                  ▼                  ▼
 Pendente (sem      Parada (pré-        Rejeitada (capacidade,
 tentativa)         requisito, N        competências) → realocar
                    tentativas)
```

### RR interna

```
Pronta para alocar ─► Processando ─► Aceita e alocada ─► [Aprovação de viagem]* ─► Confirmada ─► Iniciada
       │                  │
       ▼                  ▼
 Pendente (sem      Parada (pré-requisito,
 tentativa)         N tentativas)
```

\* Só quando a RR exige deslocamento do recurso.

**Hipótese a validar:** a RR interna nunca é rejeitada; se não houver match, ela fica parada.

### Situações em que o PM precisa agir

| Situação | Tipo de RR | Quem age | Sinal no mock |
|---|---|---|---|
| Rejeitada pelo parceiro | Parceiro | PM: realocar | "RR Rejected by Partner" |
| Parceiro não responde (SLA de 48h) | Parceiro | PM: cobrar | Coluna "Days in Status" |
| Pré-requisito ausente (taxa, tier) | Ambos | PM ou administrador | "Missing Cost Rate", "Automation Blocked" |
| Sem tentativa de automação | Ambos | PM: revisar configuração | "RR Stale — No Attempt" |
| Viagem não aprovada | Ambos, se exigir deslocamento | Aprovador, cobrado pelo PM | "Travel Not Approved" |
| Início próximo sem confirmação | Ambos | PM: escalar ao RM | "Start Date Approaching" |

## 4. O problema ✅

As cinco dores foram confirmadas pelo POD:

1. **Visibilidade fragmentada:** o PM não tem uma visão única do estado de todas as suas RRs.
2. **Problemas descobertos tarde:** rejeições, bloqueios de configuração e viagens pendentes só aparecem perto da data de início.
3. **Automação falha em silêncio:** RRs ficam paradas por falta de pré-requisito, sem ninguém avisado.
4. **Cobrança manual:** o PM persegue parceiros e aprovadores.
5. **Risco de começar o projeto sem recurso**, com impacto no cliente e em receita.

**Como é feito hoje:** com **relatórios e ações manuais**. O PM consulta os dados em telas separadas, junta as informações e **deduz** qual ação tomar.

### Evidências

A operação é grande e não há números precisos disponíveis, nem podemos usar números reais. ✅ **Decisão do POD:** entrevistar **1 ou 2 PMs** e usar as respostas como base das métricas.

| Evidência | Como obter | Serve para |
|---|---|---|
| ✅ **Entrevistas com 1 ou 2 PMs** | Conversas curtas e estruturadas, registradas de forma anonimizada em `docs/produto/discovery/` | Linha de base das métricas, validação das dores e discovery do checkpoint 02 |
| **Mapa do processo atual** | Na própria entrevista: o PM mostra quantas telas e relatórios e quantos passos percorre para decidir uma ação | Hipótese de valor (redução de passos e tempo) |
| **Dados sintéticos realistas** | Gerar um histórico de RRs que reproduza os padrões descritos nas entrevistas, sem copiar valores | Métricas do MVP e eval da IA |

**Cuidados com as entrevistas:**
- Com 1 ou 2 pessoas, os números são **estimativas declaradas** ("levo cerca de X minutos por dia"), não estatística. Registrar assim, sem apresentar como medição.
- Perguntar por **fatos recentes**, não opiniões: "conte a última vez que uma RR travou", e não "você acha que um painel ajudaria?".
- Anonimizar na hora de registrar: sem nomes, cargos específicos, clientes, parceiros ou números do negócio. Gravações e anotações brutas ficam **fora** do repositório.
- Os mesmos PMs podem testar o protótipo no checkpoint 03, que exige 2 ou mais usuários.

## 5. Funcionalidades propostas no mock

| # | Funcionalidade | Dor que ataca | O mock mostra |
|---|---|---|---|
| F1 | **Indicadores do topo:** abertas, enviadas hoje, paradas, aguardando confirmação, começam na semana | 1 | 5 cartões |
| F2 | **Lista "em alocação"** com filtros (parceiro/interno, paradas, prontas), busca e paginação | 1 | Tabela principal |
| F3 | **Lista "aguardando confirmação"** com SLA do parceiro e dias até o início, em faixas de cor | 2, 4 | Tabela laranja |
| F4 | **Lista "alocadas recentemente"** | 1 | Tabela verde |
| F5 | **Alertas acionáveis** (7 tipos) com ação direta: realocar, resolver taxa, cobrar, escalar | 2, 3, 4 | Painel lateral |
| F6 | ✅ **Próxima melhor ação (IA)** | 2, 4, 5 | Aba "Predicted Actions" |
| F7 | **Atividade recente** | 1 | Painel lateral |
| F8 | **Atualização automática** | 1 | "Refreshes every Ns" |

## 6. A IA do produto: próxima melhor ação ✅

O POD escolheu a **próxima melhor ação**: a IA olha a carteira de RRs do PM e diz **o que fazer agora, em que ordem e por quê**. É uma IA "no fluxo": age onde o PM já está.

### O que ainda precisa ser provado no grill

Tirando a IA, F1 a F5 continuam resolvendo boa parte da dor, porque os alertas são regras. Se a próxima melhor ação for só "ordenar os alertas por prioridade", **ela também é uma regra**, e a IA vira enfeite. Para não ser enfeite, ela precisa fazer algo que uma regra fixa não faz bem:

- **Combinar sinais:** cruzar tipo da RR, dias até o início, histórico de rejeição do parceiro, SLA, viagem e pré-requisitos numa prioridade única. Por exemplo: "esta RR tem 3 alertas menores, mas é a mais arriscada da sua carteira".
- **Justificar em linguagem natural** por que essa ação vem antes das outras.
- **Antecipar:** sugerir a ação **antes** de o alerta disparar (por exemplo, enviar também a outro parceiro, porque este costuma rejeitar esse perfil).

**Como medir (eval do checkpoint 05):** montar de 10 a 20 cenários sintéticos de carteira, cada um com a ação que um PM experiente tomaria. A métrica é quantas vezes a ação recomendada pela IA (ou o top 3) coincide com a do especialista. Incluir casos difíceis (sinais conflitantes) e adversariais (dados incompletos ou tentativas de fazer a IA executar algo indevido).

**Decisão em aberto:** a IA só **recomenda**, e o PM executa, ou ela também **executa** com aprovação do PM? Recomendação: só recomendar no MVP.

## 7. Restrições conhecidas

- **Plataforma Salesforce** (ADR-0001), alinhada com o professor.
- ✅ **App Lightning interno** ([ADR-0003](../adr/0003-app-lightning-interno.md)): o produto roda dentro do Salesforce, como um app Lightning para usuários internos (os PMs). Não há portal nem acesso público. A ideia de um portal no Experience Cloud foi descartada pelo POD.
  - **Conflito com o bootcamp:** a regra 2 pede o MVP em "URL pública". O app tem uma URL acessível pela internet (a da org), mas exige login no Salesforce. A leitura que proponho é que isso cumpre a regra **se** o professor tiver um usuário de demonstração na org, com dados sintéticos. **Precisa ser confirmado com o professor.**
  - **Licenças:** confirmar quantas licenças de usuário a org de desenvolvimento oferece. Elas precisam cobrir os dois membros do POD, o professor e um usuário com perfil de PM para a demo.
- **Pacote de PSA:** é um pacote gerenciado e licenciado, que **não estará disponível** numa org de desenvolvimento ou scratch org. ✅ **Direção definida pelo POD:** recriar os objetos necessários por engenharia reversa da **documentação pública** do fornecedor do PSA, no momento da Construction (checkpoint 04). Ao executar, valem estas regras, a registrar num ADR:
  - usar só a documentação pública, nunca metadados ou dados de uma org da empresa (AGENTS.md, seção 1);
  - usar nomes próprios, sem copiar o namespace nem os nomes de API do pacote, porque o repositório é público e o modelo é nosso;
  - recriar só o subconjunto que o MVP usa (RR, recurso, parceiro, atribuição, taxa), não o pacote inteiro;
  - se for útil manter o mapeamento "nosso objeto ↔ objeto do PSA" para uma futura adoção na empresa, ele fica **fora** deste repositório.
- **Confidencialidade:** nada de nomes, códigos, regras de negócio ou números reais. Termos e siglas internas foram substituídos por equivalentes genéricos.
- **Ritmo:** POD de 2 pessoas; o escopo do MVP precisa caber nisso.

## 8. Árvore de decisões

### Já decidido

| Decisão | Resposta |
|---|---|
| Persona principal | PM (o RM é complemento) |
| Tipos de RR | Parceiro e interna, exclusivos, com ciclos diferentes |
| Dores | As 5 da seção 4 |
| Como é hoje | Relatórios, telas separadas e dedução manual |
| Papel da IA | Próxima melhor ação |
| Modelo de dados | Recriado a partir da documentação pública do PSA (checkpoint 04) |
| Acesso | App Lightning interno ([ADR-0003](../adr/0003-app-lightning-interno.md)) |
| Evidências | Entrevistas com 1 ou 2 PMs como base das métricas |

### Frontier atual para o grill

**Rodada 1: valor e IA** (pré-requisitos já decididos)
1. Qual é a **uma** métrica principal? (recomendação: % de RRs que chegam à data de início confirmadas; alternativa: tempo médio de uma RR parada sem ação)
2. O que a próxima melhor ação faz que uma regra fixa não faz? Escolher entre combinar sinais, justificar e antecipar (seção 6).
3. A IA só recomenda ou também executa? (recomendação: só recomenda no MVP)
4. Qual é a hipótese de valor? ("Acreditamos que uma próxima melhor ação com IA para PMs vai gerar... Saberemos quando [métrica] mudar.")

**Rodada 2: escopo do MVP** (depende da rodada 1)
5. MoSCoW: quais de F1 a F8 são *Must*? (recomendação: F6 e o mínimo de F2 e F5 que a sustenta)
6. O MVP cobre os dois tipos de RR ou começa por um? (recomendação: os dois, porque a diferença entre eles é justamente o que a IA precisa entender)
7. O que fica explicitamente **fora**?

**Rodada 3: viabilidade técnica** (depende da rodada 2)
8. Como o professor acessa a demo, e o que a regra de "URL pública" aceita? (ver seção 7)
9. Quais objetos e campos são o mínimo para o MVP?
10. Onde roda a IA: serviço nativo da plataforma ou LLM externo via Apex? Custo, limites e LGPD.

## 9. Fora de escopo (candidatos)

- Gestão completa do projeto (marcos, horas, faturamento).
- Portal do parceiro.
- Fluxo de aprovação de viagem em si; o MVP só acompanha.
- Integração com sistemas reais da empresa.
- Portal no Experience Cloud e SSO (descartados no ADR-0003).
