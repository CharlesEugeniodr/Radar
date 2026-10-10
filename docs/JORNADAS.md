# Comparação de jornadas: E-commerce tradicional × Radar

| | **Radar — lógica orientada à demanda** | **E-commerce tradicional — lógica orientada à oferta** |
|---|---|---|
| Início | Consumidor identifica uma necessidade | Consumidor decide comprar |
| 1 | Descreve o que precisa (texto livre assistido por IA) | Entra na loja ou marketplace |
| 2 | Define limites: orçamento, prazo, quantidade e localização | Pesquisa produtos, categorias e marcas |
| 3 | Publica a intenção de compra, com dados pessoais protegidos | Compara itens disponíveis (preço, avaliações, frete) |
| 4 | Motor Radar interpreta e classifica (categoria, atributos, urgência) | Escolhe um produto do catálogo |
| 5 | Filtra fornecedores compatíveis (competência, raio, disponibilidade, reputação) | Adiciona ao carrinho |
| 6 | Fornecedores recebem a oportunidade sem acesso inicial à identidade do comprador | Informa endereço e pagamento |
| 7 | Vendedores enviam propostas estruturadas (preço, prazo, condição, frete, garantia) | Finaliza o pedido |
| 8 | Consumidor compara propostas (menor preço, rapidez, qualidade e confiança) | Aguarda separação, envio e entrega |
| 9 | Escolhe um fornecedor e inicia negociação (chat, dados liberados por etapas) | — |
| Fim | Compra ou contratação concluída | Compra concluída |

**Diferença central:** no e-commerce o consumidor procura o que já está ofertado; no Radar o
mercado procura quem declarou uma necessidade. A oferta nasce da demanda, e o contato e a
negociação são controlados pela plataforma.

```mermaid
flowchart TD
  A[Consumidor identifica uma necessidade] --> B[1. Descreve o que precisa]
  B --> C[2. Define orçamento, prazo, quantidade e localização]
  C --> D[3. Publica a intenção, dados protegidos]
  D --> E[4. Motor Radar interpreta e classifica]
  E --> F[5. Filtra fornecedores compatíveis]
  F --> G[6. Fornecedores recebem a oportunidade sem identidade]
  G --> H[7. Propostas estruturadas]
  H --> I[8. Consumidor compara propostas]
  I --> J[9. Escolhe e negocia por etapas]
  J --> K([Compra ou contratação concluída])
