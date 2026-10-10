# Governança de IA, Compliance e Privacidade (Radar)

## 1) Sumário executivo

- Esta proposta cria uma **governança de IA orientada a valor e risco**, com trilha de auditoria e evidências por métrica.
- **Conformidade ≠ valor**: conformidade garante obrigação legal/regulatória (LGPD, segurança, auditoria); valor mede resultado de negócio (ROI, produtividade, receita, qualidade).
- Base transversal: **NIST AI RMF (Govern, Map, Measure, Manage)** + **LGPD** + **ISO/IEC 42001** + **ISO/IEC 27001**.
- Contexto não informado foi marcado como **[PREMISSA]**.
- No estado atual, pelo repositório, há evidência de motor com IA para interpretação, matching, scoring e recomendação; categorias como chatbot/copiloto/agente/RAG/IA embarcada ainda exigem validação formal de inventário.

---

## 2) Inventário em tabela

| Categoria | ID | Nome | Finalidade | Área dona | Resp. técnico | Resp. negócio | Modelo de negócio impactado | Dados acessados | Sistemas consultados | Autonomia | Criticidade | Custo mensal estimado | Riscos principais | Resultados esperados | Status | Evidência de inventário |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Modelos | AI-MOD-001 | Interpretador de demanda (NLP) | Converter texto livre em atributos estruturados | Produto/Dados [PREMISSA] | [PREMISSA] | [PREMISSA] | B2C, C2B [PREMISSA] | Texto livre, orçamento, prazo, localização aproximada | Serviço de Intenções/API Gateway [PREMISSA] | Média (sugere estrutura, humano publica) | Alta | [PREMISSA] | Erro de classificação, viés, uso indevido de dados pessoais | Aumentar completude e qualidade das intenções | Piloto/Produção [PREMISSA] | `/home/runner/work/Radar/Radar/docs/ARQUITETURA.md:40-42,82-83,128`; `/home/runner/work/Radar/Radar/docs/JORNADAS.md:6` |
| Automações | AI-AUT-001 | Matching geográfico/categoria | Encontrar fornecedores compatíveis | Produto/Operações [PREMISSA] | [PREMISSA] | [PREMISSA] | B2B, C2B | Categoria, distância, área de entrega, reputação, capacidade | Perfis de vendedores, intenções | Média/Alta | Alta | [PREMISSA] | Discriminação geográfica indevida, exclusão de ofertas relevantes | Melhor taxa de match útil | Produção [PREMISSA] | `/home/runner/work/Radar/Radar/docs/ARQUITETURA.md:84-85,128` |
| Automações | AI-AUT-002 | Scoring de compatibilidade explicável | Priorizar fornecedores com justificativa | Produto/Operações [PREMISSA] | [PREMISSA] | [PREMISSA] | B2B, B2C, C2B | Dados de perfil, avaliação, distância, prazo | Motor Radar | Alta (prioriza fila) | Alta | [PREMISSA] | Viés no ranking, opacidade, contestação de fairness | Melhor conversão com explicabilidade | Produção [PREMISSA] | `/home/runner/work/Radar/Radar/docs/ARQUITETURA.md:86-87,114` |
| Automações | AI-AUT-003 | Throttling de notificações | Limitar volume/frequência para evitar abuso e ruído | Operações [PREMISSA] | [PREMISSA] | [PREMISSA] | B2B, C2B | Categoria, capacidade, frequência, limite de propostas | Motor/Notificações | Alta | Média/Alta | [PREMISSA] | Spam, perda de oportunidade, unfair exposure | Eficiência operacional e UX | Produção [PREMISSA] | `/home/runner/work/Radar/Radar/docs/ARQUITETURA.md:88-89,128` |
| Automações/Modelos | AI-AUT-004 | Recomendação “melhor equilíbrio” | Sugerir melhor proposta com motivo explícito | Produto [PREMISSA] | [PREMISSA] | [PREMISSA] | B2C, C2B | Preço, prazo, avaliação, proximidade | Propostas e avaliações | Média | Alta | [PREMISSA] | Recomendação tendenciosa, responsabilização por dano | Reduzir tempo de decisão e aumentar satisfação | Piloto/Produção [PREMISSA] | `/home/runner/work/Radar/Radar/docs/ARQUITETURA.md:50-51` |
| APIs de IA | AI-API-001 | API interna do Motor Radar | Expor serviços de inferência/decisão [PREMISSA] | Engenharia [PREMISSA] | [PREMISSA] | [PREMISSA] | B2B, B2C, C2B, C2C [PREMISSA] | Dados de intenções/propostas [PREMISSA] | API Gateway/serviços internos | Alta | Alta | [PREMISSA] | Abuso de API, privilégio excessivo, vazamento | Escalabilidade controlada | Ideação/Piloto [PREMISSA] | `/home/runner/work/Radar/Radar/docs/ARQUITETURA.md:126-129` |
| Chatbots | AI-CH-000 | Não identificado | Inventário pendente | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | Ausência de visibilidade de risco | Confirmar existência/não existência | Não identificado | Ausência de evidência em docs atuais; validar CMDB/catálogo [PREMISSA] |
| Copilotos | AI-CP-000 | Não identificado | Inventário pendente | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | Shadow AI interno | Confirmar uso corporativo | Não identificado | Ausência de evidência em docs atuais; validar endpoint/SSO [PREMISSA] |
| Agentes | AI-AG-000 | Não identificado | Inventário pendente | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | Execução autônoma sem controle | Confirmar escopo de autonomia | Não identificado | Ausência de evidência em docs atuais; validar backlog de produto [PREMISSA] |
| RAGs | AI-RAG-000 | Não identificado | Inventário pendente | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | Hallucination por base fraca | Confirmar arquitetura de conhecimento | Não identificado | Ausência de evidência em docs atuais; validar pipelines [PREMISSA] |
| IA embarcada | AI-EMB-000 | Não identificado | Inventário pendente | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | [PREMISSA] | Segurança de endpoint | Confirmar inexistência formal | Não identificado | Ausência de evidência em docs atuais; validar roadmap [PREMISSA] |

