# Matriz SPECs — Fase 1 RN Engenharia

**Status:** planejada — cliente aprovado; tasks ainda não geradas.
**Escopo:** Central Financeira de Obras construtora-first.

| Requisito/fase | SPEC | Critérios de aceite | Prova/TDD |
|---|---|---|---|
| RF-06, D7 — acesso e posição publicada | SPEC-1-001 | CA-1-001..004 | RED/GREEN/REGRESSÃO de papéis, preparação e versão |
| RF-01, D4 — ciclo em uma obra | SPEC-1-002 | CA-1-005..008 | RED/GREEN/REGRESSÃO de obra, corte, visão e validações |
| RF-02/RF-03, D3/D10 — importação e proveniência | SPEC-1-003 | CA-1-009..013 | RED/GREEN/REGRESSÃO de fixture, idempotência e quarentena |
| RF-04, RN-01/RN-02/RN-07 — consolidação semanal | SPEC-1-004 | CA-1-014..018 | RED/GREEN/REGRESSÃO com oráculo independente |
| RF-05/RF-06, RN-08/RN-10/RN-11/RN-13 — divergências/publicação | SPEC-1-005 | CA-1-019..025 | RED/GREEN/REGRESSÃO de bloqueio e versionamento |

## Cobertura dos critérios

- **25 CAs únicos:** CA-1-001 a CA-1-025, sem colisões.
- Cada SPEC contém Resultado, Limites, Dependências, Fluxo, Erros, Checklist, CAs e TDD.
- Cada CA está associado a uma prova RED, GREEN ou REGRESSÃO dentro da SPEC correspondente.
- Nenhuma SPEC contém tasks; a decomposição pertence a `gerar-tasks`.

## Ordem recomendada de execução

1. SPEC-1-001 — acesso/papéis.
2. SPEC-1-002 — ciclo/obra-piloto.
3. SPEC-1-003 — importação/normalização.
4. SPEC-1-004 — consolidação semanal.
5. SPEC-1-005 — divergências/publicação.

## Pré-condições operacionais

- Cliente escolheu obra representativa e forneceu identificador canônico.
- Cliente entregou fixture real anonimizada e dicionário mínimo.
- Controller validou saldo inicial e semântica de realizado/comprometido.
- Credenciais da API do Sienge são desejáveis, mas não bloqueiam o caminho por upload.
- Usuários de teste e papéis foram definidos.

## Fora desta fase

API completa do Sienge como caminho obrigatório, conciliação avançada, DRE, expansão a todas as obras, projeção de 12 semanas, dashboards executivos, incorporadora/SPEs, IA e conciliação bancária.

## Tasks vinculadas

Serão criadas exclusivamente pela skill `gerar-tasks` após a revisão das SPECs. Até lá, esta seção permanece sem tasks por contrato.