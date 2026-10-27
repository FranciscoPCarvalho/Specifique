# SDD — {{PROJECT_ID}}

Base documental do projeto. [Código da aplicação]({{PROJECT_ROOT_LINK}}).
Esta estrutura foi inicializada sem levantamento funcional e não representa
autorização para alterar o código.

## Índice

- [Documentação](docs/)
- [Especificações](specs/)
- Modelos: [spec](templates/spec.md), [plano](templates/plan.md) e [tarefas](templates/tasks.md)

## Especificações

Nenhuma spec criada. Ao registrar a primeira, substitua esta frase pelos links
dos artefatos. Preserve as entradas anteriores nas próximas inclusões.

## Fluxo

Na pasta da aplicação, descreva diretamente o que deseja, por exemplo:
“Adicione autenticação com Google”. O agente segue três fases:

1. **Inspeção:** lê o contexto necessário sem implementar.
2. **Proposta:** cria spec, plano e tarefas e apresenta resumo executivo com
   requisitos, escopo, plano, impactos, aceite, decisões pendentes,
   pressupostos, documentos gerados e arquivos previstos para alteração.
3. **Execução:** somente após aprovação explícita da revisão vigente em
   `spec.md`, executa uma task por vez e registra evidências.

Você pode consultar/editar os arquivos ou pedir ajustes antes de aprovar. Uma
mudança material cria nova revisão. O handoff representa sempre o estado atual
para retomada, sem acumular histórico cronológico. Para sistemas existentes,
um mapeamento arquitetural é uma demanda separada e pode usar uma spec de
descoberta.

Consulte `../docs/protocolo-operacional.md` a partir da raiz SDD.

## Documentação do projeto

Adicione documentos em `docs/` conforme necessário e mantenha este índice
atualizado. Não presuma arquitetura, comandos ou regras que não foram
verificados. O handoff de continuidade fica na raiz do checkout da aplicação.