---

## 3) Classificação por B2B, B2C, C2B, C2C

| Modelo | Aplicação no contexto Radar [PREMISSA] | Riscos prioritários | Métricas de conformidade | Métricas de valor |
|---|---|---|---|---|
| B2B | Relação com fornecedores/empresas e contratos de serviço | SLA, DPA, subprocessadores, auditoria contratual, vazamento entre contas | % contratos com cláusula IA/LGPD; % subprocessadores aprovados; SLA de incidentes | Receita por parceiro, taxa de conversão de oportunidades, custo por proposta qualificada |
| B2C | Interação com comprador pessoa física | Transparência, consentimento, direitos do titular, reputação | % consentimentos válidos; prazo de atendimento ao titular; % comunicações transparentes | CSAT/NPS, tempo para fechar decisão, retenção de usuários |
| C2B | Pessoa fornece demanda/dados para empresas responderem | Base legal, revogação, uso secundário de dados, propriedade de conteúdo | % finalidades explícitas; % revogações atendidas; RIPD para fluxos sensíveis | Taxa de match útil, redução de retrabalho, aumento de propostas relevantes |
| C2C | Troca entre usuários na plataforma [PREMISSA] | Moderação, fraude, disputa, uso indevido de dados entre usuários | % casos moderados no SLA; % disputas com trilha completa | Tempo de resolução de disputa, índice de confiança da plataforma |

---

## 4) Métricas por pilar (tabela padrão)

