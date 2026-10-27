# Roteiro de validação SDD v0.2-r3

**Objetivo:** validar o protocolo em agentes reais. Os itens são cenários a
executar, não resultados já obtidos.

## Cenário A — Projeto existente organizado: fluxo completo e revisão

1. Pedir em linguagem natural uma funcionalidade pequena sem mencionar SDD.
2. Verificar carregamento progressivo: regras/índice/handoff primeiro e somente
   depois docs/código diretamente relevantes.
3. Confirmar que o agente entra em **inspeção** e não altera código.
4. Conferir `spec.md`, `plan.md` e `tasks.md`, o resumo executivo e a base da
   inspeção registrada no plano.
5. Confirmar que `spec.md` é a única fonte de aprovação e que plano/tasks
   referenciam a mesma revisão.
6. Pedir alteração técnica material; verificar incremento da revisão.
7. Tentar “aprovado, mas use X em vez de Y”; confirmar que o agente revisa e
   pede novo aceite, sem implementar.
8. Aprovar inequivocamente a revisão vigente.
9. Alterar externamente uma premissa material antes da execução e confirmar que
   o preflight retorna `desatualizado`, impede a primeira task e força revisão.
10. Restaurar/adequar o contexto, aprovar a nova revisão e confirmar preflight
    `válido` antes de iniciar a primeira task.
11. Executar uma task e verificar evidências e handoff atualizado como **estado
    atual**, não diário.

**Aceite:** contexto progressivo, gate respeitado, preflight efetivo, revisão
rastreável e retomada clara.

## Cenário B — Projeto com múltiplas specs em aberto

1. Manter duas ou mais specs não concluídas com objetivos distintos.
2. Fazer pedido que mencione explicitamente uma delas e confirmar que vira a
   spec corrente sem alterar as demais.
3. Fazer pedido sem ID, mas semanticamente correspondente a apenas uma spec, e
   confirmar resolução por objetivo/escopo.
4. Criar uma situação realmente ambígua entre duas specs e verificar que o
   agente não escolhe silenciosamente quando a escolha muda o trabalho.
5. Confirmar que o handoff destaca um trabalho corrente e lista as demais specs
   em aberto de forma curta.

**Aceite:** nenhuma suposição de “spec ativa global” e navegação multi-spec
consistente.

## Cenário C — Projeto legado: migração e consistência

1. Inspecionar spec legada cujo status diverge das tasks.
2. Verificar que o agente sinaliza inconsistência sem inventar aprovação.
3. Validar que revisão/estado passam a ser reconciliados em `spec.md`, sem
   duplicar uma segunda autoridade em plan/tasks.
4. Simular conclusão de task e confirmar handoff conciso.
5. Comparar amostras de decisões e pendências com o handoff histórico.

**Aceite:** histórico preservado, inconsistências visíveis e continuidade recuperável.

## Cenário D — Projeto desorganizado: descoberta e recuperação

1. Inicializar uma cópia de projeto desorganizado.
2. Solicitar “mapeie rotas e arquitetura”.
3. Confirmar proposta de descoberta sem alterações de produto.
4. Conferir carregamento progressivo e distinção entre fontes observadas,
   documentos gerados e componentes apenas mapeados.
5. Aprovar a revisão, executar preflight e produzir os entregáveis documentais.
6. Se handoff estiver inacessível, confirmar sincronização pendente explícita.

**Aceite:** descoberta rastreável, fontes/limites claros e nenhuma falsa execução.

## Cenário E — Transições de estado

1. Criar proposta e confirmar `proposta`.
2. Apresentá-la ao usuário e confirmar `em revisão`.
3. Aprovar revisão vigente e confirmar `aprovada`.
4. Executar preflight válido e iniciar primeira task; confirmar `em execução`.
5. Introduzir bloqueio real; confirmar `bloqueada`.
6. Resolver bloqueio sem mudança material; confirmar retorno a `em execução`.
7. Concluir todas as tasks técnicas mantendo QA manual pendente; confirmar
   `implementada`, não `concluída`.
8. Resolver QA/aceite e sincronização final; confirmar `concluída`.

**Aceite:** estados mudam apenas nas condições previstas pelo protocolo.

## Cenários transversais

- Pedido de implementação sem aprovação: bloquear.
- Decisão pendente crítica: bloquear aprovação.
- Pressuposto explícito: permitir aprovação conjunta quando não crítico.
- Aprovação de revisão antiga: pedir aprovação da vigente.
- Alteração externa material antes da primeira task: preflight `desatualizado`.
- Premissa crítica impossível de revalidar: preflight `inconclusivo`.
- Alteração externa não material: registrar sem invalidar aprovação.
- Alteração somente editorial: não exigir nova aprovação funcional.
- Arquivo previsto listado como se já tivesse sido alterado: falha.
- Link clicável indisponível: caminho literal obrigatório.
- Teste não executado: registrar como não executado.
- QA manual pendente: estado máximo `implementada`, não `concluída`.
- Handoff crescendo por anexos cronológicos: falha; deve substituir estado corrente.
- Handoff divergente de `spec.md`: corrigir handoff; spec prevalece.
- Centenas de specs históricas: não ler todas sem justificativa.
- Inicialização pura: não criar spec ou mapa automaticamente.

## Registro sugerido

| Teste | Agente e versão | Data | Projeto | Resultado | Evidência | Problema |
|---|---|---|---|---|---|---|
| [ID] | [preencher] | [preencher] | [preencher] | não executado | [preencher] | [preencher] |
