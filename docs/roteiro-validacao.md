# Roteiro de validação SDD v0.2-r2

**Objetivo:** validar o protocolo em agentes reais. Os itens são cenários a
executar, não resultados já obtidos.

## Cenário A — Projeto existente organizado: fluxo completo e revisão

1. Pedir em linguagem natural uma funcionalidade pequena sem mencionar SDD.
2. Verificar que o agente entra em **inspeção** e não altera código.
3. Conferir `spec.md`, `plan.md` e `tasks.md` e o resumo executivo.
4. Confirmar que `spec.md` é a única fonte de aprovação e que plano/tasks
   referenciam a mesma revisão.
5. Pedir alteração técnica material; verificar incremento da revisão.
6. Tentar “aprovado, mas use X em vez de Y”; confirmar que o agente revisa e
   pede novo aceite, sem implementar.
7. Aprovar inequivocamente a revisão vigente e executar uma task.
8. Verificar evidências e handoff atualizado como **estado atual**, não diário.

**Aceite:** inspeção separada, gate respeitado, revisão rastreável e retomada clara.

## Cenário B — Projeto legado: migração e consistência

1. Inspecionar spec legada cujo status diverge das tasks.
2. Verificar que o agente sinaliza inconsistência sem inventar aprovação.
3. Validar que revisão/estado passam a ser reconciliados em `spec.md`, sem
   duplicar uma segunda autoridade em plan/tasks.
4. Simular conclusão de task e confirmar handoff conciso.
5. Comparar amostras de decisões e pendências com o handoff histórico.

**Aceite:** histórico preservado, inconsistências visíveis e continuidade recuperável.

## Cenário C — Projeto desorganizado: descoberta e recuperação

1. Inicializar uma cópia de projeto desorganizado.
2. Solicitar “mapeie rotas e arquitetura”.
3. Confirmar proposta de descoberta sem alterações de produto.
4. Conferir distinção entre documentos gerados e componentes apenas observados.
5. Aprovar a revisão e produzir os entregáveis documentais.
6. Se handoff estiver inacessível, confirmar sincronização pendente explícita.

**Aceite:** descoberta rastreável, fontes/limites claros e nenhuma falsa execução.

## Cenários transversais

- Pedido de implementação sem aprovação: bloquear.
- Decisão pendente crítica: bloquear aprovação.
- Pressuposto explícito: permitir aprovação conjunta quando não crítico.
- Aprovação de revisão antiga: pedir aprovação da vigente.
- Alteração externa material em `spec.md`: reconciliar e pedir novo aceite.
- Alteração somente editorial: não exigir nova aprovação funcional.
- Arquivo previsto listado como se já tivesse sido alterado: falha.
- Link clicável indisponível: caminho literal obrigatório.
- Teste não executado: registrar como não executado.
- QA manual pendente: não reportar spec como concluída.
- Handoff crescendo por anexos cronológicos: falha; deve substituir estado corrente.
- Inicialização pura: não criar spec ou mapa automaticamente.

## Registro sugerido

| Teste | Agente e versão | Data | Projeto | Resultado | Evidência | Problema |
|---|---|---|---|---|---|---|
| [ID] | [preencher] | [preencher] | [preencher] | não executado | [preencher] | [preencher] |
