# TRD: Open Notebook LM Clone (Exocerebro v1)

## Problema
Renato precisa de um sistema pessoal de conhecimento que cresce com interação. NotebookLM tem a UX mas é SaaS fechado. Open Notebook LM (27K stars) é open source — dá pra customizar.

## Persona
Renato — PO 25 anos, múltiplos projetos, precisa de memória externa que evolua com ele. Contexto: empreender, micro-SaaS, sair do CLT.

## JTBD
Quando eu estudo um tema, quero que o sistema registre o que eu aprendi e me mostre conexões com outros temas que eu já estudei, pra eu não perder contexto.

## Solução
Fork do Open Notebook LM adaptado pra uso pessoal: local-first (dados no browser/localStorage), anotações em Markdown, conexões automáticas entre notas via embedding. Mobile-responsive.

## Métricas
- Nº de notas criadas por semana
- Nº de conexões (links entre notas) geradas
- D7 retention (voltou no dia seguinte?)

## MVP
- 3 funcionalidades core: criar nota, buscar por embedding, ver conexões
- Index local com Chroma.js (client-side)
- Importar URLs pra resumir (scraping simples)
- Interface mobile-friendly

## Fora-de-escopo
- Multi-usuário / sharing
- Integração com APIs externas (v1 = só local)
- Sync entre dispositivos (v1 = browser only)

## Riscos
1. Chroma.js client-side pode ser lento com muitas notas
2. Renatao prefere Notion/obsidian e abandona
3. Embedding local sem GPU é limitado

---

*Atlas Drone · 2026-06-11 · Origem: dados.json GitHub Trending + exocerebro Renato + insights 11/06*
