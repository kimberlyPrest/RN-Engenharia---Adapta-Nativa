# Revisão documental das SPECs — Fase 1 RN Engenharia

**Modo:** revisão estrutural do pacote gerado; aprovação do cliente informada pela consultora em 2026-09-10.
**Veredito:** APROVADA PARA DECOMPOSIÇÃO EM TASKS, com pré-condições operacionais explícitas; não iniciar implementação antes de `gerar-tasks` e da homologação dos dados reais.

## Coerência

- 5 SPECs cobrem a fatia vertical: acesso → ciclo → importação → consolidação → divergências/publicação.
- 25 critérios de aceite são binários e apontam para uma prova dentro da própria SPEC.
- A entrega palpável da Fase 1 é preservada: posição semanal de uma obra, publicada e rastreável.
- Projeção de 12 semanas, DRE, todas as obras e dashboards permanecem fora desta onda.

## Viabilidade

- Upload governado permite demonstrar valor sem depender da API do Sienge.
- A obra-piloto, fixture real e saldo inicial continuam pré-condições críticas.
- O oráculo independente da SPEC-1-004 reduz risco de cálculo incorreto.

## Risco/segurança

1. Política de papéis, retenção, backup e contas reais ainda precisa ser homologada; usar apenas fixtures anonimizadas antes do gate.
2. Upload precisa de limite de tamanho/tipo, validação de conteúdo, quarentena e não duplicação.
3. Logs de origem e decisões podem conter dados financeiros; definir acesso e retenção antes da implementação.
4. Publicação imutável precisa ser garantida no servidor, não apenas na interface.

## Pendências operacionais antes das tasks

- Escolher obra-piloto e fornecer amostra real anonimizada.
- Homologar semântica de realizado/comprometido, saldo inicial e divergência crítica.
- Definir papéis, suplente e retenção mínima.
- A aprovação do cliente não substitui a evidência técnica: API, ambiente, limites de upload, validação no servidor, logs e backup serão confirmados na decomposição/execução.

## Próximo passo

Executar `gerar-tasks` para decompor as 5 SPECs em tasks independentes, com levas, donos e provas. Não implementar antes dessa decomposição.