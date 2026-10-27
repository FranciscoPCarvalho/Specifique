# Protocolo operacional SDD — v0.2-r3

**Estado:** proposta para revisão dos mantenedores. **Aplica-se:** a novas
instalações que usem os templates v0.2-r3 e a aplicações cujo bloco SDD seja
atualizado intencionalmente. Não migre specs legadas automaticamente.

## 1. Princípios e fontes de verdade

- O desenvolvedor define a intenção, revisa a engenharia proposta e autoriza a
  implementação. O agente organiza a documentação, propõe a abordagem técnica,
  implementa somente o que foi aprovado e registra evidências reais.
- `spec.md` é a **autoridade da proposta**: contém objetivo, escopo, requisitos,
  critérios de aceite, revisão vigente, estado e aprovação. `plan.md` descreve
  a estratégia de engenharia. `tasks.md` descreve execução e evidências.
- `plan.md` e `tasks.md` referenciam a revisão vigente da spec; não duplicam o
  registro de aprovação como fonte concorrente.
- `handoff.md`/`HANDOFF.md` da aplicação representa o **estado atual para
  retomada**, não um diário cronológico. Histórico detalhado fica em tasks e
  documentos especializados, com referências.
- O agente deve carregar contexto de forma progressiva: leia primeiro o menor
  conjunto de fontes capaz de identificar o trabalho corrente e fundamentar a
  decisão; expanda apenas quando dependências, ambiguidades ou impactos exigirem.
- Regras locais da aplicação continuam válidas. Em conflito, aplique a regra
  mais restritiva e torne a divergência explícita.
- O protocolo é declarativo. Depende do agente carregar as instruções, dos
  acessos concedidos e das capacidades da interface; não é daemon nem processo
  residente.

## 2. Fases operacionais

O ciclo normal possui três fases distintas.

### 2.1 Inspeção

Pode ocorrer antes da aprovação da implementação. O agente pode ler código,
documentação, specs, rotas, modelos, configurações e dependências declaradas
para compreender o contexto e preparar uma proposta.

Na inspeção, não pode alterar código da aplicação, instalar dependências,
executar migrações, modificar dados, fazer deploy ou executar operações
potencialmente destrutivas. Execução de aplicação/testes antes da aprovação só
é permitida quando as regras locais autorizarem explicitamente uma verificação
não modificadora e ela for necessária para fundamentar a proposta.

### 2.2 Proposta

O agente cria ou revisa os artefatos SDD necessários ao planejamento e os
apresenta ao usuário. A proposta ainda não autoriza implementação.

### 2.3 Execução

Só começa após aprovação explícita da revisão vigente registrada em `spec.md`
e após o **preflight de execução** confirmar que as premissas materiais do plano
continuam válidas. O agente executa as tasks dentro do escopo aprovado, registra
evidências e sincroniza a continuidade.

## 3. Carregamento progressivo de contexto

O agente não deve ler indiscriminadamente todo o acervo SDD ou todo o projeto a
cada interação. Use esta ordem como padrão:

1. regras locais e bloco SDD da aplicação;
2. índice documental do projeto e handoff, quando existente;
3. spec corrente e seus `plan.md`/`tasks.md`, quando houver;
4. docs temáticos e código diretamente relacionados à demanda;
5. specs históricas, documentos adicionais e áreas adjacentes somente quando
   houver dependência, ambiguidade, risco ou impacto que justifique ampliar o
   contexto.

Não carregue todas as specs antigas apenas por existirem. Prefira busca por ID,
objetivo, termo de domínio, rota, componente ou referência encontrada no
handoff/índice. Registre no plano quais fontes fundamentaram materialmente a
proposta.

## 4. Classificação da intenção

| Intenção | Exemplo | Tratamento |
|---|---|---|
| Mudança funcional | “Adicione login social” | Proposta obrigatória antes de alterar código. |
| Correção comportamental | “Corrija o cálculo” | Proposta com regressão e aceite. |
| Refatoração relevante | “Separe a lógica das views” | Proposta preservando contratos. |
| Descoberta/engenharia reversa | “Mapeie rotas e arquitetura” | Spec documental com fontes, limites e entregáveis. |
| Migração documental | “Organize o histórico no SDD” | Spec com preservação, classificação e conferência. |
| Consulta sem alteração | “Explique essa view” | Responder; nenhuma spec necessária. |
| Edição documental trivial | “Corrija um título” | Seguir regras locais; não criar spec artificial. |

A inicialização prepara estrutura e vínculo; não cria automaticamente uma spec
nem autoriza mapeamento, execução ou alteração funcional.

## 5. Specs em aberto e spec corrente

Uma **spec em aberto** é qualquer spec ainda não `concluída` ou `cancelada`.
Um projeto pode ter várias specs em aberto simultaneamente.

A **spec corrente** é a spec relacionada à demanda que o agente está tratando
na interação atual. Resolva-a, nesta ordem:

1. referência explícita do usuário a um ID/título;
2. se o usuário pedir apenas continuidade (“continue”, “prossiga”, “retome”), use
   o trabalho corrente indicado no handoff, confirmando a referência documental;
