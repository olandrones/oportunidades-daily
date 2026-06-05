# SOP — Gestão de Dados dos Boards

## 🎯 Objetivo

Garantir que todos os agentes sigam o mesmo padrão na gestão de dados. Sem desculpas, sem variação, sem "cada um faz do seu jeito".

---

## 📋 Regras de Ouro

1. **HTML é intocável** — Nunca editar HTML manualmente. Só dados.json.
2. **Template oficial é index.html** — Não existe outro.
3. **Publicar no repo certo** — olandrones (não daridaclaw)
4. **GitHub Pages atualiza automatico** — push = publicado

---

## 🏗️ Arquitetura de Cada Board

```
[NOME]/
├── index.html          ← Template oficial (NUNCA editar)
├── dados.json          ← Dados (EDITAR só este)
├── STANDARDS.md        ← Padrão visual do board
└── DATA_MANAGEMENT_SOP.md ← Este arquivo
```

---

## 📊 Template Oficial — Oportunidades

**Local:** `E:\01 - Team Claw\hermes  - Lyriane\oportunidades\index.html`

**Estrutura:**
1. Header: "📊 Oportunidades Diárias"
2. Resumo semântico: stats clicáveis (total, categorias, origens, tags)
3. Filtros: categoria + origem + ordenar por calor
4. Grid de cards: título, badge, metrics, descrição, tags
5. Footer: contagem + timestamp

**Dados necessários em dados.json:**
```json
{
  "titulo": "string",
  "badge": "string",
  "descricao": "string",
  "volume": "string",
  "crescimento": "string",
  "stars": number,
  "forks": "string",
  "tags": ["string"],
  "categoria": "tendencia|app|negocio",
  "origem": "global|brasil",
  "fonte": "string",
  "data_publicacao": "DD/MM/YYYY HH:MM"
}
```

---

## 🔄 Fluxo de Trabalho dos Agentes

### Agente de Pesquisa (6h, 12h, 18h)

1. Carregar skill `web-research`
2. Executar pesquisa
3. Formatar dados conforme schema acima
4. Editar `dados.json` (adicionar/remover itens)
5. Commitar: `git add . && git commit -m "Update $(date +%d/%m/%Y)" && git push`
6. **NÃO editar index.html**

### Agente de Manutenção (9h)

1. Verificar se `index.html` não foi modificado (git status)
2. Se modificado: `git restore index.html`
3. Verificar se `dados.json` está atualizado
4. Verificar se GitHub Pages está no ar
5. Reportar anomalias

---

## 🚫 O Que Não Fazer

- ❌ Editar index.html
- ❌ Criar novo HTML (ex: oportunidades.html, template.html)
- ❌ Usar repo daridaclaw
- ❌ Commitar arquivos de teste (.txt, etc)
- ❌ Reescrever dados.json inteiro (merge, não replace)

---

## 📁 Estrutura de Arquivos Válidos

```
oportunidades/
├── index.html          ✅ Template oficial
├── dados.json          ✅ Dados
├── STANDARDS.md        ✅ Padrão visual
└── DATA_MANAGEMENT_SOP.md ✅ Este SOP

comportamento/
├── index.html          ✅ Template
├── dados.json          ✅ (criar se não existir)
├── perguntas_anteriores.md
├── perguntas_coaching.md
├── STANDARDS.md
└── DATA_MANAGEMENT_SOP.md
```

---

## 🔧 Como Resolver Problemas

| Problema | Solução |
|----------|---------|
| Layout mudou | `git restore index.html` |
| Dados sumiram | Verificar git log, restaurar |
| Site fora do ar | Verificar GitHub Pages + push |
| Conflito de merge | Manter dados, não HTML |

---

## 📅 Revisão

Este SOP deve ser seguido por TODOS os agentes sem exceção.
Revisar a cada 30 dias ou quando houver mudança de padrão.

*Atualizado: 05/06/2026*