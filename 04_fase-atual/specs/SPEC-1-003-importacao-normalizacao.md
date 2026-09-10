# SPEC-1-003 — Importação governada e normalização de lançamentos

**Fase:** 1  
**Status:** planejada — aprovada para execução após pré-condições da Fase 1  
**Dono:** Dados/Integração  
**Origem no escopo:** RF-02, RF-03, D3, D10, CA-1.1, CA-1.2  
**Degrau da solução:** construção mínima — upload governado é o caminho funcional; API Sienge entra sem bloquear o primeiro valor.

## Resultado observável

Um relatório real da obra-piloto é importado, normalizado e convertido em lançamentos utilizáveis sem edição manual de células, preservando arquivo, linha, versão e data de importação.

## Limites e dependências

- **Inclui:** upload, validação de formato, idempotência mínima, normalização de datas/códigos/valores e proveniência.
- **Fora de escopo:** integração bancária, classificação definitiva para DRE, IA e transformação de layouts não observados.
- **Entradas/pré-condições:** fixture real anonimizada, dicionário, chaves e tamanho/encoding conhecidos; API Sienge é opcional nesta fase.
- **Saídas:** lote de importação, lançamentos normalizados, erros de linha e relatório de cobertura.
- **Dependências:** SPEC-1-002; amostras e G1; responsável do cliente para validar semântica.
- **Risco/plano B:** layout inesperado → quarentena do lote/linha e upload corrigido; não descartar silenciosamente.
- **Rollback:** invalidar lote em preparação e reprocessar nova versão; lotes publicados não são apagados.

## Fluxo e regras

1. Controller envia relatório associado ao ciclo.
2. Sistema valida tipo, tamanho, cabeçalho e período.
3. Sistema normaliza os campos previstos no dicionário.
4. Cada linha recebe origem e status.
5. Linhas inválidas ficam em quarentena com motivo.
6. Controller revisa resumo e confirma lote para consolidação.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | Fixture no layout aprovado | Lançamentos normalizados com origem | — |
| Limite | Campo opcional vazio | Linha segue com status permitido | Registrar ausência |
| Falha | Cabeçalho/layout incompatível | Lote rejeitado ou quarentenado | Exibir erro e permitir novo lote |

## Checklist de execução

- [ ] Fixture real anonimizada aprovada.
- [ ] Dicionário e chave de idempotência documentados.
- [ ] Lote importado e relatório de cobertura gerado.
- [ ] Linhas inválidas verificadas na quarentena.

## Critérios de aceite

- [ ] **CA-1-009:** fixture real é importada sem edição manual de célula.
- [ ] **CA-1-010:** cada lançamento preserva arquivo, linha, lote e data de importação.
- [ ] **CA-1-011:** reimportação do mesmo lote não duplica lançamentos.
- [ ] **CA-1-012:** linha inválida fica em quarentena com motivo verificável.
- [ ] **CA-1-013:** resumo informa total recebido, normalizado, quarentenado e rejeitado.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | Importar fixture sem parser/validação | Upload controlado | Dados não ficam normalizados ou duplicam | Log RED |
| GREEN | Importar fixture aprovada e repetir lote | Fluxo de upload | CA-1-009 a CA-1-011 passam | Lote, contagem e evidência |
| REFACTOR/REGRESSÃO | Alterar cabeçalho e inserir linha inválida | Upload de fixture adversarial | Quarentena e resumo corretos, sem regressão | Relatório de importação |

**Dados/fixtures:** relatório real anonimizado; cópia idêntica; cabeçalho alterado; linha com data/valor inválido.  
**Caminhos de erro obrigatórios:** arquivo vazio, tipo não suportado, duplicação, encoding inválido, coluna ausente e timeout.  
**Evidência exigida:** hash do arquivo, ID do lote, contagens e itens de quarentena.

## Tasks vinculadas

<!-- Preencher somente por gerar-tasks após aprovação dos gates. -->

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
| | | | |