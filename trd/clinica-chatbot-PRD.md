# TRD · Clínica Chatbot WhatsApp — Arquitetura

**Data:** 2026-06-12
**Autor:** Hermes (com Renato)
**Status:** Draft v1 — esperando 3 decisões (VPS, provider WhatsApp, visualização)
**Prioridade:** URGENTE (este fim-de-semana)

---

## Problema

Clínicas (odontologia, médica) perdem leads que chegam via WhatsApp fora do horário comercial ou porque a recepção tá ocupada. Resposta lenta = lead frio = receita perdida.

## Persona

- **Primária:** Dona/gerente de clínica pequena/média (1-5 médicos), 30-60 anos, NÃO técnica. Usa WhatsApp Business no celular.
- **Secundária:** Paciente que quer marcar consulta ou tirar dúvida rápido.
- **Terciária:** Recepção da clínica (vê o painel, dá override quando precisa).

## JTBD

**Quando** um paciente manda mensagem no WhatsApp da clínica **fora do horário** ou **com dúvida simples**, **eu quero** que ele receba uma resposta útil em segundos e consiga marcar a consulta sem precisar ligar, **para** não perder o lead e liberar a recepção.

## Solução proposta

Bot WhatsApp com IA que:
1. Identifica intenção (agendar, dúvida sobre preço, horário, convênio, etc.)
2. Responde dúvidas via RAG (base de conhecimento da clínica)
3. Agenda consulta (cria agendamento no SQLite com data/hora/especialidade)
4. Mostra painel admin em tempo real (conversa fluindo + leads entrando)
5. Tem guard rails de segurança (anti-prompt-injection, scope check, rate limit)

## Arquitetura (validada com print do Renato, 12/06)

```
PACIENTE → WhatsApp → [Meta / Evolution / Z-API] → Webhook → VPS
                                                              │
                                                              ▼
                                                    ┌─────────────────┐
                                                    │  HERMES AI      │
                                                    │  (orquestrador) │
                                                    └────┬───────┬────┘
                                                         │       │
                                            ┌────────────┘       └────────────┐
                                            ▼                                 ▼
                                      ┌──────────┐                    ┌──────────────┐
                                      │ 🛡 GUARD │                    │ 📚 RAG (KB)  │
                                      │  RAILS   │                    │  embeddings  │
                                      │ in/out   │                    │  no SQLite   │
                                      └────┬─────┘                    └──────┬───────┘
                                           │                                 │
                                           └────────────┬────────────────────┘
                                                        ▼
                                            ┌──────────────────────┐
                                            │  SQLite (vps.db)     │
                                            │  pacientes           │
                                            │  agendamentos        │
                                            │  historico_msgs      │
                                            │  rag_docs + vec      │
                                            └──────────┬───────────┘
                                                       ▼
                                            ┌──────────────────────┐
                                            │  Logs/Auditoria      │
                                            │  (arquivo rotativo)  │
                                            └──────────────────────┘

(Futuro) → API da Clínica (agenda médica, prontuário)
(Paralelo) → Painel Admin: ver conversas/leads em tempo real
```

## Stack proposto

| Camada | Escolha | Custo | Notas |
|--------|---------|-------|-------|
| VPS | Oracle Cloud Free Tier (ARM 4-core 24GB) | $0 | Always Free. Alternativa: Contabo BR R$30/mês |
| WhatsApp | Evolution API (open-source) | $0 + VPS | Webhook nativo. Alternativa: Z-API (pago por msg) |
| Backend | Node.js 20 + Fastify | $0 | Async, ecossistema WhatsApp maduro |
| LLM | OpenRouter (minimax-m2.7 ou claude-haiku) | ~R$0.01-0.05/conversa | Já configurado |
| RAG | sqlite-vec (extensão oficial) | $0 | Mesma DB. Alternativa: Chroma (overkill) |
| Embeddings | OpenRouter text-embedding-3-small | ~R$0.0001/doc | 1536-dim, em PT-BR |
| Guard Rails | Middleware Node custom | $0 | Regex + LLM judge para scope |
| Visualização | crescer.html /aba Clínica (WebSocket) | $0 | Mesmo stack que oportunidades/aprofundar |

## Métricas (definição de sucesso MVP)

| Métrica | Alvo fim-de-semana | Alvo 30 dias |
|---------|-------------------|--------------|
| Tempo 1ª resposta | < 5s | < 3s |
| Taxa de "entendi" (paciente segue conversa) | > 60% | > 80% |
| Agendamentos criados via bot | ≥ 1 | ≥ 5/semana |
| Taxa de erro (LLM/RAG) | < 5% | < 2% |
| Falsos positivos do guard rail | < 10% | < 5% |

## MVP (escopo fim-de-semana)

### ✅ Dentro
- VPS + Evolution API rodando
- Webhook → Node server que recebe mensagens
- SQLite com 3 tabelas (pacientes, agendamentos, historico)
- LLM identifica intenção (4-5 intents: agendar, dúvida, preço, convênio, humano)
- RAG com 20-30 docs básicos da clínica (FAQ, serviços, horários)
- Guard rails: rate limit (1 msg/2s por número), anti-injection básico, scope check ("só respondo sobre a clínica")
- Agendamento: cria evento no SQLite (sem API externa)
- Visualização: aba no crescer.html com últimas N conversas + leads do dia
- Logs: arquivo rotativo + métricas básicas (contagem por intent, latência)

### ❌ Fora (depois)
- Integração com API da clínica (prontuário, agenda médica)
- Multi-clínica (white-label)
- Painel admin completo com auth
- Pagamento integrado
- Suporte a voz (áudio WhatsApp)

## Riscos (top 3)

1. **WhatsApp ban**: Evolution é não-oficial. Risco de ban se volume alto. Mitigação: começar com 1 clínica teste, observar.
2. **Custo LLM escalar**: Se 1000 mensagens/dia, custo LLM sobe. Mitigação: cache de respostas similares (RAG cobre 80%), model mix (haiku p/ intents simples, sonnet só p/ conversas abertas).
3. **LGPD/PII**: Bot pode receber dados sensíveis (CPF, sintomas). Mitigação: PII detector no guard rail + política de retenção 30 dias + opt-in explícito.

## Decisões pendentes (3 perguntas abertas)

1. **VPS:** Renato já tem provisionado? (Oracle Cloud, Contabo, etc.)
2. **WhatsApp provider:** Evolution (rápido, grátis) ou Meta oficial (burocrático, confiável)?
3. **Visualização:** aba Clínica no crescer.html OU admin.html separado?

## Próximo passo

Após respostas: provisionar VPS (30 min) + subir Evolution (30 min) + scaffold Node server (1h) + SQLite schema (1h) = ~3h até "bot eco" funcionando. Resto do fim-de-semana: RAG + Guard Rails + Agendamento + Visualização.
