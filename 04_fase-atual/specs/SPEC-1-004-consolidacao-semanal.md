# SPEC-1-004 — Consolidação semanal de realizado e comprometido

**Fase:** 1  
**Status:** planejada — aprovada para execução após pré-condições da Fase 1  
**Dono:** Controladoria/Dados  
**Origem no escopo:** RF-04, RN-01, RN-02, RN-07, CA-1.3, D2  
**Degrau da solução:** construção mínima — cálculos determinísticos sobre lançamentos normalizados, sem IA.

## Resultado observável

Para a obra-piloto, o sistema calcula a posição semanal de entradas, saídas, saldo acumulado e necessidade de caixa, separando realizado de comprometido e permitindo rastrear cada total aos lançamentos de origem.

## Limites e dependências

- **Inclui:** agregação por data/obra, realizado e comprometido, saldo acumulado, necessidade de caixa e detalhamento do total.
- **Fora de escopo:** projeção oficial de 12 semanas, DRE consolidada, todas as obras e recomendação de investimento.
- **Entradas/pré-condições:** ciclo válido e lote aprovado da SPEC-1-003; saldo inicial definido para a obra.
- **Saídas:** posição semanal em preparação, totais por categoria e detalhamento rastreável.
- **Dependências:** SPEC-1-002 e SPEC-1-003; Jefferson valida semântica de comprometido e saldo inicial.
- **Risco/plano B:** sem saldo inicial confiável → exibir posição como incompleta, não publicar disponibilidade de caixa.
- **Rollback:** recalcular a versão em preparação; publicação anterior permanece imutável.

## Fluxo e regras

1. Sistema recebe lote confirmado.
2. Separa realizado e comprometido conforme classificação de origem.
3. Agrega entradas e saídas por data e obra.
4. Calcula saldo acumulado a partir do saldo inicial aprovado.
5. Exibe necessidade de caixa e permite abrir a composição.
6. Envia inconsistências para SPEC-1-005.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | Lançamentos válidos e saldo inicial | Totais semanais calculados | — |
| Limite | Semana sem movimento | Semana aparece com zero e status coberto | Não inferir dado ausente |
| Falha | Lançamento sem sinal de entrada/saída | Total não fecha e item vai à divergência | Bloquear publicação até decisão |

## Checklist de execução

- [ ] Saldo inicial e semântica de comprometido homologados.
- [ ] Cálculo realizado/comprometido executado.
- [ ] Composição dos totais acessível.
- [ ] Caso de lançamento sem classificação testado.

## Critérios de aceite

- [ ] **CA-1-014:** entradas e saídas semanais batem com os lançamentos da obra-piloto.
- [ ] **CA-1-015:** realizado e comprometido aparecem separados.
- [ ] **CA-1-016:** saldo acumulado usa saldo inicial documentado e fórmula auditável.
- [ ] **CA-1-017:** cada total abre sua composição de lançamentos.
- [ ] **CA-1-018:** item sem sinal financeiro impede posição definitiva e aparece na fila.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | Calcular com fixture sem separação realizado/comprometido | Executar ciclo | Total mistura categorias ou aceita item inválido | Snapshot RED |
| GREEN | Executar fixture aprovada | Rodar consolidação | Totais e saldo batem com oráculo calculado | Snapshot + cálculo oráculo |
| REFACTOR/REGRESSÃO | Incluir semana vazia e lançamento ambíguo | Reexecutar | Zero explícito e divergência sem publicação | Relatório de regressão |

**Dados/fixtures:** massa mínima com duas semanas, entradas, saídas, realizado, comprometido, saldo inicial e item ambíguo.  
**Caminhos de erro obrigatórios:** saldo ausente, valor negativo, duplicidade, semana sem dados e item sem natureza.  
**Evidência exigida:** snapshot da posição, planilha/oráculo independente e composição por lançamento.

## Tasks vinculadas

<!-- Preencher somente por gerar-tasks após aprovação dos gates. -->

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
| | | | |