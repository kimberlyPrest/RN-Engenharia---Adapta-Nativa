# SPEC-1-001 — Acesso, papéis e posição em preparação/publicada

**Fase:** 1  
**Status:** planejada — aprovada para execução após pré-condições da Fase 1  
**Dono:** Produto/Segurança  
**Origem no escopo:** RF-06, D7, CA-1.5, CA-1.6  
**Degrau da solução:** construção mínima — autenticação e autorização mínimas para separar preparação de posição oficial.

## Resultado observável

Usuários autenticados acessam apenas as funções compatíveis com seu papel; a Diretoria consegue consultar posições publicadas, mas não posições em preparação. Uma posição publicada não pode ser sobrescrita silenciosamente.

## Limites e dependências

- **Inclui:** login; papéis controller, analista e diretoria; estados preparação/publicada; bloqueio de edição após publicação; registro de versão.
- **Fora de escopo:** SSO, recuperação avançada, gestão organizacional complexa, permissões por campo e integração com diretórios corporativos.
- **Entradas/pré-condições:** usuários de teste e decisão do cliente sobre quem ocupará cada papel.
- **Saídas:** sessão autenticada, matriz de acesso, posição versionada e evidência de bloqueio.
- **Dependências:** SPEC-1-002 e SPEC-1-005; dono RN para validar usuários.
- **Risco/plano B:** se identidade corporativa não estiver disponível, usar contas locais de teste; não usar conta compartilhada em produção.
- **Rollback:** desativar usuário de teste e descartar posição de homologação; nunca apagar uma posição oficial.

## Fluxo e regras

1. Usuário faz login e recebe o papel atribuído.
2. Controller/analista cria ou consulta posição em preparação.
3. Controller publica após os critérios da SPEC-1-005.
4. Diretoria consulta apenas posições publicadas.
5. Nova correção gera nova versão, preservando a anterior.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | Diretoria acessa posição publicada | Consulta permitida | — |
| Limite | Diretoria tenta abrir posição em preparação | Acesso negado ou item invisível | Registrar tentativa sem revelar dados |
| Falha | Usuário sem papel tenta publicar | Publicação bloqueada | Controller assume ou atribui papel formalmente |

## Checklist de execução

- [ ] Usuários e papéis homologados.
- [ ] Estados de posição implementados.
- [ ] Bloqueio de sobrescrita demonstrado.
- [ ] Evidências anexadas.

## Critérios de aceite

- [ ] **CA-1-001:** usuário autenticado vê somente funções compatíveis com seu papel.
- [ ] **CA-1-002:** diretoria não acessa posição em preparação.
- [ ] **CA-1-003:** posição publicada não pode ser editada; correção cria nova versão.
- [ ] **CA-1-004:** tentativa de publicação por papel não autorizado é bloqueada e registrada.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | Usuário diretoria tenta acessar preparação | Fluxo manual com posição em preparação | Acesso indevidamente permitido antes da regra | Captura/log RED |
| GREEN | Repetir com autorização aplicada | Login + acesso aos dois estados | CA-1-001/002 passam | Captura e log |
| REFACTOR/REGRESSÃO | Tentar editar posição publicada e publicar com analista | Fluxo manual | Sobrescrita e publicação indevidas bloqueadas | Relatório de regressão |

**Dados/fixtures:** três usuários de teste, uma posição em preparação e uma publicada.  
**Caminhos de erro obrigatórios:** senha inválida, papel ausente, acesso direto à URL e edição pós-publicação.  
**Evidência exigida:** capturas, logs de autorização e ID das posições.

## Tasks vinculadas

<!-- Preencher somente por gerar-tasks após aprovação dos gates. -->

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
| | | | |