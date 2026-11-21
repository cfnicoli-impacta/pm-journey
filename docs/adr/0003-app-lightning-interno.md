# ADR-0003: App Lightning interno como forma de acesso

- **Status:** Aceito
- **Data:** 2026-11-20

## Contexto

A persona principal é o Gerente de Projetos (PM), que já trabalha como usuário interno do Salesforce. O acesso ao produto precisa ser restrito a um grupo específico de usuários.

O POD avaliou duas opções:

| Opção | Prós | Contras |
|---|---|---|
| **Portal no Experience Cloud** com login restrito (e SSO) | URL própria; acesso separado do resto da org | Os PMs são usuários internos, então um portal duplica o acesso que eles já têm. Exige licenças específicas e configuração de site, e o SSO não pode usar o provedor de identidade da empresa no projeto acadêmico |
| **App Lightning interno** | Fica onde o PM já trabalha (IA "no fluxo"); usa o modelo de segurança padrão (perfis, permission sets, sharing); menos configuração | Exige login no Salesforce; a demo precisa de um usuário na org |

## Decisão

Construir o produto como um **app Lightning interno**, com LWC, para usuários internos da org. O acesso é controlado por um permission set próprio do app.

## Consequências

- **Regra "URL pública" do bootcamp:** a URL da org é acessível pela internet, mas exige login. A proposta é dar ao professor um usuário de demonstração com dados sintéticos. **É preciso confirmar com o professor** se isso cumpre a regra 2.
- **Licenças:** confirmar se a org de desenvolvimento tem licenças de usuário suficientes para o POD, o professor e um usuário de demo com perfil de PM.
- **Segurança:** permission set do app, `with sharing` e `WITH USER_MODE` (constituição, princípio 4). Cada PM vê só as RRs dos seus projetos.
- **Fora de escopo:** o portal no Experience Cloud e o SSO.
- Substitui o item "URL pública" das consequências do [ADR-0001](0001-salesforce-como-plataforma.md).
