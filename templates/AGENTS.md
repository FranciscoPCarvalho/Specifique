<!-- SDD:BEGIN -->
## Documentação e fluxo SDD

Projeto SDD: `{{PROJECT_ID}}`.
A partir da pasta que contém este `AGENTS.md`, a raiz SDD está em
`{{SDD_ROOT_PATH}}` e a base deste projeto em `{{SDD_PROJECT_PATH}}`.
Resolva os caminhos a partir deste arquivo, ainda que o terminal esteja em
subpasta. Não dependa de Git nem de caminhos absolutos de outra máquina.

Consulte o [índice SDD]({{SDD_INDEX_LINK}}), a
[documentação]({{SDD_DOCS_LINK}}), as [specs]({{SDD_SPECS_LINK}}) e os
[templates]({{SDD_TEMPLATES_LINK}}), além do protocolo compartilhado em
`{{SDD_ROOT_PATH}}/docs/protocolo-operacional.md`. Leia as regras locais da
aplicação, a spec, o plano e as tarefas relevantes antes de trabalhar.
Se a base estiver ausente/inacessível, informe qual vínculo falhou; não
invente documentação, não procure nem clone outros repositórios. Para
restaurar, abra o SDD e solicite reinicialização informando a aplicação.

### Detectar intenção e preparar proposta

Não espere pelo comando “crie uma spec”. Mudanças funcionais, correções com
impacto de comportamento e refatorações significativas, mesmo solicitadas em
linguagem natural, acionam preparação de spec, plano e tarefas **antes da
implementação**. Mapeamentos de arquitetura/rotas são specs de descoberta
quando o usuário solicita tal entrega; sua execução investigativa também passa
por aprovação do plano quando se propuser uma spec. Perguntas, leitura de
código e explicações não exigem uma spec. Não crie uma nova spec se a solicitação
pertencer claramente a uma spec ativa: proponha uma revisão nela, preservando
histórico e rastreabilidade. Corrigir apenas formatação documental não implica
mudança funcional; mantenha aprovações locais aplicáveis.

1. Entenda a demanda, consulte a documentação e inspecione estaticamente o
   código pertinente; não altere implementação, execute a aplicação, instale
   dependências nem faça migrações antes da autorização pertinente. Separe
   fatos observados, hipóteses e propostas. Pergunte apenas o que impedir
   delimitação segura do escopo; dúvidas importantes também podem constar da
   proposta, que permanecerá bloqueada para aprovação até serem resolvidas.
2. Leia os templates do projeto; calcule o próximo ID pelo maior prefixo
   numérico das pastas em `specs/`, mais um (iniciando em `0001`). Preserve
   IDs legados, não reutilize lacunas/IDs arquivados. Use no mínimo quatro
   dígitos e slug minúsculo com hífens. Reconfira colisões antes de escrever.
3. Crie `specs/NNNN-slug/spec.md`, `plan.md` e `tasks.md` com base nos
   templates locais, substituindo `{{SPEC_ID}}`, `{{SPEC_TITLE}}`, `{{DATE}}`
   e o identificador do projeto. Preencha a proposta conforme as evidências
   disponíveis. Classifique a spec (funcionalidade, correção, refatoração,
   descoberta ou migração documental) e use “não aplicável” com justificativa.
4. Registre a spec no índice do projeto sem duplicação. Apresente
   **automaticamente** no chat o resumo executivo: ID/título/status/revisão,
   objetivo, requisitos/regras, plano técnico, impactos, critérios de aceite,
   riscos e decisões pendentes, arquivos criados/alterados e próxima ação.
   Referencie `spec.md`, `plan.md` e `tasks.md` com caminhos reais, links
   navegáveis quando suportados e caminhos literais em todos os casos.
   Não invente links nem afirme que o editor os abrirá sem suporte.
5. Solicite revisão e aprovação **explícita** da revisão atual. Se o usuário
   pedir alterações, atualize os artefatos pertinentes, incremente a revisão,
   apresente diferenças relevantes e peça nova aprovação. Nenhuma criação de
   documento significa aprovação ou início da implementação.

### Aprovação, implementação e controle de mudança

Estados de spec: `proposta` → `em revisão` → `aprovada` → `em execução` →
`implementada` → `concluída`; `bloqueada` e `cancelada` são alternativas
justificadas, conforme o protocolo central. Somente uma revisão aprovada da
spec, plano **e** tarefas autoriza a execução correspondente. Registre
revisão, aprovador/manifestação e data quando conhecidos; sem evidência, deixe
como pendente. Documentação histórica não vale como aprovação da demanda atual.

Execute uma task por vez, seguindo dependências, e registre evidências,
comandos/testes e resultados. Diferencie implementação técnica, testes
automatizados e QA manual. QA manual requer confirmação explícita ou indicação
justificada de “não aplicável”. Não declare testes, deploy, commit ou aprovação
sem prova. Mudanças materiais de escopo, requisitos, dados, segurança ou
arquitetura exigem nova revisão da proposta e autorização antes de seguir na
parte afetada. Uma spec de descoberta não autoriza alterar o produto.

### Sincronização e handoff

Ao concluir tecnicamente cada task: atualize `tasks.md` com resultado e
referências; confira consistência entre requisitos, plano e tarefas; registre
desvios para revisão em vez de mudar a spec silenciosamente; atualize handoff
da aplicação (`handoff.md`, `HANDOFF.md` ou nome adotado) com **estado atual**,
**próxima ação**, **impedimentos** e **referências** para detalhes. Ao concluir
uma spec, consolide a situação e pendências; mantenha QA manual pendente
visível, inclusive se a implementação técnica estiver pronta. Não transforme
o handoff em diário de milhares de linhas: registros longos ficam nas tasks ou
nos docs temáticos, com links.

Preserve instruções e fatos existentes. Migração/compactação de handoff exige
preservar o histórico original antes de resumir e conferir que informações
relevantes continuam recuperáveis. Se não houver handoff, crie um Markdown
curto na raiz da aplicação e registre seu caminho no índice e nas tasks. Se o
checkout/arquivo não estiver disponível, registre a limitação e mantenha a
sincronização como pendente, sem alegar conclusão documental total.
<!-- SDD:END -->
