# SDD — {{PROJECT_ID}}

Base documental do projeto. [Código da aplicação]({{PROJECT_ROOT_LINK}}).
Esta estrutura foi inicializada sem levantamento funcional e não representa
aprovação para alterar o código.

## Índice

- [Documentação](docs/)
- [Especificações](specs/)
- Modelos: [spec](templates/spec.md), [plano](templates/plan.md) e [tarefas](templates/tasks.md)

## Especificações

Nenhuma spec criada. Ao registrar a primeira, substitua esta frase pelos links
de spec, plano e tarefas. Preserve as entradas anteriores nas próximas inclusões.

## Fluxo

Na pasta da aplicação, descreva diretamente o que deseja, por exemplo:
“Adicione autenticação com Google”. O agente detecta a demanda, investiga o
contexto e prepara uma spec, um plano e tarefas numerados. Antes de implementar,
apresenta resumo executivo com objetivo, regras, estratégia, impactos, critérios
de aceite, decisões pendentes e caminhos para os três arquivos. Você pode
consultar/editar os arquivos ou solicitar ajustes; a **revisão atual** depende
de aprovação explícita. Só então o agente executa uma tarefa por vez,
registrando testes e QA manual separadamente. Para sistemas existentes, peça
um mapeamento de arquitetura como **demanda separada**, também sujeito a plano
e aprovação. Consulte `../docs/protocolo-operacional.md` a partir da raiz SDD.

## Documentação do projeto

Adicione documentos em `docs/` conforme necessário e mantenha este índice
atualizado. Não presuma arquitetura, comandos ou regras que não foram verificados.
O handoff de continuidade fica na raiz do checkout da aplicação e deve ser
atualizado ao concluir cada task e ao consolidar uma spec; consulte o `AGENTS.md`
da SDD para o conteúdo mínimo e para registrar a localização adotada.