| Pilar | Métrica | Definição | Fórmula | Fonte de dados | Frequência | Dono | Meta/Threshold | Evidência/Citação | Modelo de negócio | Risco/LGPD | Ação se fora da meta |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Inventário | % sistemas de IA inventariados (compliance) | Mede cobertura real do inventário corporativo de IA. | (Sistemas IA com cadastro completo / Sistemas IA detectados) x 100 | CMDB, catálogo IA, discovery de APIs | Semanal | PMO de IA [PREMISSA] | >= 98% | NIST AI RMF Govern/Map; política interna de inventário [PREMISSA] | B2B/B2C/C2B/C2C | Falta de accountability e risco não mapeado | Bloquear novos deploys até regularizar cadastro |
| Inventário | Custo mensal por sistema (valor) | Mede eficiência financeira por ativo de IA. | (Infra+licenças+operações+terceiros) / nº de sistemas ativos | FinOps, ERP, contratos | Mensal | FinOps + Dono de negócio [PREMISSA] | Dentro orçamento e tendência de queda trimestral | NIST Govern; controles financeiros internos [PREMISSA] | B2B/B2C/C2B/C2C | Estouro orçamentário sem valor | Revisar arquitetura, renegociar contratos ou descontinuar |
| Dados | % ativos de dados com base legal/finalidade (compliance) | Mede aderência de uso de dados à LGPD. | (Ativos usados por IA com base legal+finalidade documentadas / Ativos usados por IA) x 100 | Catálogo de dados, RIPD, RoPA | Quinzenal | DPO + Data Governance | 100% | LGPD arts. 6º, 7º, 9º, 37; NIST Map | B2B/B2C/C2B/C2C | Tratamento sem base legal | Suspender uso do dado até regularização |
| Dados | % intenções com atributos completos pós-IA (valor) | Mede qualidade prática da estruturação por IA. | (Intenções com campos obrigatórios completos / Intenções processadas) x 100 | Logs do interpretador, banco de intenções | Diário | Produto + MLOps [PREMISSA] | >= 95% | `/home/runner/work/Radar/Radar/docs/ARQUITETURA.md:40-42`; NIST Measure | B2C/C2B | Decisão ruim por dado incompleto | Ajustar prompts/modelo e reforçar revisão humana |
| Segurança | % sistemas com kill switch testado (compliance) | Mede prontidão de interrupção segura de IA. | (Sistemas críticos com teste de kill switch <=90 dias / Sistemas críticos) x 100 | Runbooks, logs de teste, GRC | Mensal | Segurança + SRE [PREMISSA] | 100% | LGPD art. 46; ISO 27001; NIST Manage | B2B/B2C/C2B/C2C | Incidente sem contenção | Escalonar ao Comitê de IA e congelar mudanças |
| Segurança | Taxa de incidente de IA por 10k execuções (valor/risco) | Mede estabilidade operacional com impacto de risco. | (Incidentes confirmados / Execuções IA) x 10.000 | SIEM, SOC, incidentes | Semanal | Segurança | <= 0,5 | ISO 27001; NIST Manage | B2B/B2C/C2B/C2C | Vazamento/fraude/interrupção | Análise de causa, patch e revisão de permissões |
| Avaliação e ROI | ROI líquido por caso de uso (valor) | Mede retorno econômico real de cada sistema de IA. | ((Benefício financeiro - Custo total) / Custo total) x 100 | FinOps, BI, dados operacionais | Mensal | Dono de negócio + Finanças | >= 20% [PREMISSA] | NIST Measure; IBM CEO Study [PREMISSA] | B2B/B2C/C2B/C2C | Investimento sem retorno | Pivotar escopo ou encerrar caso de uso |
| Avaliação e ROI | Impacto no EBIT atribuído à IA (valor) | Mede contribuição macro da carteira de IA no resultado operacional. | (EBIT com IA - EBIT baseline sem IA) / EBIT baseline x 100 | Controladoria, BI executivo | Trimestral | CFO + Comitê IA | Meta definida por unidade [PREMISSA] | McKinsey State of AI [PREMISSA]; NIST Measure | B2B/B2C/C2B/C2C | Superestimar benefício | Recalibrar baseline e priorização de portfólio |
| Supervisão humana | % decisões de alto impacto revisadas por humano (compliance) | Mede presença real de HITL em operação, não só em desenho. | (Decisões críticas com revisão humana / Decisões críticas totais) x 100 | Logs de workflow, trilha de aprovação | Diário | Operações + Dono de processo | 100% para alto impacto | NIST Govern/Manage; política HITL [PREMISSA] | B2B/B2C/C2B/C2C | Dano sem revisão humana | Forçar fallback manual imediato |
| Supervisão humana | Tempo mediano de aprovação humana (valor) | Mede eficiência operacional do HITL sem perder controle. | Mediana(tempo entre alerta e decisão humana) | Sistema de filas/workflow | Semanal | Operações | <= 15 min [PREMISSA] | NIST Manage; SLA operacional [PREMISSA] | B2B/B2C/C2B/C2C | Gargalo operacional | Ajustar capacidade/equipe e regras de escalonamento |
| Compliance, auditoria e LGPD | % direitos do titular atendidos no prazo (compliance) | Mede aderência a obrigações de atendimento ao titular. | (Solicitações atendidas no SLA / Total solicitações) x 100 | Plataforma de privacidade, CRM, jurídico | Mensal | DPO | >= 99% | LGPD art. 18; NIST Govern | B2C/C2B/C2C | Sanção regulatória e reputação | Plano de contingência e reforço de atendimento |
| Compliance, auditoria e LGPD | Custo evitado de não conformidade (valor) | Mede benefício financeiro de controles de compliance efetivos. | Multas/perdas potenciais estimadas - perdas reais ocorridas | Jurídico, risco, auditoria | Trimestral | Jurídico + Risco | Tendência crescente | LGPD; ISO/IEC 42001; ISO 31000 | B2B/B2C/C2B/C2C | Custo regulatório oculto | Repriorizar controles críticos e orçamento |

