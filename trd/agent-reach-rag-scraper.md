# TRD: Agent-Reach RAG Scraper

## Problema
Agente de IA precisa de dados atualizados do mercado (Reddit, X, HN, GitHub) mas scrapers pagos (SerpAPI, ScrapeAPI) custam caro. Arquitetura atual do Agent-Reach (24K stars) mostra que dá pra fazer de graça com CLI.

## Persona
Dev brasileiro construindo produto SaaS ou agente de IA. Precisa alimentar seu RAG com dados de mercado sem gastar em APIs de scraping.

## JTBD
Quando meu agente precisa research de mercado, quero que ele busque direto em múltiplas plataformas (X, Reddit, HN) sem eu pagar API, pra eu validar hipóteses de produto rápido.

## Solução
CLI que abstrai Agent-Reach e similares, alimentando diretamente um vector store (Qdrant/Chroma). Integra com LlamaIndex como tool de busca. Custo zero em APIs.

## Métricas
- Nº de queries/mês por usuário
- Tempo até insight (query → resultado vetorial)
- Precisão da busca (relevância medida por click-through)

## MVP
- Tool Agent-Reach como tool LangChain
- Indexação automática em Qdrant cloud (free tier)
- Query interface via chat (RAG completo)
- Suporte a 4 plataformas: X, Reddit, HN, GitHub

## Fora-de-escopo
- Scheduling automático de queries
- Análise de sentimiento / trends
- Dashboards visuais (v1 = só chat)

## Riscos
1. Rate limiting das plataformas bloqueia o scraper
2. Qualidade do dado scraped varia demais
3. Vector store free tier limita escala

---

*Atlas Drone · 2026-06-11 · Origem: dados.json GitHub Trending + insights 11/06*
