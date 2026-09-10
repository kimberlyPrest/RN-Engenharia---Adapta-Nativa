# Fase 1 — Fundação e prova em 1 obra

**Objetivo:** provar o ciclo completo de consolidação semanal em UMA obra representativa da construtora, com posição oficial publicada pelo sistema.
**Entrega palpável:** posição semanal oficial da obra-piloto (realizado + comprometido, saldo, necessidade de caixa, data de corte) publicada e rastreável — sem limpeza manual de planilhas.
**Sequência ASA:** automação determinística nas etapas repetíveis; decisão humana nas divergências; sem IA.

## Escopo da fase

1. Ambiente e acessos: aplicação com login e papéis (controller, analista, diretoria leitura); backup mínimo.
2. Importação padronizada: upload governado dos relatórios do Sienge da obra-piloto; API não bloqueia a fase.
3. Base única de lançamentos com origem rastreável.
4. Consolidação semanal de realizado e comprometido: entradas, saídas, saldo acumulado, necessidade de caixa.
5. Fila de divergências com decisão, justificativa e responsável.
6. Publicação da posição oficial com data de corte e versionamento.
7. Medição do baseline.

## Pré-requisitos (gate G1)

Amostras reais anonimizadas, dicionário, chaves, obra-piloto, saldo inicial, semântica de realizado/comprometido, papéis e suplente. Credenciais da API do Sienge são desejáveis, mas upload é fallback.

## Fora desta fase

Conciliações, classificação DRE, múltiplas obras, projeção 12 semanas, dashboards executivos, incorporadora/SPEs, IA e conciliação bancária.

## Tasks

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| T1.1 | Preparar fixture, configuração e caminho principal | Produto/Segurança | SPEC-1-001 | CA-1-001; CA-1-002 | RED/GREEN acesso | fixture + logs | dados e gate | ☐ |
| T1.2 | Bordas e prova final | Produto/Segurança | SPEC-1-001 | CA-1-003; CA-1-004 | regressão | relatório | T1.1 | ☐ |
| T2.1 | Preparar ciclo da obra | Controller/Operação | SPEC-1-002 | CA-1-005; CA-1-006 | RED/GREEN ciclo | ID/captura | obra/corte | ☐ |
| T2.2 | Bordas do ciclo | Controller/Operação | SPEC-1-002 | CA-1-007; CA-1-008 | regressão | relatório | T2.1 | ☐ |
| T3.1 | Preparar importação | Dados/Integração | SPEC-1-003 | CA-1-009; CA-1-010 | fixture/proveniência | lote/log | dicionário | ☐ |
| T3.2 | Idempotência/quarentena | Dados/Integração | SPEC-1-003 | CA-1-011..013 | bordas | relatório | T3.1 | ☐ |
| T4.1 | Consolidação principal | Controladoria/Dados | SPEC-1-004 | CA-1-014; CA-1-015 | cálculo | snapshot/oráculo | lote/saldo | ☐ |
| T4.2 | Oráculo/regressão | Controladoria/Dados | SPEC-1-004 | CA-1-016..018 | regressão | relatório | T4.1 | ☐ |
| T5.1 | Divergência/decisão | Controller/Controladoria | SPEC-1-005 | CA-1-019..021 | RED/GREEN | decisão/log | posição | ☐ |
| T5.2 | Publicação/versionamento | Controller/Controladoria | SPEC-1-005 | CA-1-022..025 | bloqueio/versão | auditoria | T5.1 | ☐ |

## Critérios de aceite da fase

Upload sem edição; origem por lançamento; consolidação correta; divergência tratável; publicação imutável; diretoria só vê publicado; baseline registrado; fallback sem API.