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

O contrato completo de intenção, inspeção, proposta, aprovação, execução e
sincronização está em [docs/protocolo-operacional.md](docs/protocolo-operacional.md).
Aplique-o com as regras locais e com o bloco SDD vinculado à aplicação.

Regras essenciais:

- intenção de mudança relevante aciona o SDD mesmo sem palavra-chave;
- inspeção pode ler o necessário, mas não implementar antes da aprovação;
- `spec.md` é a autoridade de revisão, estado e aprovação;
- `plan.md` descreve estratégia e `tasks.md` execução/evidências;
- a proposta deve separar decisões pendentes de pressupostos e distinguir
  documentos já gerados de arquivos apenas previstos para alteração;
- mudança material exige nova revisão e nova aprovação;
- handoff deve representar o estado atual e próxima ação, não um diário;
- QA, testes, commit, deploy e homologação só podem ser declarados com evidência.

Não duplique aqui as regras detalhadas do protocolo. Se houver incompatibilidade
entre este resumo e o protocolo, interrompa a execução e reconcilie as instruções
antes de alterar a aplicação.

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
