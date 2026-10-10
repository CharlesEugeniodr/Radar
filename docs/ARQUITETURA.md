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

## Núcleo operacional

> O comprador publica uma necessidade estruturada; o Radar encontra fornecedores compatíveis;
> os vendedores competem por valor; e o consumidor escolhe a proposta que melhor combina
> preço, prazo, qualidade e confiança.
