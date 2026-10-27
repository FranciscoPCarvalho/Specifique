# Guia para revisar e adotar a proposta v0.2-r3

Esta distribuição é uma proposta para revisão, gerada em cópia separada. Não
substitua indiscriminadamente uma árvore SDD já em uso.

## Principais mudanças da r3

- separação formal entre **inspeção → proposta → execução**;
- `spec.md` passa a ser a fonte única de revisão, estado e aprovação;
- `plan.md` e `tasks.md` referenciam a revisão da spec;
- distinção entre **decisão pendente** e **pressuposto**;
- distinção entre documentos efetivamente gerados e arquivos previstos para
  alteração após aprovação;
- critérios explícitos para revisar uma spec existente ou abrir nova spec;
- definição objetiva de mudança material;
- handoff atualizado como estado corrente, sem diário cronológico crescente;
- carregamento progressivo de contexto;
- distinção entre specs em aberto e spec corrente;
- preflight após aprovação e antes da primeira task;
- transições de estado determinísticas;
- handoff capaz de resumir múltiplas specs em aberto.

## Procedimento controlado

1. Faça backup/commit do SDD existente e compare os arquivos compartilhados.
2. Atualize primeiro `docs/protocolo-operacional.md` e o bloco SDD da aplicação.
3. Não sobrescreva automaticamente templates locais personalizados. Migre-os
   explicitamente por projeto para o modelo em que `spec.md` é a autoridade.
4. Preserve specs e handoffs históricos; não invente revisões/aprovações
   retroativas.
5. Teste primeiro em uma cópia de um projeto existente e organizado usando `docs/roteiro-validacao.md`.
6. Depois valide também um projeto legado e um projeto desorganizado, cobrindo os demais cenários do roteiro.
7. Somente após os testes registre resultados reais por agente/IDE e considere
   congelar uma versão pública.

## Compatibilidade

- Este pacote contém a base compartilhada; não migra automaticamente os
  projetos históricos.
- O comportamento depende de como cada agente carrega `AGENTS.md` e expõe
  links de arquivos.
- A r3 é conceitualmente compatível com o acervo anterior, mas muda a fonte de
  verdade da aprovação: em novos artefatos, ela fica apenas em `spec.md`.
