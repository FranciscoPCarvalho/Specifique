# Evolução do Microframework SDD

## v0.2-r3 — proposta para revisão — 2026-10-27

- Carregamento progressivo de contexto para evitar leitura indiscriminada do acervo.
- Distinção entre **specs em aberto** e **spec corrente** da interação.
- Registro da **base da inspeção** no `plan.md`.
- Preflight obrigatório após aprovação e antes da primeira task da revisão.
- Resultados de preflight: `válido`, `desatualizado` ou `inconclusivo`.
- Transições de estado determinísticas, incluindo distinção formal entre
  `implementada` e `concluída`.
- Handoff multi-spec: destaca trabalho corrente e resume outros trabalhos em aberto.
- Roteiro de validação ampliado para testar contexto, preflight, concorrência de specs
  e transições de estado.

## v0.2-r2 — proposta para revisão — 2026-10-27

- Separação formal do ciclo em **inspeção → proposta → execução**.
- `spec.md` definida como fonte única de revisão, estado e aprovação.
- `plan.md` e `tasks.md` passam a referenciar a revisão vigente da spec.
- Distinção entre decisões pendentes bloqueantes e pressupostos explícitos.
- Separação entre documentos SDD efetivamente gerados e componentes previstos
  para alteração após aprovação.
- Critério para revisar uma spec ativa versus abrir uma nova spec.
- Definição de mudança material e invalidação da aprovação anterior.
- Aprovação em linguagem natural permitida quando inequívoca; aprovação com
  mudança material gera nova revisão em vez de iniciar execução.
- Handoff redefinido como representação do estado atual, não diário histórico.
- Roteiro de validação atualizado para testar esses comportamentos.

## v0.2 — proposta para revisão — 2026-10-26

- Intenção em linguagem natural para iniciar proposta, sem comando SDD explícito.
- Resumo executivo obrigatório com caminhos dos arquivos.
- Gate de aprovação vinculado à revisão vigente.
- Estados e controle de mudança; separação de QA e execução.
- Handoff conciso com referências e preservação de histórico nas migrações.
- Templates atualizados e protocolo/roteiro de validação adicionados.
