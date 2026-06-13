# Mergulho Livre · Clínica Chatbot · 12/06/2026

**Tipo:** Mergulho (drone educação × drone trabalho)
**Aplicado em:** 🦷 Clínica Chatbot
**Duração do mergulho:** ~10 min de foco
**Saída:** 1 framework operacional + 3 conversas-teste + 5 validações concretas

---

## 🎯 O que é Mergulho (operacionalizado)

**Mergulho** = teste profundo que cruza 4 eixos pra provar resultado real:

| Eixo | Clínica |
|------|---------|
| 🎓 **Educação** (drone) | O que o paciente APRENDE na conversa (sobre a clínica, sobre saúde) |
| 🛠️ **Trabalho** (drone) | O que o BOT FAZ (responde, agenda, redireciona) |
| 🥗 **Nutrição** | O VALOR entregue (lead capturado, dúvida sanada, agendamento criado) |
| ⚙️ **Tecnologia** | O que AUTOMATIZA (RAG, intent classifier, guard rails) |

**Teste de prova:** "se a paciente sair da conversa COM VALOR REAL e SEM ATENDIMENTO HUMANO, o mergulho funcionou."

---

## 🧪 3 conversas-teste (simuladas, prontas pra virar dado real)

### Conversa 1: "Quanto custa limpeza?"
```
👤 Paciente: Oi, quanto custa uma limpeza?
🤖 Bot: Olá! 😊 Aqui é a [Clínica], assistente virtual.

   A limpeza (profilaxia) tá R$180, dura ~40min e inclui:
   • Avaliação geral da saúde bucal
   • Remoção de tártaro e placa
   • Polimento e orientação de higiene

   🦷 Atendemos com os convênios: Unimed, Amil, Bradesco Saúde.
   📅 Quer agendar? Me diz o melhor dia/horário.

👤 Paciente: Quarta de manhã
🤖 Bot: Beleza! Tenho quarta 10h ou 11h. Qual prefere?
👤 Paciente: 10h
🤖 Bot: ✅ Agendado: Quarta 18/06 às 10h — Limpeza, Dra. Mariana.
   Vou mandar confirmação por aqui 1 dia antes. Até lá! 🦷
```

**Eixos acionados:**
- 🎓 Educação: paciente entende o que é limpeza, tempo, cobertura
- 🛠️ Trabalho: bot identifica intenção (preço) → responde com KB → agenda
- 🥗 Nutrição: lead CAPTURADO + agendamento CRIADO
- ⚙️ Tech: intent classification + RAG + slot check (SQLite)

### Conversa 2: "Atende emergência agora?"
```
👤 Paciente: Tô com dor forte no dente, atendem agora?
🤖 Bot: ⚠️ Dor forte precisa de avaliação rápida, mas nosso
   horário de emergência hoje já fechou (17h). 

   📞 Te recomendo:
   • UPA 24h (R. das Acácias, 200) — 5 min de você
   • Hospital [X] tem odontologia de plantão

   Se preferir, amanhã às 8h a Dra. Mariana tem slot
   de urgência. Quer que eu reserve?

👤 Paciente: Pode ser amanhã 8h
🤖 Bot: ✅ Reservado Amanhã 13/06 08h — Urgência dor,
   Dra. Mariana. Leve documento com foto + carteirinha.
```

**Eixos acionados:**
- 🎓 Educação: paciente sabe pra onde ir AGORA + tem plano B
- 🛠️ Trabalho: bot detecta emergência, redireciona com ética, oferece agenda
- 🥗 Nutrição: paciente NÃO fica desamparado (mesmo fora do horário)
- ⚙️ Tech: classificador de urgência + KB de emergências + slot check

### Conversa 3: "Aceita Pix?"
```
👤 Paciente: Forma de pagamento inclui Pix?
🤖 Bot: Aceitamos:
   💳 Pix (5% desconto à vista)
   💳 Cartão (parcelamos em até 3x sem juros)
   💵 Dinheiro
   🏥 Convênio (Unimed/Amil/Bradesco)

   Quer que eu mande a tabela completa de preços?
👤 Paciente: Manda sim
🤖 Bot: [PDF da tabela enviado] 📎
   Qualquer dúvida, tô por aqui. Quer agendar?
```

**Eixos acionados:**
- 🎓 Educação: paciente recebe info completa (não só Pix)
- 🛠️ Trabalho: bot responde, oferece PDF, deixa porta aberta
- 🥗 Nutrição: paciente sente que tá sendo BEM ATENDIDO (upsell natural)
- ⚙️ Tech: KB de pagamento + envio de asset + lead tracking

---

## ✅ 5 validações que PROVAM o mergulho funcionou

| # | Validação | Métrica-alvo |
|---|-----------|--------------|
| 1 | Paciente recebe resposta útil em < 5s | Latência P95 |
| 2 | Taxa de "entendi e continuei" | > 70% das conversas |
| 3 | Zero prompt-injection que passou do guard rail | Count = 0 |
| 4 | Taxa de agendamento criado / conversa | > 30% |
| 5 | Paciente FINALIZA conversa sem pedir humano | > 60% |

Se 4 das 5 passarem em 50 conversas reais → mergulho provado → primeira clínica pagante.

---

## 🔄 Próximo mergulho (sugestão)

Quando a Clínica tiver 1 cliente piloto rodando 7 dias:
- **Mergulho 2:** aplicar a 🤖 PM Skills — ver se o conceito "PM cover the whole frontier" funciona na prática com 1 PM em trial
- **Comparar:** os 2 mergulhos lado a lado (nutrição × tech, mesmo framework, projetos diferentes)

---

**Anotação 12/06:** Mergulho livre ≠ mergulho solto. É mergulho COM FRAMEWORK (4 eixos) + COM OUTPUT (artefato concreto, como este .md) + COM VALIDAÇÃO (métricas pra provar que funcionou).

**Origem:** "mergulho livre" dito por Renato 12/06 às ~21h Manaus, em meio a uma divagação sobre drone da educação × drone do trabalho.
