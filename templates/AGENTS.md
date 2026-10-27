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

Um projeto pode ter várias specs em aberto. **Spec corrente** é a que corresponde
à demanda desta interação. Use referência explícita do usuário quando houver; em
pedidos apenas de continuidade, use o trabalho corrente do handoff; em novas
demandas com objetivo próprio, compare objetivo/escopo com as specs em aberto e
use o handoff apenas como índice de navegação. Não presuma uma única spec ativa
global. Se duas ou mais specs continuarem plausíveis e a escolha mudar o
trabalho, torne a ambiguidade explícita antes de editar artefatos.

Revise a spec corrente quando a demanda continua perseguindo o mesmo objetivo.
Abra nova spec quando houver novo objetivo, workflow ou conjunto independente de
critérios de aceite.

### 2. Carregar contexto progressivamente

Não leia todo o acervo SDD nem todo o projeto por padrão. Use esta ordem:

1. regras locais e este bloco SDD;
2. índice do projeto e handoff, quando existente;
3. spec corrente e seus `plan.md`/`tasks.md`, quando houver;
4. docs e código diretamente relacionados;
5. specs históricas e áreas adjacentes apenas quando dependência, ambiguidade,
   risco ou impacto exigirem.

Prefira busca por ID, objetivo, termo de domínio, rota, componente ou referência
do handoff/índice. Expanda o contexto somente quando necessário.

### 3. Inspecionar antes de propor

Na fase de inspeção, leia o necessário para compreender contexto, regras,
arquitetura e impacto. Diferencie fatos observados, informação do usuário,
hipóteses e propostas.

Antes da aprovação, não altere código da aplicação, instale dependências,
execute migrações, modifique dados, faça deploy ou execute operações destrutivas.
Execução de aplicação/testes prévia só é permitida quando as regras locais a
autorizarem explicitamente e ela for necessária para fundamentar a proposta.

### 4. Preparar e apresentar a proposta

Use os templates locais para criar/revisar `spec.md`, `plan.md` e `tasks.md`.
`spec.md` é a autoridade de estado, revisão e aprovação. `plan.md` e `tasks.md`
referenciam a revisão vigente da spec.

Ao criar nova spec, use o próximo ID após o maior prefixo numérico existente em
`specs/`, iniciando em `0001`, sem reutilizar lacunas. Preserve IDs legados.

Registre no plano a **base da inspeção**: arquivos, docs, interfaces e outras
fontes que fundamentaram materialmente a proposta. Git/commit pode aparecer
como evidência auxiliar quando disponível, mas não é requisito do SDD.

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

### 5. Gate de aprovação

Somente uma aprovação explícita da revisão vigente registrada em `spec.md`
autoriza implementação, condicionada ao preflight de execução. Linguagem natural
inequívoca é válida quando houver uma única proposta em contexto. Silêncio,
criação dos documentos ou aprovação histórica não autorizam execução.

**Decisões pendentes** críticas bloqueiam aprovação. **Pressupostos** podem ser
aceitos junto com a proposta quando estiverem visíveis e não esconderem decisão
de negócio, segurança, dados ou arquitetura relevante.

Se o usuário aprovar e ao mesmo tempo solicitar mudança material, atualize a
proposta, incremente a revisão e peça nova aprovação antes de implementar.
Mudança material inclui requisito, aceite, escopo, contrato, dados, segurança,
arquitetura ou dependência relevante.

### 6. Fazer o preflight de execução

Após a aprovação e antes da primeira task da revisão, revalide somente as
premissas materiais que fundamentam o plano. Verifique componentes centrais,
contratos, modelos, rotas, interfaces, dependências e pressupostos relevantes,
conforme aplicável.

Registre em `tasks.md` o resultado:

- `válido`: contexto material compatível; pode iniciar;
- `desatualizado`: mudança material encontrada; revise a proposta e obtenha nova
  aprovação;
- `inconclusivo`: premissa crítica não pôde ser confirmada; bloqueie a parte
  afetada e torne a limitação explícita.

Somente após preflight `válido` e início da primeira task altere o estado da spec
de `aprovada` para `em execução`.

### 7. Executar e registrar evidências

Execute uma task por vez e respeite dependências. Registre em `tasks.md`
alterações reais, comandos, resultados, limitações, testes e QA. Não declare
teste, QA, commit, deploy ou homologação sem evidência.

Use as transições de estado do protocolo. Em particular, `implementada` significa
que as tasks técnicas terminaram; `concluída` exige aceite/QA aplicável e
sincronização documental final.

Se a implementação exigir desvio material, suspenda a parte afetada e volte à
revisão. Não altere `spec.md` apenas para fazer o requisito coincidir com o
código produzido.

### 8. Sincronizar o handoff

Após cada task tecnicamente concluída, atualize o handoff para representar o
**estado atual**, não para acrescentar um diário.

Registre o **trabalho corrente** com spec/revisão, estado, última task e próxima
ação. Quando existirem outras specs em aberto, liste-as de forma curta por
ID/título/estado em uma seção separada; se forem numerosas, destaque as
relevantes/bloqueadas e referencie o índice SDD para a lista completa. Inclua
bloqueios, testes/QA e referências aos artefatos detalhados.

O handoff é índice de continuidade, não fonte concorrente de status; em caso de
divergência, `spec.md` prevalece e o handoff deve ser sincronizado.

Histórico extenso deve permanecer em `tasks.md` ou docs especializados. Em
migração de handoff legado, preserve a fonte original antes de compactar e
verifique a recuperabilidade de decisões, pendências e evidências.

Se não houver handoff, crie um Markdown curto na raiz da aplicação. Se ele ou
o checkout estiver inacessível, registre a sincronização como pendente e não
alegue conclusão documental completa.
<!-- SDD:END -->
