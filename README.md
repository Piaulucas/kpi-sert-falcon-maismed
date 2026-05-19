# KPI Dashboard — Sert Med · Falcon · Mais Med

Dashboard de visualização de KPIs operacionais e financeiros para três empresas de UTI móvel contratadas pela SESAB (Secretaria de Saúde do Estado da Bahia).

## O que faz

Lê dados já processados do banco PostgreSQL e exibe um painel comparativo por empresa com atualização automática a cada 5 minutos. Não realiza ingestão de dados — apenas visualização.

> **Pipeline de dados:** a extração das planilhas e carga no banco é feita pelo repositório [`kpi-maismed`](https://github.com/Piaulucas/kpi-maismed), via `atualizar_kpi_multi.py`.

## Empresas monitoradas

| Empresa |
|---|
| Sert Med |
| Falcon |
| Mais Med |

## Stack

- **Python** · psycopg2 · Pandas
- **Streamlit** — interface do dashboard
- **PostgreSQL / Supabase** — fonte dos dados
- **Plotly** — gráficos comparativos e de evolução

## Arquitetura

```
PostgreSQL (Supabase)                  ← dados carregados pelo kpi-maismed
        ↓
dashboard_sert_falcon_maismed.py       ← leitura e visualização
```

## KPIs exibidos por empresa

| Indicador | Descrição |
|---|---|
| Valor Consolidado | Faturamento total até o corte |
| Faturamento/dia | Média diária de receita |
| Previsão de Faturamento | Projeção para o mês |
| Remoções Adulto / Neonatal | Volume por tipo |
| Remoções/dia | Média diária de atendimentos |
| Km/dia | Média diária de quilometragem |
| Ticket Médio | Receita por remoção |

## Como rodar localmente

```bash
pip install -r requirements.txt
```

Crie o arquivo `.env` com as credenciais do banco:

```
DB_HOST=...
DB_PORT=5432
DB_NAME=postgres
DB_USER=...
DB_PASS=...
```

Inicie o dashboard:

```bash
streamlit run dashboard_sert_falcon_maismed.py
```

---
Desenvolvido por [Lucas Piau](https://linkedin.com/in/lucaspiausantana) · Piau Gestão em Saúde
