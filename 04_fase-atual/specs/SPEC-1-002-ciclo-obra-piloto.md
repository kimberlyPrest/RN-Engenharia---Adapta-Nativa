# SPEC-1-002 — Obra-piloto e ciclo de atualização financeira

**Fase:** 1  
**Status:** planejada — aprovada para execução após pré-condições da Fase 1  
**Dono:** Controller/Operação  
**Origem no escopo:** RF-01, Fase 1, G1, D4  
**Degrau da solução:** construção mínima — configura somente uma obra representativa e um ciclo semanal demonstrável.

## Resultado observável

A RN consegue selecionar a obra-piloto, o período e a visão financeira do ciclo e iniciar uma atualização identificável, sem misturar obras ou períodos.

## Limites e dependências

- **Inclui:** cadastro/seleção da obra-piloto, período, data de corte e tipo de visão (realizado/comprometido); validação de escopo.
- **Fora de escopo:** todas as obras, projeção de 12 semanas, incorporadora/SPEs e regras de venda.
- **Entradas/pré-condições:** lista e identificador canônico da obra, período de corte, responsável e amostras reais.
- **Saídas:** ciclo criado com ID, obra, período, data de corte e status.
- **Dependências:** cliente escolhe a obra no G1; SPEC-1-001 para acesso.
- **Risco/plano B:** identificador do ERP inconsistente → bloquear o ciclo e enviar para divergência, nunca inferir a obra.
- **Rollback:** cancelar ciclo em preparação; ciclos publicados permanecem preservados.

## Fluxo e regras

1. Controller seleciona a obra-piloto e informa o corte.
2. Sistema valida se obra e período estão completos.
3. Controller escolhe realizado, comprometido ou ambos.
4. Sistema cria ciclo em preparação.
5. Ciclo recebe status e fica pronto para importação.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | Obra e corte válidos | Ciclo criado | — |
| Limite | Obra sem identificador canônico | Ciclo não inicia | Solicitar homologação do cadastro |
| Falha | Período final anterior ao inicial | Validação impede criação | Corrigir datas |

## Checklist de execução

- [ ] Obra-piloto escolhida e identificador documentado.
- [ ] Data de corte homologada.
- [ ] Ciclo criado em preparação.
- [ ] Visão escolhida e evidência anexada.

## Critérios de aceite

- [ ] **CA-1-005:** ciclo identifica obra, período, corte e responsável.
- [ ] **CA-1-006:** ciclo não é criado com obra ou período inválido.
- [ ] **CA-1-007:** ciclo permite selecionar realizado e/ou comprometido.
- [ ] **CA-1-008:** ciclo em preparação não aparece para Diretoria.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | Criar ciclo sem obra/corte | Fluxo manual | Sistema aceita dados incompletos antes da validação | Captura RED |
| GREEN | Criar ciclo válido | Informar obra, corte e visão | Ciclo criado corretamente | ID e captura |
| REFACTOR/REGRESSÃO | Datas invertidas e obra desconhecida | Repetir validações | Criação bloqueada sem vazamento de dados | Log/captura |

**Dados/fixtures:** uma obra-piloto real, uma obra inexistente, períodos válido e inválido.  
**Caminhos de erro obrigatórios:** campos vazios, obra desconhecida, corte inválido e duplicação do mesmo ciclo.  
**Evidência exigida:** ID do ciclo, captura do formulário e registro de validação.

## Tasks vinculadas

<!-- Preencher somente por gerar-tasks após aprovação dos gates. -->

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
| | | | |