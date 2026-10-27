# Instruções do agente no SDD

Este repositório mantém documentação por projeto. Pedidos de inicialização
autorizam preparar a base documental e integrar o vínculo ao `AGENTS.md` do
projeto informado. Não autorizam implementar funcionalidades, executar a
aplicação, instalar dependências ou criar um levantamento inicial.

Estas regras se aplicam à documentação compartilhada e às aplicações
consumidoras quando carregarem estas instruções, respeitando as instruções
específicas de cada aplicação. O checkout SDD não é ancestral dos checkouts de
código irmãos. Estas regras não copiam nem substituem as regras globais de
subagentes.

## Inicializar um projeto

1. Identifique a raiz deste SDD pela localização deste arquivo, sem depender
   de Git nem assumir que o diretório atual seja a raiz. Resolva o caminho
   informado pelo usuário: caminhos relativos partem desta raiz SDD. Normalize
   caminhos e symlinks e confirme que o destino é um diretório existente.
   Se faltar o caminho, solicite-o. Não crie a pasta da aplicação.
2. Leia as instruções aplicáveis no destino e seu `AGENTS.md`, quando existente.
   Inspecione o README e os arquivos de identificação necessários para reconhecer
   o projeto, sem executar código. Não copie regras de negócio de outro projeto.
3. Use como identificador o nome da pasta de destino, preservando espaços e
   caixa, salvo identificador explícito do usuário. O identificador deve ser um
   único componente de caminho, diferente de `.` e `..`. Rejeite separadores,
   caracteres de controle e os nomes reservados `templates`, `.git`, `AGENTS.md`,
   `README.md` e `LICENSE`. O destino não pode ser a própria raiz SDD nem estar
   dentro dela; a documentação ficará em `<raiz-SDD>/<identificador>/`.
4. Antes de escrever, verifique se a base já existe e a qual aplicação pertence.
   Use o vínculo de código no índice do projeto e o bloco SDD no `AGENTS.md`
   da aplicação, resolvendo os caminhos. Se apontarem para outro projeto,
   peça outro identificador; se a associação for ambígua, esclareça com o usuário.
   Uma pasta vazia pode ser completada. Não atribua documentação existente a uma
   aplicação apenas porque os nomes das pastas coincidem.
5. Prepare os valores dos templates conforme a tabela abaixo. Crie somente os
   arquivos ausentes: índice a partir de `templates/project-README.md`,
   diretórios `docs/`, `specs/` e `templates/`, e cópias dos modelos `spec.md`,
   `plan.md` e `tasks.md` dentro dos templates do projeto. Substitua somente
   `{{PROJECT_ID}}` nesses três modelos; os demais campos serão preenchidos ao
   criar uma spec. Preserve documentos, specs e modelos personalizados existentes.
   Crie `.gitkeep` em `docs/` e `specs/` somente quando estiverem vazios.
6. Integre o conteúdo de `templates/AGENTS.md` ao `AGENTS.md` da aplicação.
   Se não existir, crie-o com esse conteúdo. Caso exista, preserve as regras
   locais e acrescente o bloco delimitado por `<!-- SDD:BEGIN -->` e
   `<!-- SDD:END -->`. Se já houver exatamente um bloco completo, atualize-o
   em vez de duplicá-lo. Marcadores incompletos ou duplicados precisam ser
   conciliados antes de escrever. Revise instruções SDD fora do bloco: atualize
   apenas referências antigas cujo destino esteja confirmado, preservando regras
   de ambiente, negócio e aprovações. Se houver conflito real entre regras,
   esclareça antes de alterar o arquivo; não deixe duas orientações incompatíveis.
7. Registre um link para o índice do projeto na seção `Projetos` do README
   geral. Compare destinos normalizados para não duplicar entradas. Preserve
   as demais entradas e o conteúdo do índice de projeto existente. Se ele ainda
   não tiver o vínculo para o código, acrescente-o sem reescrever o documento.
8. Valide os links gerados, a existência da estrutura e a ausência de campos
   de inicialização pendentes. Informe os arquivos criados/alterados e que a próxima demanda pode ser
   expressa naturalmente (por exemplo, “Adicione a funcionalidade X”).
   Ofereça o mapeamento arquitetural como próxima etapa opcional, sujeito a
   proposta e aprovação. Não crie uma spec automaticamente na inicialização,
   nem marque aprovação ou testes sem evidência.

