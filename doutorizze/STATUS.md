# 📍 Status Projeto Doutorizze

## ✅ Fase 1: Mapeamento (CONCLUÍDA - 13/12/2024)

### Arquivos criados:
- `FINANCEIRAS.md` - Documentação completa com fluxos
- `financeiras.json` - Estrutura JSON para código
- `.env.financeiras` - Credenciais (NÃO COMMITAR!)
- `.gitignore` - Atualizado para ignorar credenciais

### 6 Financeiras mapeadas:

| # | Financeira | URL | Resposta | Prioridade |
|---|------------|-----|----------|------------|
| 1 | Parcela Mais | parcelamais.com | Manual | 5 |
| 2 | AVIVA | avivapay.com.br | Manual | 6 |
| 3 | MaisTodos | maistodos.com.br | Instantânea | 4 |
| 4 | Capim | capim.com.br | Instantânea | 1 |
| 5 | KonsigaPay | konsigapay.com.br | Instantânea | 2 |
| 6 | Dr.Cash | drcash.com.br | Instantânea | 3 |

### Credenciais configuradas:
- ✅ Todas as 6 financeiras com login/senha no `.env.financeiras`
- ✅ Arquivo protegido (não vai pro GitHub)

---

## ⚠️ Diagnóstico Arsenal SYNTX (13/12/2024 - 19h)

### O que EXISTE:
- ✅ Infraestrutura Docker rodando (Oracle 164.152.59.49)
- ✅ Redis (pode ser usado pra fila)
- ✅ n8n funcionando (v1.123.5)
- ✅ Bot Telegram básico (@dcaibr_bot)
- ✅ Pasta ~/arsenal-syntx/ existe
- ✅ PostgreSQL leads rodando

### O que NÃO EXISTE (precisa criar):
- ❌ `workers/` (drivers das financeiras)
- ❌ `queue/` (sistema de fila)
- ❌ Playwright (browser automation)
- ❌ `driver_base.py` (template)
- ❌ Drivers das 6 financeiras

### Containers rodando:

| Container | Status | Função |
|-----------|--------|--------|
| n8n | ✅ Up 28h | Automação workflows |
| postgres-leads | ✅ Up 2d | Banco de leads |
| telegram-bot | ✅ Up 11d | Bot orquestrador |
| redis | ✅ Up 11d | Cache/Fila |

### Bot Telegram atual:
- `/start` - Boas-vindas
- `/status` - Status básico
- `/ias` - Lista 85 perfis TCS SPY
- `/help` - Ajuda
- **NÃO** tem orquestração real de financeiras

---

## 🔄 Fase 2: Implementação Arsenal SYNTX (A FAZER)

### Estrutura a criar em ~/arsenal-syntx/:

```
arsenal-syntx/
├── workers/
│   ├── __init__.py
│   ├── driver_base.py        # Classe base Playwright
│   ├── driver_capim.py       # Prioridade 1
│   ├── driver_konsigapay.py  # Prioridade 2
│   ├── driver_drcash.py      # Prioridade 3
│   ├── driver_maistodos.py   # Prioridade 4
│   ├── driver_parcelamais.py # Prioridade 5
│   └── driver_aviva.py       # Prioridade 6
│
├── queue/
│   ├── __init__.py
│   ├── job_processor.py      # Processa fila Redis
│   └── models.py             # Modelos de job
│
├── api/
│   ├── __init__.py
│   └── webhook.py            # Recebe requisições do n8n
│
├── Dockerfile.playwright     # Container com Playwright
├── requirements.txt          # Dependências Python
└── docker-compose.override.yml  # Adiciona worker ao compose
```

### Tecnologias:
- **Playwright** - Browser automation (suporta login persistente)
- **Redis** - Fila de jobs (já rodando!)
- **FastAPI** - Webhook para receber do n8n
- **PostgreSQL** - Salvar resultados (já rodando!)

### Fluxo planejado:
```
n8n (lead chega)
    ↓
Webhook FastAPI
    ↓
Redis Queue (job)
    ↓
Worker Playwright
    ↓
Simula nas 6 financeiras
    ↓
Salva no PostgreSQL
    ↓
Retorna pro n8n
```

### Decisões pendentes:
- [ ] Paralelo vs Sequencial (começar sequencial, depois paralelo)
- [ ] Parar na 1ª aprovação ou mostrar todas?
- [ ] Timeout por financeira (sugestão: 60s)
- [ ] Retry em caso de falha (sugestão: 1x)
- [ ] Screenshots de comprovação

---

## 🔮 Fases Futuras

### Fase 3: Integração n8n
- Webhook recebe dados do paciente
- Dispara Arsenal SYNTX
- Retorna resultados para IA Natália
- Salva no PostgreSQL (lead_sessions)

### Fase 4: Front-end Doutorizze
- Interface para dentistas
- Dashboard de simulações
- Histórico de leads
- Relatórios de conversão

### Fase 5: Escala
- Multi-clínica
- API pública para parceiros
- White-label

---

## 📊 Métricas (a implementar)

| Métrica | Atual | Meta |
|---------|-------|------|
| Simulações/dia | 0 | 100+ |
| Taxa aprovação | - | 40%+ |
| Tempo médio simulação | - | < 60s |
| Financeiras ativas | 0/6 | 6/6 |
| Drivers implementados | 0/6 | 6/6 |

---

## 📝 Histórico de Sessões

### 13/12/2024 - 19h - Diagnóstico Arsenal SYNTX
- Verificado estrutura real do arsenal-syntx
- Descoberto que NÃO tem workers/drivers
- Bot Telegram é apenas placeholder
- Redis pode ser usado como fila
- Definido estrutura para Fase 2

### 13/12/2024 - 18h - Mapeamento Completo
- Criado estrutura ~/felipe-brain/doutorizze/
- Mapeadas 6 financeiras com fluxos detalhados
- Configuradas credenciais no .env.financeiras
- Commit no GitHub (10f6cbf)

---

*Última atualização: 13/12/2024 19:30*
