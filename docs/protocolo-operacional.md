# Protocolo operacional SDD — v0.2-r2

**Estado:** proposta para revisão dos mantenedores. **Aplica-se:** a novas
instalações que usem os templates v0.2-r2 e a aplicações cujo bloco SDD seja
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

Só começa após aprovação explícita da revisão vigente registrada em `spec.md`.
O agente executa as tasks dentro do escopo aprovado, registra evidências e
sincroniza a continuidade.

## 3. Classificação da intenção

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

## 4. Nova spec ou revisão da spec ativa

Revise a spec ativa quando a nova solicitação continua perseguindo o mesmo
objetivo funcional e apenas altera ou esclarece a forma de satisfazê-lo.

Abra nova spec quando houver novo objetivo, novo workflow independente, novo
conjunto relevante de critérios de aceite ou escopo que possa ser implementado,
validado e retomado separadamente.

Não use revisão indefinida para absorver funcionalidades adjacentes. Preserve
IDs históricos e registre mudanças materiais entre revisões.

## 5. Criar e apresentar a proposta

1. Identifique projeto, instruções locais, base SDD, specs relacionadas e
   contexto necessário. Diferencie fatos observados, informação fornecida pelo
   usuário, hipóteses e propostas.
2. Crie ou revise `spec.md`, `plan.md` e `tasks.md`. `spec.md` recebe a nova
   revisão; plano e tarefas referenciam essa mesma revisão.
3. Registre requisitos e critérios com IDs rastreáveis quando aplicável. Para
   descoberta, use entregáveis e perguntas de levantamento em vez de requisitos
   funcionais artificiais.
4. Apresente automaticamente no chat uma **Proposta de Implementação** (ou de
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
5. Não trate arquivos previstos como já modificados. Não liste arquivo como
   criado/alterado sem tê-lo gravado. Links clicáveis são best effort; sempre
   mostre caminhos literais copiáveis e não invente URLs de editor.

## 6. Decisões pendentes e pressupostos

**Decisão pendente** é uma escolha necessária que afeta requisito, workflow,
segurança, dados, contrato, arquitetura relevante ou escopo. Enquanto crítica e
não resolvida, bloqueia aprovação válida.

**Pressuposto** é uma interpretação explícita e reversível usada para completar
a proposta sem criar uma pergunta desnecessária. Pode ser aceito junto com a
aprovação, desde que esteja visível e não esconda uma decisão crítica.

Se o usuário corrigir um pressuposto e isso alterar materialmente a proposta,
gere nova revisão antes da execução.

## 7. Estados e autorização

| Estado da spec | Significado | Implementação autorizada? |
|---|---|---|
| `proposta` | Artefatos em elaboração | Não |
| `em revisão` | Proposta apresentada ao usuário | Não |
| `aprovada` | Revisão vigente explicitamente aprovada | Sim, apenas escopo aprovado |
| `em execução` | Tasks autorizadas em andamento | Sim, dentro do escopo aprovado |
| `bloqueada` | Dependência ou decisão impede avanço | Não para a parte bloqueada |
| `implementada` | Trabalho técnico entregue; QA/sincronização pode faltar | Não autoriza novas mudanças |
| `concluída` | Aceite verificado e pendências finais resolvidas/justificadas | Não |
| `cancelada` | Trabalho encerrado sem conclusão integral | Não |

Fluxo típico: `proposta` → `em revisão` → `aprovada` → `em execução` →
`implementada` → `concluída`.

A aprovação fica registrada em `spec.md` e deve identificar a revisão vigente,
a manifestação inequívoca, data e autor quando identificáveis. Expressões
naturais como “aprovado”, “pode implementar” ou “pode executar essa proposta”
são válidas quando o contexto identifica uma única revisão sem ambiguidade.

Silêncio, criação dos documentos, aprovação antiga ou autorização de outro
escopo não contam como aprovação.

Se a mensagem de aprovação também trouxer mudança material — por exemplo,
“aprovado, mas use Redis” — atualize a proposta, incremente a revisão e peça
nova aprovação. Não implemente com base na aprovação condicionada anterior.

## 8. Mudança material

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

## 9. Execução, evidência e QA

- Execute uma task por vez, respeitando dependências e permissões locais.
- `tasks.md` registra estado da task, artefatos afetados, decisões, comandos,
  resultados, limitações e evidências reais.
- Testes automatizados e QA manual são separados. Use `não executado`,
  `realizado` com evidência, ou `não aplicável` com justificativa.
- Não declare teste, commit, deploy, homologação ou QA que não ocorreu.
- Se surgir mudança material durante implementação, suspenda a parte afetada,
  registre o desvio, revise a proposta e obtenha novo aceite.
- Não altere `spec.md` retrospectivamente para transformar desvio de código em
  requisito aprovado.

## 10. Handoff como estado atual

Após cada task tecnicamente concluída, **sincronize** o handoff para representar
o estado corrente. Não acrescente indefinidamente entradas cronológicas.

Conteúdo mínimo:

- spec e revisão ativa;
- estado atual;
- última task concluída e task/ação seguinte;
- resultado técnico mais recente;
- bloqueios/decisões relevantes;
- estado de testes e QA;
- referências para `spec.md`, `plan.md`, `tasks.md` e docs especializados.

Se detalhes antigos precisarem ser preservados, mova-os ou referencie-os em
`tasks.md`/docs temáticos. Em migração de handoff legado, preserve o original,
classifique o conteúdo e verifique recuperabilidade antes de compactar.

Se o handoff estiver inacessível, registre a sincronização como pendente; não
anuncie conclusão documental total.

## 11. Checagem de integridade

Antes de encerrar uma task ou spec, confirme:

- IDs e links existem e não há duplicação de spec;
- `plan.md` e `tasks.md` referenciam a revisão vigente de `spec.md`;
- estado e aprovação em `spec.md` correspondem ao trabalho executado;
- requisitos/entregáveis possuem critérios rastreáveis;
- tasks registram evidências e validações reais;
- decisões pendentes, pressupostos e desvios estão visíveis;
- mudanças materiais receberam nova revisão/aprovação quando necessário;
- handoff representa o estado atual e próxima ação.

## 12. Compatibilidade com legados

Não renomeie IDs nem reescreva automaticamente o acervo antigo. Se uma spec
legada tiver estado incompatível com tasks executadas, não invente aprovação
passada. Registre a inconsistência, confronte o histórico verificável e peça
decisão quando necessário.

Migre por projeto, com backup e relatório de alterações.