## Campos dos templates

Todos os caminhos são relativos à pasta do arquivo que os contém, não ao
diretório de execução do terminal. Calcule-os entre os destinos normalizados,
por exemplo com `os.path.relpath`, sem caminhos pessoais absolutos. Use `/`
como separador nos links. Para URLs Markdown, aplique percent-encoding aos
componentes especiais (inclusive espaços, `#` e parênteses), preservando `/`
e `..`, por exemplo com `urllib.parse.quote(caminho, safe="/.")`.
Escape também caracteres Markdown nos textos de exibição; mantenha nomes
originais e delimitadores de código válidos nos valores literais.

| Campo | Valor e origem |
|---|---|
| `{{PROJECT_ID}}` | Identificador da pasta documental do projeto. |
| `{{SDD_ROOT_PATH}}` | Caminho relativo da raiz da aplicação para a raiz SDD, como texto literal. |
| `{{SDD_PROJECT_PATH}}` | Caminho relativo da raiz da aplicação para sua base documental, como texto literal. |
| `{{SDD_INDEX_LINK}}` | URL relativa do `AGENTS.md` da aplicação para o índice documental. |
| `{{SDD_DOCS_LINK}}` | URL relativa do `AGENTS.md` da aplicação para `docs/`. |
| `{{SDD_SPECS_LINK}}` | URL relativa do `AGENTS.md` da aplicação para `specs/`. |
| `{{SDD_TEMPLATES_LINK}}` | URL relativa do `AGENTS.md` da aplicação para `templates/`. |
| `{{PROJECT_ROOT_LINK}}` | URL relativa do índice documental para a pasta da aplicação; identifica a associação. |

Os campos `{{SPEC_ID}}`, `{{SPEC_TITLE}}` e `{{DATE}}` permanecem nos modelos
locais e são substituídos apenas ao gerar os documentos de uma spec. Nunca
reprocesse os templates personalizados existentes durante uma reinicialização.

## Trabalho em bases existentes

O protocolo de intenção, revisão, aprovação, execução e sincronização está em
[docs/protocolo-operacional.md](docs/protocolo-operacional.md). Aplique-o com
as regras locais do projeto e com o bloco SDD vinculado à aplicação.

**Intenção, não palavra-chave:** após a inicialização, solicitações naturais de
mudança funcional, correção de comportamento ou refatoração relevante iniciam
a preparação de spec/plano/tarefas, mesmo sem menção a SDD. Solicitações de
mapeamento/documentação podem iniciar uma spec de descoberta. Não crie specs
para perguntas, consultas informativas ou simples leitura de código; antes de
alterar código, confirme se a demanda exige proposta e aprovação. Pequenas
mudanças funcionais também exigem aprovação. Alterações editoriais estritamente
triviais podem seguir regras locais, mas nunca contornar aprovações explícitas.

**Revisão antes da implementação:** apresente no chat um resumo executivo
com identificação/status/revisão, objetivo, regras/requisitos, plano técnico,
impactos, critérios de aceite, riscos/dúvidas, caminhos navegáveis dos três
artefatos e próxima ação. Diferencie fatos observados, hipóteses e decisões.
Gere os arquivos primeiro; não anuncie arquivos que não foram gravados. Use
links relativos ou referências de arquivo reconhecidas pelo agente/IDE quando
suportadas e mostre sempre o caminho literal como alternativa. Não invente
URLs `file://` nem afirme que o editor abrirá o link sem suporte confirmado.

**Gate obrigatório:** só implemente depois de aprovação inequívoca da
**revisão atual** de spec, plano e tarefas, registrada nos artefatos. Silêncio,
criação de arquivos, aprovação de outro escopo e aprovação histórica não
valem. Em caso de alteração substancial de escopo ou decisão arquitetural,
interrompa a parte afetada e obtenha nova aprovação da revisão atualizada.
Bloqueie a execução quando uma dúvida impactar requisitos, segurança, dados
ou arquitetura e não houver decisão suficiente.