3. para uma demanda com objetivo próprio, compare objetivo/escopo com as specs em
   aberto; use o handoff apenas como índice de navegação, não como autoridade para
   forçar a nova demanda para a spec anteriormente corrente;
4. se duas ou mais specs continuarem plausíveis e a escolha alterar o trabalho,
   torne a ambiguidade explícita antes de editar artefatos.

Não presuma que exista uma única spec ativa global.

Revise a spec corrente quando a nova solicitação continua perseguindo o mesmo
objetivo funcional e apenas altera ou esclarece a forma de satisfazê-lo.

Abra nova spec quando houver novo objetivo, novo workflow independente, novo
conjunto relevante de critérios de aceite ou escopo que possa ser implementado,
validado e retomado separadamente.

Não use revisão indefinida para absorver funcionalidades adjacentes. Preserve
IDs históricos e registre mudanças materiais entre revisões.

## 6. Criar e apresentar a proposta

1. Identifique projeto, instruções locais, índice, handoff, spec corrente ou
   specs relacionadas e somente o contexto necessário. Diferencie fatos
   observados, informação fornecida pelo usuário, hipóteses e propostas.
2. Crie ou revise `spec.md`, `plan.md` e `tasks.md`. `spec.md` recebe a nova
   revisão; plano e tarefas referenciam essa mesma revisão.
3. Registre requisitos e critérios com IDs rastreáveis quando aplicável. Para
   descoberta, use entregáveis e perguntas de levantamento em vez de requisitos
   funcionais artificiais.
4. Registre em `plan.md` a **base da inspeção**: fontes e caminhos que
   fundamentaram materialmente a proposta e, quando disponível, referência de
   versão/commit apenas como evidência auxiliar, nunca como dependência do SDD.
5. Apresente automaticamente no chat uma **Proposta de Implementação** (ou de
   Descoberta/Migração) proporcional à complexidade, contendo:
   - identificação, revisão e status;
   - objetivo;
   - requisitos e regras de negócio;
   - escopo e, quando relevante, fora de escopo;
   - plano técnico;
   - impacto previsto;
   - critérios de aceite e estratégia de validação;
   - riscos;
   - decisões pendentes;
   - pressupostos relevantes;
   - documentos SDD efetivamente gerados/alterados;
   - componentes/arquivos previstos para alteração após aprovação;
   - próxima ação: revisar, solicitar ajustes ou aprovar.
6. Não trate arquivos previstos como já modificados. Não liste arquivo como
   criado/alterado sem tê-lo gravado. Links clicáveis são best effort; sempre
   mostre caminhos literais copiáveis e não invente URLs de editor.

## 7. Decisões pendentes e pressupostos

**Decisão pendente** é uma escolha necessária que afeta requisito, workflow,
segurança, dados, contrato, arquitetura relevante ou escopo. Enquanto crítica e
não resolvida, bloqueia aprovação válida.

**Pressuposto** é uma interpretação explícita e reversível usada para completar
a proposta sem criar uma pergunta desnecessária. Pode ser aceito junto com a
aprovação, desde que esteja visível e não esconda uma decisão crítica.

Se o usuário corrigir um pressuposto e isso alterar materialmente a proposta,
gere nova revisão antes da execução.

## 8. Estados, transições e autorização

| Estado da spec | Significado | Implementação autorizada? |
|---|---|---|
| `proposta` | Artefatos em elaboração | Não |
| `em revisão` | Proposta apresentada ao usuário | Não |
| `aprovada` | Revisão vigente explicitamente aprovada | Sim, condicionada ao preflight |
| `em execução` | Tasks autorizadas em andamento | Sim, dentro do escopo aprovado |
| `bloqueada` | Dependência ou decisão impede avanço | Não para a parte bloqueada |
| `implementada` | Trabalho técnico entregue; QA/aceite final pode faltar | Não autoriza novas mudanças |
| `concluída` | Critérios de aceite verificados e pendências finais resolvidas/justificadas | Não |
| `cancelada` | Trabalho encerrado sem conclusão integral | Não |

Transições determinísticas:

- `proposta → em revisão`: quando a proposta é apresentada ao usuário;
- `em revisão → aprovada`: quando a revisão vigente recebe aprovação explícita;
- `aprovada → em execução`: quando o preflight é aprovado e a primeira task é
  iniciada;
- `em execução → bloqueada`: quando impedimento real impossibilita continuar a
  parte relevante;
- `bloqueada → em execução`: quando o impedimento é resolvido sem mudança
  material; se houver mudança material, gere nova revisão;
- `em execução → implementada`: quando todas as tasks técnicas previstas para a
  revisão aprovada estão concluídas, ainda que QA/aceite final dependa de etapa
  posterior;
- `implementada → concluída`: quando os critérios de aceite foram verificados,
  QA aplicável foi resolvido e a documentação/handoff está sincronizada;
- estado aplicável → `cancelada`: quando o usuário cancela ou o trabalho é
  formalmente abandonado, preservando o histórico existente.

A aprovação fica registrada em `spec.md` e deve identificar a revisão vigente,
a manifestação inequívoca, data e autor quando identificáveis. Expressões
naturais como “aprovado”, “pode implementar” ou “pode executar essa proposta”
são válidas quando o contexto identifica uma única revisão sem ambiguidade.

