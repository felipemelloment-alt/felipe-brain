# 🏦 MAPEAMENTO DAS 6 FINANCEIRAS - DOUTORIZZE

**Última atualização:** 13/12/2024
**Projeto:** Arsenal SYNTX (Browser Automation)
**Objetivo:** Automatizar simulação de crédito em 6 financeiras

---

## 📋 RESUMO GERAL

| # | Financeira | Resposta | Campos Únicos |
|---|------------|----------|---------------|
| 1 | Parcela Mais | Manual | Nome, Data nasc, Email, CEP |
| 2 | Aviva | Manual | Procedimento, Valor, Data, Duração |
| 3 | MaisTodos | Instantânea | Renda mensal, Valor solicitado |
| 4 | Capim | Instantânea | Valor tratamento, Situação profissional |
| 5 | KonsigaPay | Instantânea | Valor, Data vencimento |
| 6 | Dr.Cash | Instantânea | Clínica (dropdown), Email |

**Campos COMUNS a todas:** CPF, Telefone

---

## 1️⃣ PARCELA MAIS

### Informações
- **URL:** https://parcelamais.com/novaportal
- **Tipo de resposta:** Manual (análise posterior)

### Fluxo de Automação
```
Login 
  → Financiamentos 
  → + SOLICITAR 
  → Financiamento 
  → Completo 
  → CPF (valida) 
  → Preencher formulário
```

### Campos Obrigatórios
| Campo | Tipo | Observação |
|-------|------|------------|
| CPF | input | Validação automática |
| Nome | input | |
| Data nascimento | date | |
| Email | input | |
| Telefone | input | |
| CEP | input | |

---

## 2️⃣ AVIVA

### Informações
- **URL:** https://grupomello.avivapay.com.br/flipcred/pedidos
- **Tipo de resposta:** Manual
- **⚠️ ÚNICA que pede procedimento ANTES da pré-aprovação**

### Fluxo de Automação
```
Login 
  → Solicitações 
  → "+" 
  → CPF 
  → Confirmar cadastro 
  → Nome + WhatsApp 
  → Procedimento + Valor + Data + Duração 
  → Salvar
```

### Campos Obrigatórios
| Campo | Tipo | Observação |
|-------|------|------------|
| CPF | input | |
| Nome | input | Auto-preenchido após CPF |
| WhatsApp | input | |
| Procedimento | dropdown | ~50 opções |
| Valor | input | R$ |
| Data início | date | |
| Duração | dropdown | Ver opções abaixo |

### Opções de Procedimento (principais)
- Implante
- Invisalign
- Aparelhos ortodônticos
- Clareamento
- Próteses
- Lentes de contato dental
- Facetas
- Tratamento de canal
- Extração
- Limpeza/Profilaxia

### Opções de Duração
- Menos de 1 mês
- 1-3 meses
- 3-6 meses
- 6-12 meses
- Mais de 12 meses

---

## 3️⃣ MAISTODOS

### Informações
- **URL:** https://plataforma.maistodos.com.br/hub-credit/simulations/create
- **Tipo de resposta:** ✅ Instantânea (CDC/FGTS/INSS)

### Fluxo de Automação
```
Login 
  → Crédito 
  → Simulações 
  → Fazer simulação 
  → Preencher tudo 
  → Salvar e simular
```

### Campos Obrigatórios
| Campo | Tipo | Observação |
|-------|------|------------|
| CPF | input | |
| Nome | input | |
| Data nascimento | date | |
| CEP | input | |
| Email | input | |
| Telefone | input | |
| Renda mensal | input | R$ |
| Valor solicitado | input | R$ |

---

## 4️⃣ CAPIM

### Informações
- **URL:** https://dash.capim.com.br
- **Tipo de resposta:** ✅ Instantânea
- **Range de valor:** R$ 1.000 a R$ 30.000

### Fluxo de Automação
```
Login 
  → Financiamento Capim 
  → Simular 
  → Etapa 1 (Valor R$1k-30k) 
  → Etapa 2 ("Não tenho paciente cadastrado") 
  → Dados 
  → Checkbox SCR ✓
  → Continuar 
  → Etapa 3 (Resultado)
```

### Campos Obrigatórios
| Campo | Tipo | Observação |
|-------|------|------------|
| Valor tratamento | input | R$ 1.000 - R$ 30.000 |
| CPF | input | |
| Telefone | input | |
| Situação profissional | dropdown | Ver opções |
| CEP | input | |

### Opções de Situação Profissional
- Autônomo
- Empresário
- Do lar
- Funcionário público
- Aposentado/Pensionista
- Profissional liberal
- Estudante
- Desempregado
- Assalariado/Registrado

---

## 5️⃣ KONSIGAPAY

### Informações
- **URL Login:** https://entrar-dentista.konsigapay.com.br
- **URL Simulação:** https://cadastro-proposta.konsigapay.com.br
- **Tipo de resposta:** ✅ Instantânea
- **⚠️ NUNCA marcar "Irá informar Avalista"**

### Fluxo de Automação
```
Login 
  → Painel 
  → CDC 
  → (fechar anúncio se aparecer) 
  → Modal Comunicado 
  → Continuar 
  → Preencher 
  → Calcular parcelas
```

### Campos Obrigatórios
| Campo | Tipo | Observação |
|-------|------|------------|
| CPF | input | |
| Telefone | input | |
| Valor | input | R$ |
| Data vencimento | dropdown | Datas próximas |

### Regras Especiais
- Fechar popup de anúncio se aparecer
- Fechar modal de comunicado
- **NUNCA** marcar checkbox de avalista

---

## 6️⃣ DR.CASH

### Informações
- **URL:** https://portal.drcash.com.br
- **Tipo de resposta:** ✅ Instantânea

### Fluxo de Automação
```
Login 
  → Nova simulação 
  → Step 1 (Informações) 
  → Próximo 
  → Step 2 (Pré análise = Resultado)
```

### Campos Obrigatórios
| Campo | Tipo | Observação |
|-------|------|------------|
| Clínica | dropdown | Auto-preenchido |
| CPF | input | |
| CEP | input | |
| Celular | input | |
| Email | input | |

---

## 🔧 INTEGRAÇÃO COM ARSENAL SYNTX

### Estrutura de Dados do Lead
```json
{
  "cpf": "string",
  "nome": "string",
  "telefone": "string",
  "email": "string",
  "data_nascimento": "YYYY-MM-DD",
  "cep": "string",
  "renda_mensal": "number",
  "valor_solicitado": "number",
  "procedimento": "string",
  "situacao_profissional": "string"
}
```

### Prioridade de Simulação
1. **Capim** - Resposta instantânea, mais rápido
2. **KonsigaPay** - Resposta instantânea
3. **Dr.Cash** - Resposta instantânea
4. **MaisTodos** - Resposta instantânea, mais completo
5. **Parcela Mais** - Manual
6. **Aviva** - Manual, requer mais dados

---

## 📁 ARQUIVOS RELACIONADOS

- `financeiras.json` - Estrutura JSON para código
- `.env.financeiras` - Credenciais (NÃO COMMITAR\!)
- `.env.financeiras.template` - Template sem valores

---

**⚠️ CREDENCIAIS:** Nunca commitar no GitHub. Usar arquivo .env.financeiras local.