**Integridade:** mantenha IDs estáveis, requisitos ligados a critérios de
aceitação e tarefas, status coerentes e evidências verificáveis. A cada task
tecnicamente concluída, registre os resultados em `tasks.md`, atualize os
documentos quando houver decisão aprovada relevante, e sintetize a retomada no
handoff. Não altere a spec só para justificar divergência do código. Marque
bloqueios/documentos indisponíveis; nunca declare sincronização realizada sem
acesso ao destino. Handoff é índice de estado e continuidade, não log extenso.


Leia o índice e os documentos relevantes antes de propor alterações. Siga as
instruções da aplicação para trabalhar no seu código. O fluxo é proposta →
revisão de spec/plano/tarefas → aprovação → execução sequencial. Documentação
histórica não representa aprovação de mudanças futuras. QA manual exige
confirmação explícita para ser registrado como realizado.

### Handoff obrigatório ao concluir tasks e specs

Ao concluir tecnicamente cada task, atualize o arquivo de handoff do projeto
(`handoff.md`, `HANDOFF.md` ou o nome já adotado) com o estado necessário para
que outra pessoa possa continuar: resultado e comportamento implementado,
decisões relevantes, arquivos/áreas afetados, testes e comandos com resultados,
falhas ou limitações conhecidas, QA manual ainda pendente e próximo passo. Ao
concluir uma spec, consolide no handoff o estado final de todas as tasks e as
pendências remanescentes. Registre fatos; não declare QA, aprovação, commit,
deploy ou homologação sem confirmação/evidência.

Preserve as convenções, decisões e referências do handoff existente, mas não
perpetue um histórico cronológico crescente: mova ou referencie registros
detalhados em `tasks.md` ou documentos especializados. Em uma migração de
handoff antigo, preserve o original em arquivo/versão identificável e confira
a recuperabilidade de decisões, pendências e evidências antes de compactá-lo.
Se o projeto ainda não
tiver handoff, crie um em Markdown na raiz do projeto e inclua nele um caminho
curto para retomar a SDD e a task/spec ativa. Registre a localização adotada no
índice e nas tasks relevantes. Se o checkout ou o arquivo não estiver
disponível, conclua a documentação que puder e registre explicitamente a
limitação, sem inventar o conteúdo do handoff.

Handoff serve à continuidade do trabalho e não substitui `tasks.md`, resultados
de teste, QA manual ou fontes de código. Atualize-o em conjunto com o registro
da task, antes de considerar concluída a etapa documental.

## Saídas de comandos

Antes de executar, limite a consulta ao necessário: arquivos, testes,
serviços, intervalo de tempo e campos relevantes. Prefira opções nativas de
saída concisa que preservem o resultado necessário.

No início da sessão, verifique se `rtk` está disponível com `command -v rtk`.

O RTK é opcional. Quando instalado, use-o explicitamente apenas se houver
ganho líquido de contexto, tempo e confiabilidade, com cobertura compatível e
sem perda de informação necessária ou mudança de semântica, status, argumentos,
interpretador ou ambiente virtual. Se estiver ausente, use o comando nativo.
Não execute as duas formas apenas para comparar. Prefira o comando nativo para
saídas já curtas ou dados que exijam bytes, ordem ou estrutura exatos. Não
presuma hook ou reescrita automática.

Em sucesso, retorne status e resultados necessários. Em falha, preserve código
de saída, alvo, erro, diferenças esperadas e obtidas e contexto suficiente da
cadeia de exceções. Remova progresso, banners e repetições, mantendo avisos
pertinentes; não aplique filtros com perda quando texto exato ou sequência dos
eventos forem necessários.

Para execuções potencialmente extensas, preserve stdout e stderr completos em
arquivo temporário e apresente um resumo com seu caminho. Preserve o código de
saída original, inclusive ao usar pipelines. Se faltar evidência, recupere
primeiro trechos específicos pelo caminho informado ou por `rtk recall`, quando
disponível; use `rtk bypass` somente quando necessário e não repita execuções
apenas para recuperar saída. Agrupe verificações independentes relacionadas,
mantendo identificáveis comando e resultado, e amplie a saída conforme a
investigação exigir.

As instruções da aplicação prevalecem para seu ambiente, interpretador, venv,
comandos e escopo. Os projetos devem seguir seus próprios AGENTS e handoffs.