Silêncio, criação dos documentos, aprovação antiga ou autorização de outro
escopo não contam como aprovação.

Se a mensagem de aprovação também trouxer mudança material — por exemplo,
“aprovado, mas use Redis” — atualize a proposta, incremente a revisão e peça
nova aprovação. Não implemente com base na aprovação condicionada anterior.

## 9. Preflight de execução

Após a aprovação e imediatamente antes da primeira task, revalide somente as
premissas materiais que fundamentam o plano. O objetivo não é repetir toda a
inspeção, mas confirmar que o contexto relevante não mudou de forma que invalide
ou altere materialmente a proposta.

Verifique, conforme aplicável:

- existência e forma dos arquivos/componentes centrais usados no plano;
- contratos, modelos, rotas, interfaces e dependências materiais;
- decisões e pressupostos que sustentam a estratégia;
- referência de versão/commit quando disponível, sem tornar Git obrigatório.

Registre o resultado em `tasks.md`:

- `válido`: contexto material compatível; execução pode iniciar;
- `desatualizado`: mudança material encontrada; não inicie a task, revise a
  proposta e solicite nova aprovação;
- `inconclusivo`: não foi possível confirmar premissa crítica; bloqueie a parte
  afetada e torne a limitação explícita.

Alterações externas não materiais podem ser registradas sem invalidar a
aprovação, desde que não mudem requisito, aceite, escopo, contrato, dados,
segurança, arquitetura relevante ou estratégia de risco/operação.

## 10. Mudança material

Exige nova revisão e invalida a aprovação anterior quando altera um ou mais:

- requisito ou regra de negócio;
- critério de aceite;
- escopo ou fora de escopo;
- contrato público/API;
- persistência ou migração de dados relevante;
- segurança, autorização ou privacidade;
- arquitetura ou dependência relevante;
- estratégia técnica com impacto material em risco, operação ou manutenção.

Correções editoriais sem impacto nesses itens não exigem nova aprovação; apenas
registre a edição quando necessário.

## 11. Execução, evidência e QA

- Execute uma task por vez, respeitando dependências e permissões locais.
- `tasks.md` registra preflight, estado da task, artefatos afetados, decisões,
  comandos, resultados, limitações e evidências reais.
- Testes automatizados e QA manual são separados. Use `não executado`,
  `realizado` com evidência, ou `não aplicável` com justificativa.
- Não declare teste, commit, deploy, homologação ou QA que não ocorreu.
- Se surgir mudança material durante implementação, suspenda a parte afetada,
  registre o desvio, revise a proposta e obtenha novo aceite.
- Não altere `spec.md` retrospectivamente para transformar desvio de código em
  requisito aprovado.

## 12. Handoff como estado atual e navegação multi-spec

Após cada task tecnicamente concluída, **sincronize** o handoff para representar
o estado corrente. Não acrescente indefinidamente entradas cronológicas.

Conteúdo mínimo:

- **trabalho corrente**, com spec, revisão, estado, última task concluída e
  próxima ação;
- **outros trabalhos em aberto**, listados de forma curta por ID/título/estado,
  quando existirem; se forem numerosos, destaque apenas os relevantes/bloqueados
  e referencie o índice SDD para a lista completa;
- resultado técnico mais recente do trabalho corrente;
- bloqueios/decisões relevantes;
- estado de testes e QA;
- referências para `spec.md`, `plan.md`, `tasks.md` e docs especializados.

O handoff é índice de continuidade, não fonte concorrente de status. Se houver
divergência, `spec.md` prevalece e o handoff deve ser sincronizado.

Se detalhes antigos precisarem ser preservados, mova-os ou referencie-os em
`tasks.md`/docs temáticos. Em migração de handoff legado, preserve o original,
classifique o conteúdo e verifique recuperabilidade antes de compactar.

Se o handoff estiver inacessível, registre a sincronização como pendente; não
anuncie conclusão documental total.

## 13. Checagem de integridade

Antes de encerrar uma task ou spec, confirme:

- IDs e links existem e não há duplicação de spec;
- a spec corrente foi resolvida sem confundir outros trabalhos em aberto;
- `plan.md` e `tasks.md` referenciam a revisão vigente de `spec.md`;
- estado e aprovação em `spec.md` correspondem ao trabalho executado;
- preflight foi registrado antes da primeira task da revisão aprovada;
- requisitos/entregáveis possuem critérios rastreáveis;
- tasks registram evidências e validações reais;
- decisões pendentes, pressupostos e desvios estão visíveis;
- mudanças materiais receberam nova revisão/aprovação quando necessário;
- handoff representa o trabalho corrente, demais trabalhos em aberto e próxima
  ação sem acumular histórico.

## 14. Compatibilidade com legados

Não renomeie IDs nem reescreva automaticamente o acervo antigo. Se uma spec
legada tiver estado incompatível com tasks executadas, não invente aprovação
passada. Registre a inconsistência, confronte o histórico verificável e peça
decisão quando necessário.

Migre por projeto, com backup e relatório de alterações.
