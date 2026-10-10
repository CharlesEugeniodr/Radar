# Radar — Arquitetura de produto

O Radar tem dois ambientes principais:

1. **Ambiente do comprador:** publicar uma intenção de compra e receber propostas.
2. **Ambiente do vendedor:** encontrar demandas qualificadas e enviar propostas comerciais.

A lógica central **não** é "vendedores disputando agressivamente o cliente", e sim
**vários fornecedores respondendo a uma necessidade real, com regras de transparência,
privacidade e qualidade**. O objeto principal da plataforma é a **demanda**, não o produto.

## 1. Visão geral

```text
COMPRADOR  ── publica necessidade, orçamento, prazo e localização ──▶ MOTOR RADAR
MOTOR RADAR ── classifica · extrai atributos · aplica raio · filtra fornecedores
               · controla prazo e nº de propostas ──▶ VENDEDORES COMPATÍVEIS
VENDEDORES  ── propostas estruturadas (preço + prazo + condição + garantia) ──▶ COMPRADOR
COMPRADOR   ── compara e escolhe ──▶ CHAT / NEGOCIAÇÃO / FECHAMENTO
```

### Entidades centrais

| Entidade | Descrição |
|---|---|
| Intenção de compra | Necessidade estruturada publicada pelo comprador |
| Fornecedor compatível | Vendedor selecionado pelo motor para uma intenção |
| Proposta | Oferta estruturada de um fornecedor |
| Negociação / fechamento | Chat, escolha, resultado e avaliações |

### Ciclo de vida da intenção

`Rascunho → Publicada → Recebendo propostas → Propostas encerradas → Em negociação →
Fornecedor escolhido → Concluída`; saídas alternativas: `Cancelada`, `Expirada`.

## 2. Ambiente do comprador

- **Início:** uma única pergunta ("O que você está procurando?") em texto livre, mais a lista
  "Minhas demandas" com nº de propostas. Sem vitrines nem banners.
- **Estruturação por IA:** o texto livre é convertido em categoria, produto, quantidade,
  orçamento máximo, prazo, local, estado (novo/usado/indiferente), preferência de entrega,
  observações e imagem opcional. Perguntas complementares só quando necessário.
- **Revisão antes de publicar:** mostra produto, orçamento, prazo, raio e a garantia de que
  dados pessoais não serão exibidos. Deve informar: *"Você não está comprando ainda. Está
  informando ao mercado o que deseja comprar."*
- **Minha intenção:** status, tempo restante, nº de propostas, aviso de privacidade.
- **Propostas:** comparação com ordenação (menor preço, mais rápido, melhor avaliado). Cada
  proposta exibe preço, solução, marca/modelo/material, prazo, frete, condição, distância
  aproximada, nota, nº de vendas, garantia, fotos, forma de pagamento e validade.
- **Recomendação explicável:** "Melhor equilíbrio" sempre acompanhada dos motivos
  (dentro do orçamento, entrega mais rápida, avaliação > 4,5, fornecedor próximo).
- **Navegação:** Início · Publicar intenção · Minhas intenções · Propostas recebidas ·
  Conversas · Compras concluídas · Perfil e privacidade.

## 3. Ambiente do vendedor

O vendedor vê **oportunidades qualificadas**, não uma lista bruta de pedidos.

- **Painel:** resumo do dia (novas demandas, compatíveis, propostas enviadas), filtros
  (categoria, distância, orçamento, prazo) e cards ordenados por compatibilidade.
- **Card da oportunidade:** título, categoria, orçamento máximo, prazo, distância
  aproximada, descrição da necessidade, custo em créditos, ações *Não tenho* / *Enviar proposta*.
  Indicador de qualidade da demanda ("bem especificada" / "faltam informações").
- **Envio de proposta (formulário estruturado):** produto/solução, preço, frete (valor,
  incluso ou a combinar), prazo, condição (novo/usado/sob medida), garantia, mensagem, anexos.
  Prévia: preço final estimado, prazo, validade (ex.: 48 h) e custo em créditos.
  Campos obrigatórios impedem propostas vazias ("Tenho aqui", "Chama no WhatsApp"), sem frete
  ou sem prazo.
- **Navegação:** Painel · Novas demandas · Minhas propostas · Conversas · Negócios ganhos ·
  Créditos · Categorias e área de atendimento · Avaliações · Perfil da empresa.

### Competição por valor

