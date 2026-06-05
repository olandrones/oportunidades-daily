# Padrão Visual — Oportunidades Daily

## 🎯 Regra de Ouro

> **Cronjob toca SOMENTE dados.json. HTML é intocável.**

Se um cronjob reescrever o HTML, restaurar imediatamente com `git restore`.

---

## 🏗️ Layout Padrão

O site viver em: `https://olandrones.github.io/oportunidades-daily/`

**Estrutura:**
1. **Header** — título "📊 Oportunidades Diárias" + subtítulo com frequência de atualização
2. **Resumo** — bloco no topo com stats do dia (total oportunidades, categorias, tendências)
3. **Filtros** — botões de categoria (Todas | 🔥 Tendência | 🚀 App | 💼 Negócio)
4. **Região** — botões de origem (Todas | 🌐 Global | 🇧🇷 Brasil)
5. **Ordenação** — "🔥 Ordenar por calor"
6. **Cards** — grid de oportunidades com: título, badge, metrics, descrição, tags

---

## 📋 Estrutura do Card

```
┌─────────────────────────────────────────────┐
│ [Badge]                           [Volume]  │
│ Título do Card                              │
│                                             │
│ 📊 376K  🚀 908 stars/dia  📌 GitHub Trending│
│                                             │
│ Descrição do card em até 4 linhas...        │
│                                             │
│ [NOVO] [categoria] [origem] tag1 tag2 tag3  │
└─────────────────────────────────────────────┘
```

---

## 🔴 Nunca Fazer

- ❌ Editar index.html manualmente (é o template de produção)
- ❌ Gerar novo HTML a partir do cronjob
- ❌ Remover seção de resumo do topo
- ❌ Mudar estilo CSS (cores, fontes, espaçamento)
- ❌ Publicar em daridaclaw.github.io (usar olandrones)

---

## ✅ Sempre Fazer

- ✅ Atualizar dados.json com novos itens
- ✅ Manter campos: titulo, descricao, badge, volume, crescimento, tags, categoria, origem, data_publicacao
- ✅ Push para origin após atualizar dados.json
- ✅ Verificar site no ar após push

---

## 📦 Publicação

1. Editar `dados.json` na pasta `oportunidades/`
2. `cd oportunidades && git add . && git commit -m "Update $(date +%d/%m/%Y)" && git push`
3. GitHub Pages atualiza automaticamente em ~1 min

---

## 👥 Times

- **IAA (Conteúdo)**: pesquisa e adiciona itens em dados.json
- **Manutenção**: verifica se HTML não foi sobrescrito, mantém padrão visual

---

*Atualizado: 05/06/2026*