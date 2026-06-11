# TRD: AI Agent Research Tool

## Problema
Renato precisa researchar oportunidades de produto todo dia. Hoje faz manualmente (Google, HN, GitHub). last30days-skill (38.6K stars) mostra que existe demanda por pesquisa automatizada multi-plataforma.

## Persona
Renato — research diário de oportunidades, 30-60min por dia. Precisa filtrar sinal de ruído e ter insight acionável, não só links.

## JTBD
Quando eu preciso researchar um nicho, quero que o agente pesquise em múltiplas fontes simultaneamente e me entregue um resumo com oportunidades concretas, não só uma lista de links.

## Solução
CLI/web tool que usa last30days-skill ou similar pra pesquisar tema X em Reddit, X, HN, Polymarket, YouTube e entrega relatório estruturado. Integra com Telegram pra notificação diária (Atlas).

## Métricas
- Tempo salvo por research (meta: 30min → 5min)
- % de insights que viram ação (anotado por Renato)
- Qualidade percebia (1-5 stars via Telegram)

## MVP
- Input: tema/nicho em texto
- Output: relatório markdown com fontes + oportunidades
- 5 plataformas: Reddit, X, HN, Polymarket, GitHub
- Agendamento: daily 07:30 (coupled with 0ddc)

## Fora-de-escopo
- Dashboard visual
- Alertas em tempo real
- Multi-usuário

## Riscos
1. API rate limits das plataformas
2. Qualidade do resumo depende de prompt engineering
3. Renato abandona se não ver valor em 2 semanas

---

*Atlas Drone · 2026-06-11 · Origem: dados.json GitHub Trending + skill 0ddc + insights 11/06*
