# TRD: Agent-PM Skills Marketplace

## Problema
PO/PM freelance precisa de framework pra montar, validar e operar agentes de IA sem começar do zero. Hoje cada projeto reinventa o mesmo conjunto de skills (discovery, strategy, execution, launch, growth).

## Persona
PO/PM brasileiro, 25-40 anos, freelancer ou micro-SaaS builder. Trabalha sozinho ou com 1-2 devs. Precisa shipar rápido, sem bureaucracy.

## JTBD
Quando eu inicio um projeto de agente de IA, quero usar um framework de skills pré-validadas, pra não perder tempo reinventando prompting e chain design.

## Solução
Marketplace de skills modulares (discovery, strategy, execution, launch, growth) onde cada skill é um prompt + chain + tool spec. O usuário monta seu agente como LEGO.

## Métricas
- Nº de skills instaladas por usuário
- Tempo médio pra montar um agente (meta: <2h)
- Retenção D7 (voltou depois de 7 dias?)

## MVP
- 20-30 skills core em categorias fixas
- Interface web pra montar agente (seleciona skills, define ordem)
- Exportar como prompt LangChain/LlamaIndex
- 1 template de agente completo funcional

## Fora-de-escopo
- Marketplace de skills comunitárias (v1)
- Billing/pagamento dentro da plataforma
- Agente auto-executável (só output = prompt/chain)

## Riscos
1. Skills genéricas demais não resolvem dor específica
2. Usuário prefere copiar prompt de tweet do que pagar
3. Concorrência de frameworks maiores (LangChain templates, Superpowers)

---

*Atlas Drone · 2026-06-11 · Origem: dados.json GitHub Trending + insights 11/06*
