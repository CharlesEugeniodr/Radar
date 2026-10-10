# Estruturação de repositórios, ramificação e governança

Este documento define o padrão oficial para organização técnica do Radar.

## 1) Estratégia oficial de repositórios

**Decisão:** adotar **multi-repo** com governança central neste repositório (`Radar`).

Motivação principal:
- separar ciclos de entrega por domínio;
- reduzir acoplamento entre times e pipelines;
- permitir evolução tecnológica por frente (API, web, mobile, infra).

## 2) Mapa de divisão por repositório

| Repositório | Responsabilidade |
|---|---|
| `Radar` | visão de produto, arquitetura, governança e backlog macro |
| `radar-api` | APIs de autenticação, intenções, propostas, chat, avaliações, créditos |
| `radar-web-comprador` | experiência do comprador (publicação e comparação de propostas) |
| `radar-web-vendedor` | experiência do vendedor (oportunidades e envio de proposta) |
| `radar-mobile` | app mobile (prioridade em fluxos críticos de comprador e vendedor) |
| `radar-infra` | infraestrutura, ambientes, observabilidade, segurança operacional e deploy |

> Opcional de fase 2: criar `radar-shared` para contratos, SDKs e componentes compartilhados.

## 3) Modelo de branch

**Modelo escolhido:** **trunk-based**.

- branch base única: `main`;
- sem branch `develop` permanente;
- branches curtas por tarefa;
- branch temporária `release/x.y` apenas quando necessário para estabilização de release.

## 4) Padrões de ramificação e merge

### Nomenclatura de branches

- `feat/<slug>`
- `fix/<slug>`
- `hotfix/<slug>`
- `chore/<slug>`
- `docs/<slug>`
- `refactor/<slug>`
- `test/<slug>`

### Regras de merge

- PR obrigatório para `main`;
- mínimo de 1 aprovação;
- `squash merge` como padrão;
- push direto em `main` bloqueado;
- branch deve estar atualizada com `main` no momento do merge;
- branch removida após merge.

## 5) Governança obrigatória

- `CODEOWNERS` ativo em todos os repositórios;
- template de Pull Request obrigatório;
- templates de issue para bug e feature;
- proteção de branch em `main` com:
  - aprovação obrigatória;
  - checks obrigatórios;
  - bloqueio de force push;
  - bloqueio de deleção de branch protegida;
  - exigência de resolução de conversas de review.

## 6) CI mínimo por repositório

Todos os repositórios operacionais devem ter checks obrigatórios com os nomes abaixo:

- `ci/lint`
- `ci/test`
- `ci/build`
- `security/codeql`
- `security/secret-scan`

### Aplicação por domínio

| Repositório | Lint | Test | Build |
|---|---|---|---|
| `radar-api` | análise estática e estilo | testes unitários/integrados | build/pacote da API |
| `radar-web-comprador` | lint de frontend | testes de unidade/integração | build da aplicação web |
| `radar-web-vendedor` | lint de frontend | testes de unidade/integração | build da aplicação web |
| `radar-mobile` | lint mobile | testes unitários | build de artefato mobile |
| `radar-infra` | validação de IaC | validação de plano/contrato | empacotamento/artefatos de infra |

## 7) Plano de releases e hotfix

### Versionamento

- padrão **SemVer**: `MAJOR.MINOR.PATCH`;
- tags no formato: `vMAJOR.MINOR.PATCH`.

### Fluxo de release

1. Consolidar mudanças em `main`;
2. Opcional: abrir `release/x.y` para estabilização;
3. Executar checks obrigatórios;
4. Criar tag `vX.Y.Z` em commit aprovado;
5. Publicar notas de release e impactos.

### Fluxo de hotfix

1. Criar `hotfix/<slug>` a partir da tag/commit de produção;
2. Corrigir, validar e abrir PR;
3. Fazer merge em `main`;
4. Gerar nova tag de patch (`vX.Y.(Z+1)`);
5. Atualizar notas da release de correção.