---

## 5) Painel para Conselho e Comitês

### Visão executiva

- **Quais IAs usamos?** 5 capacidades com evidência documental + 6 categorias ainda sem confirmação formal (inventário pendente).
- **Quanto custam?** [PREMISSA] sem baseline consolidado; exigir FinOps por sistema (infra, licença, operação, terceiros).
- **Quais riscos assumimos?** Privacidade de dados pessoais, viés de matching/scoring, excesso de autonomia, incidentes de segurança e risco contratual.
- **Quanto valor geram?** [PREMISSA] sem mensuração consolidada; medir ROI por sistema e impacto em EBIT.
- **Onde acelerar/controlar/corrigir/parar?**
  - **Acelerar:** ROI >= 20%, conformidade >= 95%, risco residual baixo.
  - **Controlar:** ROI positivo com risco médio ou conformidade 90–95%.
  - **Corrigir:** ROI baixo (0–20%) ou lacuna relevante de segurança/LGPD.
  - **Parar:** ROI negativo por 2 ciclos + risco alto não mitigado.

### Perguntas para Conselho/Comitê

1. Sabemos inventário/custo/risco/valor? **Parcial; falta fechamento de inventário e FinOps por sistema.**
2. Como algo funciona e não gera retorno? **Quando métrica técnica sobe, mas KPI de negócio (conversão/custo/EBIT) não muda.**
3. Como algo está conforme e não gera valor? **Quando cumpre LGPD/auditoria, mas ROI é nulo/negativo.**
4. Quem responde por cada sistema? **[PREMISSA] definir owner técnico + owner de negócio obrigatório por ID.**
5. Quem pode interromper? **Operações/Segurança (imediato), DPO (privacidade), Comitê IA (decisão estrutural).**
6. Conseguimos provar com evidências? **Só após trilha mínima: logs, políticas, contratos, RIPD e dashboards versionados.**

---

## 6) RACI e fluxos de governança

### RACI (resumo)

| Atividade | Conselho | Comitê IA | Dono Negócio | Resp. Técnico | DPO | Segurança | Jurídico | Auditoria |
|---|---|---|---|---|---|---|---|---|
| Definir apetite de risco de IA | A | R | C | C | C | C | C | I |
| Aprovar entrada em produção | I | A | R | R | C | C | C | I |
| Validar base legal/RIPD | I | C | C | C | A/R | C | C | I |
| Definir controles de segurança/kill switch | I | C | I | R | C | A/R | I | I |
| Monitorar ROI e KPIs | I | C | A/R | C | I | I | I | I |
| Responder incidente de IA | I | C | C | R | A (privacidade) | A/R (segurança) | C | I |
| Auditoria periódica | I | C | I | I | C | C | C | A/R |