Vendedores competem em preço, prazo, qualidade, garantia, distância, avaliação,
personalização, disponibilidade e condição de pagamento. Propostas de concorrentes **não** são
reveladas; o vendedor recebe apenas feedback agregado (ex.: "Você está entre as três melhores
propostas" ou "Sua proposta está acima da média recebida"), evitando cópia de preço e
comportamento predatório.

## 4. Motor Radar

1. **Entender a demanda** — NLP transforma texto livre em saída estruturada
   (categoria, tipo, atributos, orçamento, quantidade, prazo).
2. **Encontrar fornecedores compatíveis** — categorias, produtos/serviços, distância, área
   de entrega, estoque declarado, horário, reputação e capacidade de cumprir o prazo.
3. **Priorizar** — score de compatibilidade **explicável** (ex.: 94%: trabalha com o produto,
   a 5 km, atende a região, boas avaliações, prazo a confirmar).
4. **Controlar notificações** — limites de fornecedores notificados, raio, categorias,
   capacidade de atendimento, frequência de alertas e máximo de propostas por demanda.
5. **Encerrar e registrar** — proposta escolhida, valor final, prazo, motivo (opcional),
   resultado (vendido, não vendido, cancelado, expirado) e avaliações mútuas. Esses dados
   realimentam o motor.

## 5. Privacidade em camadas

| Momento | Vendedor vê | Vendedor **não** vê |
|---|---|---|
| Antes da proposta | Categoria, descrição, orçamento, prazo, região/distância aproximada | Nome, telefone, e-mail, endereço, identidade |
| Após interesse | Área mais específica | Contato direto |
| Após aceite | Chat interno, dados de entrega/pagamento/fiscais, endereço exato (com consentimento) | — |

O primeiro contato ocorre dentro da plataforma, reduzindo golpes, assédio comercial e fuga
do sistema.

## 6. Modelo de domínio (sugerido)

```text
Usuario(id, tipo: comprador|vendedor)
Comprador(usuario_id, preferencias_privacidade)
Vendedor(usuario_id, categorias[], area_atendimento, horario, reputacao, saldo_creditos)
Intencao(id, comprador_id, texto_original, categoria, atributos{}, quantidade,
         orcamento_max, prazo, localizacao_aproximada, raio_km, estado_produto,
         status, expira_em, max_propostas)
Notificacao(intencao_id, vendedor_id, score_compatibilidade, motivos[])
Proposta(id, intencao_id, vendedor_id, produto, preco, frete, prazo_entrega,
         condicao, garantia, mensagem, anexos[], validade, custo_creditos, status)
Conversa(proposta_id, mensagens[])
Fechamento(intencao_id, proposta_id, valor_final, resultado, motivo)
Avaliacao(fechamento_id, autor, nota, comentario)
Credito(vendedor_id, movimentos[])
```

### Componentes

```text
Apps (web/mobile) ─▶ API Gateway ─▶ Serviços:
  Intenções · Propostas · Chat · Créditos · Avaliações · Perfis/Privacidade
Motor Radar: Interpretador (IA) · Matching geográfico/categoria · Scoring · Throttling de notificações
Infra: Banco relacional + busca geoespacial · Fila de eventos/notificações · Armazenamento de mídia
```

## 7. MVP

**Comprador:** cadastro, publicação (orçamento, prazo, localização aproximada), recebimento e
comparação de propostas, chat interno, escolha do fornecedor, avaliação.

**Vendedor:** cadastro comercial, categorias e região, painel de demandas compatíveis, envio
de proposta, controle de créditos, chat, histórico, avaliação.

**Segunda fase:** IA avançada, leilão reverso em tempo real, integração com estoque/ERP,
recomendação automática, pagamento protegido, nota fiscal, assinatura, API para lojas,
demandas recorrentes.

## 8. Hipóteses e lacunas

- **[HIPÓTESE]** Compradores evitam formulários longos → começar com texto livre.
- **[HIPÓTESE]** Vendedores ignoram demandas mal qualificadas → exibir indicador de qualidade.
- **[LACUNA]** Modelo de créditos a validar (propostas por demanda, conversão, ticket médio,
  custo de aquisição, propostas inúteis, sensibilidade a preço por proposta).
- **[LACUNA]** Intermediação de pagamento: *geração de leads* (mais simples, menos controle,
  recomendado no MVP) vs. *marketplace completo* (pagamento, garantia, cancelamento, disputa,
  entrega, nota fiscal).

## 9. LGPD by design

### Princípios obrigatórios

- **Finalidade e necessidade:** coletar apenas o necessário para publicar, casar e fechar uma demanda.
- **Minimização:** identidade e contato direto do comprador só após aceite e consentimento.
- **Transparência:** explicar claramente o uso dos dados em cada etapa do fluxo.
- **Segurança e prevenção:** criptografia, trilhas de auditoria e controle de acesso por perfil.

### Base legal e ciclo de dados

| Etapa | Dados principais | Base legal | Retenção sugerida |
|---|---|---|---|
| Cadastro e autenticação | nome, e-mail, telefone, documentos de conta | execução de contrato | enquanto conta ativa + prazo legal |
| Publicação da intenção | necessidade, orçamento, prazo, localização aproximada | execução de contrato | histórico operacional |
| Match e propostas | categoria, região aproximada, score, proposta comercial | legítimo interesse + execução de contrato | histórico operacional |
| Fechamento | dados de entrega/pagamento/fiscal (quando aplicável) | execução de contrato + obrigação legal | conforme obrigação fiscal/contábil |
| Marketing opcional | preferências de comunicação | consentimento | até revogação |

### Direitos do titular (fluxo produto)

- acesso e portabilidade de dados;
- correção cadastral;
- revogação de consentimento;
- anonimização/exclusão quando possível juridicamente;
- registro de requisição com protocolo e prazo de atendimento.

### Controles operacionais mínimos

- consentimento versionado (`quem`, `quando`, `qual termo`);
- trilha de auditoria de acesso a PII;
- política de descarte/anonimização por tipo de dado;
- canal de privacidade para requisições LGPD.

## 10. Lógica de busca por área, região e proximidade

### Entradas do matching geográfico

- `intencao.localizacao_aproximada` (geoponto aproximado);
- `intencao.raio_km` (alcance desejado);
- `vendedor.area_atendimento` (cidades/bairros/UF ou polígonos);
- `vendedor.raio_max_entrega` e disponibilidade declarada.

### Etapas de busca

1. **Filtro por área macro:** UF/cidade/região atendida pelo vendedor.
2. **Filtro por região local:** bairro/zona/polígono de entrega compatível.
3. **Proximidade:** cálculo de distância entre demanda e origem operacional do vendedor.
4. **Elegibilidade final:** distância dentro do raio efetivo e capacidade de atendimento.

### Score geográfico explicável

```text
score_geo = 0,5*score_proximidade + 0,3*score_regiao + 0,2*score_capacidade
score_proximidade = max(0, 1 - distancia_km / raio_efetivo_km)
```

### Regras de expansão controlada

- iniciar com raio da intenção;
- expandir em faixas progressivas (ex.: +5 km, +15 km, +30 km) quando oferta insuficiente;
- respeitar limite máximo para evitar propostas irrelevantes;
- manter explicação do motivo de notificação para o vendedor.

## 11. Métricas de estimativa de precificação (média de valores)

### Base de cálculo

- propostas históricas e fechamentos da mesma categoria/subcategoria;
- segmentação por região, faixa de quantidade, prazo e condição do item;
- exclusão de registros incompletos e outliers extremos.

### Métricas principais

1. **Média simples local** (`media_local`).
2. **Média ponderada** por recência, similaridade e reputação do fornecedor.
3. **Mediana e faixa interquartil** para robustez contra distorções.
4. **Desvio padrão** para medir volatilidade.
5. **Índice de confiança** com base em volume e estabilidade amostral.

```text
media_ponderada = Σ(preco_i * peso_i) / Σ(peso_i)
peso_i = peso_recencia * peso_similaridade * peso_qualidade
```

### Saída para produto

- **Comprador:** faixa sugerida (`P25-P75`), média estimada e nível de confiança.
- **Vendedor:** feedback relativo (abaixo/na/acima da média da demanda comparável).
- **Motor:** uso do benchmark para priorização e alertas de proposta fora do padrão.

## 12. Lógica C2B (Consumer-to-Business)

No Radar, o fluxo central é C2B: o consumidor inicia a demanda e o mercado responde com oferta qualificada.

### Fluxo operacional

1. **Consumidor declara necessidade** (texto livre + orçamento/prazo/localização aproximada).
2. **Motor estrutura a intenção** (categoria, atributos, urgência e critérios de match).
3. **Plataforma seleciona vendedores compatíveis** (área, região, proximidade e capacidade).
4. **Vendedores enviam propostas estruturadas** (preço, prazo, frete, garantia e condição).
5. **Consumidor compara e negocia** com privacidade em camadas.
6. **Escolha e fechamento** com registro de resultado e motivo.
7. **Avaliações mútuas e realimentação** para melhorar matching e precificação.

### Regras de qualidade C2B

- limite de propostas por intenção para manter qualidade de decisão;
- bloqueio de proposta incompleta (sem preço, frete ou prazo);
- privacidade progressiva para reduzir assédio comercial e fraude;
- feedback agregado para competição por valor, sem expor preço individual de concorrentes.

## Núcleo operacional

> O comprador publica uma necessidade estruturada; o Radar encontra fornecedores compatíveis;
> os vendedores competem por valor; e o consumidor escolhe a proposta que melhor combina
> preço, prazo, qualidade e confiança.
