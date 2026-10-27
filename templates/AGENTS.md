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
`{{SDD_ROOT_PATH}}/docs/protocolo-operacional.md`. Leia também as regras locais
da aplicação. Em conflito, aplique a orientação mais restritiva e torne a
divergência explícita.

Se a base SDD estiver ausente/inacessível, informe qual vínculo falhou; não
invente documentação nem clone outro repositório para substituí-la.

### 1. Detectar intenção

Não espere pelo comando “crie uma spec”. Mudanças funcionais, correções de
comportamento e refatorações relevantes acionam o fluxo SDD. Mapeamentos de
arquitetura/rotas podem ser specs de descoberta. Perguntas, explicações e
leitura sem alteração não exigem spec.

Se a demanda continua perseguindo o mesmo objetivo de uma spec ativa, proponha
revisão dessa spec. Abra nova spec quando houver novo objetivo, workflow ou
conjunto independente de critérios de aceite.

### 2. Inspecionar antes de propor

Na fase de inspeção, leia apenas o necessário para compreender contexto,
regras, arquitetura e impacto. Diferencie fatos observados, informação do
usuário, hipóteses e propostas.

Antes da aprovação, não altere código da aplicação, instale dependências,
execute migrações, modifique dados, faça deploy ou execute operações destrutivas.
Execução de aplicação/testes prévia só é permitida quando as regras locais a
autorizarem explicitamente e ela for necessária para fundamentar a proposta.

### 3. Preparar e apresentar a proposta

Use os templates locais para criar/revisar `spec.md`, `plan.md` e `tasks.md`.
`spec.md` é a autoridade de estado, revisão e aprovação. `plan.md` e `tasks.md`
referenciam a revisão vigente da spec.

Ao criar nova spec, use o próximo ID após o maior prefixo numérico existente em
`specs/`, iniciando em `0001`, sem reutilizar lacunas. Preserve IDs legados.

Apresente automaticamente no chat, de forma proporcional à complexidade:

- ID, título, revisão e status;
- objetivo;
- requisitos e regras de negócio;
- escopo e, quando relevante, fora de escopo;
- plano técnico;
- impacto previsto;
- critérios de aceite e validação;
- riscos;
- decisões pendentes;
- pressupostos relevantes;
- documentos SDD efetivamente criados/alterados;
- componentes/arquivos previstos para alteração após aprovação;
- próxima ação: revisar, solicitar ajustes ou aprovar.

Mostre caminhos reais dos documentos e links navegáveis quando o ambiente
suportar. Não invente links nem apresente arquivos previstos como já alterados.

### 4. Gate de aprovação

Somente uma aprovação explícita da revisão vigente registrada em `spec.md`
autoriza implementação. Linguagem natural inequívoca é válida quando houver uma
única proposta em contexto. Silêncio, criação dos documentos ou aprovação
histórica não autorizam execução.

**Decisões pendentes** críticas bloqueiam aprovação. **Pressupostos** podem ser
aceitos junto com a proposta quando estiverem visíveis e não esconderem decisão
de negócio, segurança, dados ou arquitetura relevante.

Se o usuário aprovar e ao mesmo tempo solicitar mudança material, atualize a
proposta, incremente a revisão e peça nova aprovação antes de implementar.
Mudança material inclui requisito, aceite, escopo, contrato, dados, segurança,
arquitetura ou dependência relevante.

### 5. Executar e registrar evidências

Após aprovação, execute uma task por vez e respeite dependências. Registre em
`tasks.md` alterações reais, comandos, resultados, limitações, testes e QA.
Não declare teste, QA, commit, deploy ou homologação sem evidência.

Se a implementação exigir desvio material, suspenda a parte afetada e volte à
revisão. Não altere `spec.md` apenas para fazer o requisito coincidir com o
código produzido.

### 6. Sincronizar o handoff

Após cada task tecnicamente concluída, atualize o handoff para representar o
**estado atual**, não para acrescentar um diário. Inclua spec/revisão ativa,
estado, última task, próxima ação, bloqueios, testes/QA e referências aos
artefatos detalhados.

Histórico extenso deve permanecer em `tasks.md` ou docs especializados. Em
migração de handoff legado, preserve a fonte original antes de compactar e
verifique a recuperabilidade de decisões, pendências e evidências.

Se não houver handoff, crie um Markdown curto na raiz da aplicação. Se ele ou
o checkout estiver inacessível, registre a sincronização como pendente e não
alegue conclusão documental completa.
<!-- SDD:END -->