### Fluxo operacional (aprovação, escalonamento e interrupção)

1. **Intake** (demanda + hipótese de valor + classificação B2B/B2C/C2B/C2C).
2. **Mapeamento** (dados, base legal, risco, autonomia, criticidade).
3. **Gate de conformidade mínima** (LGPD, segurança, contrato, evidências).
4. **Gate de valor** (KPI de negócio + baseline + meta).
5. **Deploy controlado** (HITL ativo + limites de autonomia + kill switch testado).
6. **Operação contínua** (monitoramento técnico, risco e ROI).
7. **Escalonamento** (quebra de threshold -> corrigir/controlar/parar).
8. **Auditoria e aprendizado** (lições, atualização de política e inventário).

---

## 7) Plano de ação 30/60/90 dias

### 0–30 dias

- Fechar inventário único de IA (ID, owner técnico/negócio, status, autonomia, criticidade).
- Publicar padrão de evidências (fonte, log, contrato, política, periodicidade).
- Implantar dashboard mínimo com 12 métricas (6 compliance + 6 valor).
- Formalizar matriz de criticidade e regra de kill switch.

### 31–60 dias

- Executar RIPD/DPIA nos sistemas de maior impacto.
- Implantar HITL operacional com SLA e escalonamento por risco.
- Integrar DPO, Segurança, Jurídico e Risco no fluxo de aprovação.
- Validar baseline de custo e ROI por sistema.

### 61–90 dias

- Rodar 1 ciclo completo de auditoria de IA (amostra crítica).
- Aplicar decisões de portfólio: acelerar/controlar/corrigir/parar por evidência.
- Revisar contratos/DPA/SLA de fornecedores e subprocessadores.
- Reportar ao Conselho: risco residual, valor capturado e backlog de correção.

---

## 8) Referências citáveis

1. **LGPD (Lei 13.709/2018)**: arts. 6º, 7º, 9º, 18, 37, 46.
2. **NIST AI RMF 1.0**: Govern, Map, Measure, Manage.
3. **ISO/IEC 42001:2023** (AIMS).
4. **ISO/IEC 27001:2022** (ISMS e controles de segurança).
5. **ISO 31000:2018** (gestão de riscos).
6. **IBM CEO Study** (2.000 CEOs; referência de ROI/escala) **[PREMISSA: validar edição exata]**.
7. **McKinsey State of AI** (impacto em EBIT; distribuição de captura de valor) **[PREMISSA: validar edição exata]**.
8. Evidência interna Radar:
   - `/home/runner/work/Radar/Radar/docs/ARQUITETURA.md:40-42,50-51,82-89,114,126-129`
   - `/home/runner/work/Radar/Radar/docs/JORNADAS.md:6`
9. Políticas internas, contratos, DPAs, SLAs, logs e auditorias: **[PREMISSA: mapear e anexar por sistema]**.

---

## 9) Premissas e lacunas

- **[PREMISSA]** Organização/setor/porte não informados.
- **[PREMISSA]** Jurisdição principal (Brasil/UE/EUA) não confirmada; assume Brasil pela LGPD.
- **[PREMISSA]** Owners técnicos e de negócio por sistema não definidos.
- **[PREMISSA]** Custos por sistema e baseline de ROI/EBIT não consolidados.
- **[PREMISSA]** DPO/Encarregado e comitês formais não identificados.
- **[PREMISSA]** Catálogo oficial para chatbot/copiloto/agente/RAG/IA embarcada não disponível.
- **[PREMISSA]** Política de retenção, transferência internacional e subprocessadores precisa de validação documental.

### Critério para conflito velocidade vs controle

- Se **risco LGPD/segurança alto** e sem mitigação comprovada: **controlar/corrigir/parar** mesmo com ROI potencial.
- Se **conformidade alta** e **valor baixo por 2 ciclos**: **corrigir ou parar**.
- Só **acelerar** quando risco residual, conformidade e valor estiverem simultaneamente dentro das metas.
