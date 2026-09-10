# Tasks — Fase 1 RN Engenharia

**Status:** planejadas; 10 tasks sincronizadas com a Fase 1 e suas 5 SPECs.

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| T1.1 | Preparar fixture, configuração e caminho principal | Produto/Segurança | SPEC-1-001 | CA-1-001; CA-1-002 | RED/GREEN de acesso e papéis | fixture, logs e captura | dados de teste e gate operacional | ☐ |
| T1.2 | Executar bordas, recuperação e prova final | Produto/Segurança | SPEC-1-001 | CA-1-003; CA-1-004 | regressão de publicação e acesso | relatório de regressão | T1.1 concluída | ☐ |
| T2.1 | Preparar fixture, configuração e caminho principal | Controller/Operação | SPEC-1-002 | CA-1-005; CA-1-006 | RED/GREEN do ciclo | ID do ciclo e captura | obra/corte homologados | ☐ |
| T2.2 | Executar bordas, recuperação e prova final | Controller/Operação | SPEC-1-002 | CA-1-007; CA-1-008 | regressão de validações e visibilidade | logs/capturas | T2.1 concluída | ☐ |
| T3.1 | Preparar fixture, configuração e caminho principal | Dados/Integração | SPEC-1-003 | CA-1-009; CA-1-010 | RED/GREEN de importação e proveniência | fixture, lote e logs | dicionário e fixture | ☐ |
| T3.2 | Executar bordas, recuperação e prova final | Dados/Integração | SPEC-1-003 | CA-1-011..013 | idempotência, quarentena e resumo | relatório de importação | T3.1 concluída | ☐ |
| T4.1 | Preparar fixture, configuração e caminho principal | Controladoria/Dados | SPEC-1-004 | CA-1-014; CA-1-015 | cálculo principal | snapshot e oráculo | lote e saldo inicial | ☐ |
| T4.2 | Executar bordas, recuperação e prova final | Controladoria/Dados | SPEC-1-004 | CA-1-016..018 | fórmula, composição e regressão | relatório e oráculo | T4.1 concluída | ☐ |
| T5.1 | Preparar fixture, configuração e caminho principal | Controller/Controladoria | SPEC-1-005 | CA-1-019..021 | RED/GREEN de divergência e decisão | fila, decisão e logs | posição em preparação | ☐ |
| T5.2 | Executar bordas, recuperação e prova final | Controller/Controladoria | SPEC-1-005 | CA-1-022..025 | bloqueio, publicação e versionamento | auditoria e versões | T5.1 concluída | ☐ |

## Regra

Cada task aponta para uma única SPEC, possui critério binário, prova, evidência, pré-condições e status. Nenhuma task está marcada como concluída.