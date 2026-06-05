# Padrão Visual — Oportunidades Daily

## ⚠️ REGRA DE OURO

> **Cronjob/edição toca SOMENTE dados.json. HTML é intocável.**
> Se alguém editar HTML, restaurar: `git restore index.html`

---

## 🌐 Site Oficial

**URL:** https://olandrones.github.io/oportunidades-daily/

> ⚠️ NÃO usar daridaclaw.github.io — está desatualizado.

---

## 🏗️ Layout Padrão

**Header:**
- Título: "📊 Oportunidades Diárias"
- Subtítulo: "Relatório automático de tendências e oportunidades — atualizado 3x ao dia"

**Resumo Semântico (TOPO):**
Bloco clicável com stats:
- Total de entradas
- Por categoria (🔥 tendência, 🚀 app, 💼 negócio)
- Por origem (🌐 global, 🇧🇷 brasil)
- Top 6 tags

**Filtros:**
- Categoria: Todas | 🔥 Tendência | 🚀 App | 💼 Negócio
- Origem: Todas | 🌐 Global | 🇧🇷 Brasil
- Ordenar: 🔥 Ordenar por calor

**Cards:**
- Título + badge
- Metrics: volume, crescimento, fonte
- Descrição (2 linhas)
- Tags
- Origem (🌐/🇧🇷)

---

## 📦 Arquivos Válidos

```
oportunidades/
├── index.html              ← ✅ Template oficial
├── dados.json              ← ✅ Dados
├── STANDARDS.md            ← ✅ Este arquivo
└── DATA_MANAGEMENT_SOP.md  ← ✅ SOP de gestão
```

### ❌ ARQUIVOS PROIBIDOS (apagados)
- oportunidades.html — DELETE
- template.html — DELETE
- test.txt — DELETE

---

## 📝 Schema de Dados (dados.json)

```json
{
  "categoria": "tendencia|app|negocio",
  "origem": "global|brasil",
  "titulo": "string",
  "badge": "string",
  "volume": "string (ex: '376K')",
  "crescimento": "string (ex: '908 stars/dia')",
  "stars": 375868,
  "forks": "78,478",
  "descricao": "string",
  "tags": ["AI", "assistant"],
  "fonte": "GitHub Trending",
  "data_publicacao": "DD/MM/YYYY HH:MM"
}
```

---

## 🔄 Publicação

```bash
cd oportunidades
git add .
git commit -m "Update $(date +%d/%m/%Y)"
git push
# GitHub Pages atualiza em ~1 min
```

---

*Atualizado: 05/06/2026*