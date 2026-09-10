# SPEC-1-005 — Divergências, revisão humana e publicação oficial

**Fase:** 1  
**Status:** planejada — aprovada para execução após pré-condições da Fase 1  
**Dono:** Controller/Controladoria  
**Origem no escopo:** RF-05, RF-06, RN-08, RN-10, RN-11, RN-13, CA-1.4, CA-1.5  
**Degrau da solução:** construção mínima — fila de exceções e publicação versionada preservam julgamento humano sem automatizar decisão financeira.

## Resultado observável

O controller encontra divergências em uma fila estruturada, decide ou justifica cada item e publica uma posição semanal versionada. A Diretoria vê somente a posição publicada; nenhum lançamento ambíguo entra silenciosamente no total definitivo.

## Limites e dependências

- **Inclui:** tipos de divergência, evidências, decisão/justificativa, responsável/data, status da fila, critérios de publicação e versionamento.
- **Fora de escopo:** classificação automática definitiva, IA, conciliação bancária, decisão de investimento e notificações externas.
- **Entradas/pré-condições:** posição em preparação da SPEC-1-004 e divergências geradas pelas SPECs anteriores.
- **Saídas:** itens resolvidos/justificados, posição publicada, versão e trilha de auditoria.
- **Dependências:** SPEC-1-001 e SPEC-1-004; controller e suplente devem validar o fluxo.
- **Risco/plano B:** divergência crítica não resolvida → posição permanece em preparação; exportação/consulta mostra o bloqueio.
- **Rollback:** cancelar publicação em preparação; publicação oficial não é apagada. Nova correção gera versão nova.

## Fluxo e regras

1. Sistema cria divergências para itens sem correspondência, sem regra ou com total conflitante.
2. Controller abre o item e consulta evidências de origem.
3. Controller resolve, justifica ou encaminha ao responsável da obra.
4. Sistema recalcula a posição em preparação.
5. Controller publica quando as condições de RN-11 estão satisfeitas.
6. Sistema registra versão, corte, responsável e composição.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | Divergência resolvida com evidência | Posição recalculada e pronta | — |
| Limite | Divergência não crítica justificada | Publicação registra justificativa | — |
| Falha | Divergência crítica pendente | Publicação bloqueada | Corrigir, justificar formalmente ou manter ciclo aberto |

## Checklist de execução

- [ ] Tipos de divergência e severidade homologados.
- [ ] Decisão e justificativa registram responsável/data/evidência.
- [ ] Recalculo após decisão demonstrado.
- [ ] Publicação e nova versão demonstradas.
- [ ] Acesso da Diretoria validado.

## Critérios de aceite

- [ ] **CA-1-019:** divergência sem correspondência aparece com origem e motivo.
- [ ] **CA-1-020:** decisão/justificativa exige responsável, data e evidência.
- [ ] **CA-1-021:** lançamento ambíguo não entra no total definitivo sem decisão.
- [ ] **CA-1-022:** posição recalcula após tratamento de divergência.
- [ ] **CA-1-023:** posição publicada tem corte, versão, responsável e composição.
- [ ] **CA-1-024:** publicação com divergência crítica pendente é bloqueada.
- [ ] **CA-1-025:** nova correção cria nova versão sem sobrescrever a publicada.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | Publicar posição com divergência crítica aberta | Fluxo de publicação | Sistema publica indevidamente antes da regra | Log/captura RED |
| GREEN | Resolver/justificar divergência e publicar | Fluxo controller | CA-1-019 a CA-1-024 passam | ID de decisão, versão e captura |
| REFACTOR/REGRESSÃO | Corrigir posição já publicada | Criar nova versão e tentar editar antiga | Antiga preservada; nova versionada; Diretoria vê válida | Comparação de versões |

**Dados/fixtures:** divergência sem correspondência, divergência crítica, item ambíguo e posição publicada.  
**Caminhos de erro obrigatórios:** evidência ausente, usuário não autorizado, decisão sem justificativa, publicação duplicada e tentativa de apagar versão oficial.  
**Evidência exigida:** fila, decisão, trilha de auditoria, versões e captura do acesso da Diretoria.

## Tasks vinculadas

<!-- Preencher somente por gerar-tasks após aprovação dos gates. -->

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
| | | | |