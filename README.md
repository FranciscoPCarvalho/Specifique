# SDD

Microframework leve de desenvolvimento orientado por especificações (SDD),
com agentes de codificação e documentação Markdown versionável. O usuário
solicita mudanças em linguagem natural; o agente prepara a proposta e só
implementa após revisão e aprovação explícita.

Instruções compartilhadas: [AGENTS](AGENTS.md) e [decisão sobre saídas de
comandos e RTK](docs/decisao-saidas-comandos-rtk.md).
Consulte também o [protocolo operacional](docs/protocolo-operacional.md) e o
[roteiro de validação](docs/roteiro-validacao.md) e o
[guia de atualização segura](docs/guia-atualizacao.md).

Cada projeto mantém sua base em `SDD/<projeto>/`, com fontes, especificações, planos e tarefas próprios. Esta estrutura não substitui a documentação do código nem aprova mudanças funcionais.

## Inicializar o SDD em um projeto

Pré-requisitos: uma pasta de projeto existente, este repositório SDD acessível
e um agente de IA que leia `AGENTS.md` e tenha permissão para escrever nas duas
pastas. O fluxo é conduzido pelas instruções Markdown; não há CLI ou script
de inicialização. Se seu agente não carregar `AGENTS.md` automaticamente,
peça explicitamente que leia o arquivo antes de começar.

Abra a pasta SDD no agente e solicite:

> Leia o AGENTS.md e inicialize o SDD no projeto localizado em `../meu-projeto`.

O caminho pode ser absoluto ou relativo à pasta SDD. Por exemplo, se SDD e
sigApp forem pastas irmãs, use `../sigApp`. Também são aceitos
caminhos com espaços, como `../Meu Projeto`. Não é necessário usar Git.

O agente usará os [templates](templates/) e o procedimento em
[AGENTS.md](AGENTS.md) para preparar:

```text
workspace/
├── SDD/
│   ├── AGENTS.md
│   ├── README.md
│   ├── templates/           # Modelos genéricos reutilizáveis
│   └── meu-projeto/
│       ├── README.md        # Índice e vínculo com o código
│       ├── docs/           # .gitkeep enquanto vazia
│       ├── specs/          # .gitkeep enquanto vazia
│       └── templates/
│           ├── spec.md
│           ├── plan.md
│           └── tasks.md
└── meu-projeto/
    └── AGENTS.md            # Bloco com vínculo e fluxo SDD
```

O nome da pasta do projeto será o identificador padrão. Você pode informar
outro identificador no pedido. Se o nome já estiver associado a outro projeto,
o agente solicitará um identificador diferente antes de escrever.

Se já houver `AGENTS.md`, o agente preservará suas regras e integrará um bloco
entre `<!-- SDD:BEGIN -->` e `<!-- SDD:END -->`. Referências SDD anteriores
serão conciliadas; conflitos que não possam ser resolvidos preservando as
regras locais serão apresentados antes da alteração.

Repetir a inicialização completa itens ausentes e atualiza o bloco de vínculo,
sem duplicar entradas ou substituir documentos, specs e templates personalizados.
Os links são relativos, sem caminhos pessoais fixos. Se mover as pastas para
outro layout, solicite novamente a inicialização para revisar os vínculos.

Inicializar prepara a estrutura e as instruções. Não faz levantamento funcional,
não cria a primeira spec, não executa a aplicação e não instala dependências.

## Fluxo em linguagem natural

Depois da inicialização, não é necessário invocar comandos SDD. Abra a pasta
da aplicação e descreva a mudança: “Adicione autenticação com Google”. O
agente investiga, escreve **spec.md, plan.md e tasks.md** e apresenta no chat
um **resumo executivo com caminhos dos arquivos**, incluindo objetivo, regras,
plano, impactos, critérios de aceite e questões para confirmação. O formato
de links clicáveis depende do agente e da IDE; os caminhos literais sempre
devem ser mostrados.

Você pode pedir detalhes, editar documentos e solicitar revisões. **Somente
uma aprovação explícita da revisão vigente** autoriza implementar; nova
mudança material invalida essa aprovação até nova revisão. Cada task concluída
atualiza evidências e um handoff conciso. O fluxo completo e os estados
constam no [protocolo](docs/protocolo-operacional.md).

Em projetos legados, após a inicialização, você pode solicitar separadamente
“Mapeie as rotas e a arquitetura do projeto”. O agente apresenta a proposta
de descoberta para aprovação antes do levantamento previsto. A inicialização
sozinha não cria specs nem executa essa descoberta.

## Criar uma spec depois de inicializar

Abra a pasta da aplicação no agente e diga, por exemplo:

> Adicione a funcionalidade X.

O comando “Vamos criar uma nova spec para este projeto: ...” continua aceito,
mas não é necessário.

Se disser apenas “Vamos criar uma nova spec para este projeto”, o agente
perguntará qual é a demanda. Ele lerá o contexto e os modelos locais, esclarecerá
o escopo e criará `spec.md`, `plan.md` e `tasks.md` em `specs/NNNN-slug/`,
dentro da base documental do projeto no SDD. A numeração começa em `0001`
e segue o maior número existente, sem reutilizar lacunas.

Os documentos serão apresentados como proposta e resumidos no chat com links
ou caminhos reais para consulta. Após revisão e aprovação explícita da revisão
vigente, a implementação seguirá uma tarefa por vez, respeitando as regras
do projeto e registrando evidências de testes e QA manual separadamente. Ao
concluir cada task, o responsável atualiza o handoff do projeto para permitir
retomada por outras pessoas; ao concluir a spec, consolida nele o estado final
e as pendências. A regra e o conteúdo mínimo estão em [AGENTS.md](AGENTS.md).

## License

Licensed under the Apache License, Version 2.0.
See the LICENSE file for details.
