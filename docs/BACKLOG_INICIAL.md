# Backlog inicial por domínio

Este backlog quebra as épicas da arquitetura em entregas pequenas por repositório.

## `Radar` (produto + governança)

- [ ] Formalizar e revisar documentação de arquitetura e jornadas
- [ ] Publicar padrão oficial de branch, merge e release
- [ ] Configurar templates de PR/issue e CODEOWNERS
- [ ] Definir critérios de pronto (DoD) para MVP
- [ ] Estruturar board macro com trilhas: comprador, vendedor, motor, plataforma

## `radar-api`

- [ ] Inicializar projeto base da API
- [ ] Implementar autenticação e autorização por perfil (comprador/vendedor)
- [ ] Implementar CRUD de intenção de compra com ciclo de vida
- [ ] Implementar publicação e gestão de propostas
- [ ] Implementar endpoints de chat e negociação
- [ ] Implementar fechamento e avaliações mútuas
- [ ] Expor eventos de domínio para notificações e analytics

## `radar-web-comprador`

- [ ] Tela inicial com publicação de intenção em texto livre
- [ ] Fluxo de revisão e confirmação da intenção
- [ ] Lista de intenções com status e contagem de propostas
- [ ] Comparador de propostas com ordenação
- [ ] Visualização de recomendação explicável
- [ ] Início de conversa e negociação após escolha

## `radar-web-vendedor`

- [ ] Painel de oportunidades qualificadas
- [ ] Filtros por categoria, distância, orçamento e prazo
- [ ] Formulário estruturado de proposta com validações obrigatórias
- [ ] Gestão de propostas enviadas e status
- [ ] Feedback agregado de competitividade da proposta
- [ ] Fluxo de conversa e fechamento

## `radar-mobile`

- [ ] Definir escopo MVP mobile (comprador, vendedor ou ambos)
- [ ] Implementar autenticação e sessão
- [ ] Implementar notificações de novas oportunidades/propostas
- [ ] Implementar visão resumida de demandas e propostas
- [ ] Implementar fluxo de mensagens e atualizações críticas

## `radar-infra`

- [ ] Definir padrão de ambientes (dev, staging, prod)
- [ ] Provisionar banco relacional e componente geoespacial
- [ ] Provisionar fila de eventos e notificações
- [ ] Provisionar storage de mídia com política de acesso
- [ ] Definir pipeline de deploy por ambiente
- [ ] Definir baseline de observabilidade (logs, métricas, alertas)

## Ordem recomendada de execução

1. `radar-infra` (fundação de ambientes e deploy)
2. `radar-api` (domínio e contratos)
3. `radar-web-comprador` (entrada de demanda)
4. `radar-web-vendedor` (resposta de oferta)
5. `radar-mobile` (canais complementares)
