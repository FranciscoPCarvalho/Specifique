# Protocolo operacional SDD — proposta v0.2

**Estado:** proposta para revisão dos mantenedores. **Aplica-se:** a novas
instalações que usem os templates v0.2 e a aplicações cujo bloco SDD for
atualizado intencionalmente. Não migre specs legadas automaticamente.

## 1. Princípios e fontes de verdade

- O desenvolvedor formula intenção e aprova **o quê** e **como**; o agente
  gerencia documentação, propõe arquitetura, implementa apenas o aprovado e
  registra evidências.
- `spec.md` é fonte de requisitos e aceite aprovados; `plan.md`, da abordagem
  técnica aprovada; `tasks.md`, da execução e dos testes reais. Código é o
  comportamento observado e não reescreve requisitos retroativamente.
- `handoff.md`/`HANDOFF.md` da aplicação é índice breve de retomada. Detalhes
  históricos ficam em tasks e docs especializados, com referências.
- Regras locais da aplicação sobre segurança, execução e aprovações continuam
  válidas. Respeitar sempre os controles mais restritivos, resolvendo conflitos
  explícitos em vez de ignorá-los.
- O protocolo é declarativo e depende do agente carregar `AGENTS.md`, dos
  acessos concedidos e das capacidades da interface. Não é processo residente,
  daemon, observador de arquivos ou garantia automática de conformidade.

## 2. Classificação da intenção

| Intenção | Exemplo | Tratamento |
|---|---|---|
| Mudança funcional | “Adicione login social” | Proposta obrigatória antes de alterar código. |
| Correção comportamental | “Corrija o cálculo” | Proposta; cobertura de regressão. |
| Refatoração relevante | “Separe a lógica das views” | Proposta; preservar contratos. |
| Descoberta/engenharia reversa | “Mapeie rotas e arquitetura” | Spec documental de investigação, com fontes e limites. |
| Migração documental | “Organize o histórico no SDD” | Spec com plano de preservação e conferência. |
| Consulta sem alteração | “Explique essa view” | Responder; nenhuma spec necessária. |
| Edição documental trivial | “Corrija um título” | Seguir regras locais; não criar spec funcional artificial. |

Uma demanda coberta por spec ativa resulta em proposta de revisão, não em
novo ID automaticamente. A mera inicialização prepara estrutura e vínculo,
não exige criar spec ou executar mapeamento. Não presumir permissão de rodar
app, testes ou operações de dados por ter permissão de escrever documentação.

## 3. Criar e revisar a proposta

1. Identificar projeto, instruções locais, base SDD, specs relacionadas e
   escopo. Inspecionar estaticamente o necessário; registrar fontes e graus de
   confiança. Perguntar o que for indispensável para evitar uma decisão
   irreversível ou ambígua.
2. Criar/revisar spec, plano e tarefas da **mesma revisão** usando os modelos
   locais. Preservar IDs e o histórico. Distinguir requisitos, fatos atuais,
   hipóteses, decisões e alternativas. Incluir IDs de requisitos/aceite nas
   tasks, quando aplicável.
3. Apresentar automaticamente no chat a **Proposta de Implementação** (ou de
   Descoberta/Migração, conforme o tipo), proporcional à complexidade, com:
   - identificação, revisão e status;
   - objetivo;
   - requisitos e regras de negócio (ou entregáveis de descoberta);
   - plano técnico e decisões de arquitetura;
   - impacto previsto (componentes, arquivos, dados e integrações);
   - validações e critérios de aceite;
   - riscos, pressupostos e dúvidas que exigem confirmação;
   - arquivos gerados/alterados (caminhos reais, links quando suportados);
   - próxima ação: revisar, solicitar ajustes ou aprovar.
4. Não listar arquivos inexistentes como criados. Links clicáveis são
   **best effort** dependente de Codex/Claude/IDE; sempre exibir caminhos
   literais copiáveis. Não criar esquemas ou URLs de editor arbitrariamente.
5. Se houver alterações após apresentação, atualizar documentos pertinentes,
   incrementar a revisão e descrever diferenças. Uma revisão material torna
   inválida a aprovação anterior. Ajustes editoriais que não mudam escopo nem
   critérios devem ser registrados, sem fingir uma nova autorização se não
   houve mudança material.

## 4. Estados e autorização

| Estado da spec | Significado | Implementação autorizada? |
|---|---|---|
| `proposta` | Documentos em elaboração | Não |
| `em revisão` | Expostos ao usuário, com ajustes possíveis | Não |
| `aprovada` | Revisão atual explicitamente aprovada | Sim, apenas escopo aprovado |
| `em execução` | Tasks autorizadas sendo realizadas | Sim, dentro do escopo aprovado |
| `bloqueada` | Dependência ou decisão impede avanço | Não para parte bloqueada |
| `implementada` | Código/trabalho técnico entregue; QA ou sincronização pode faltar | Não autoriza novas mudanças |
| `concluída` | Aceite verificado e pendências de conclusão resolvidas/justificadas | Não autoriza novas mudanças |
| `cancelada` | Trabalho encerrado sem execução/completação integral | Não |

Fluxo típico: `proposta` → `em revisão` → `aprovada` → `em execução` →
`implementada` → `concluída`. Uma spec pode voltar a `em revisão` após mudança
material ou sair de `bloqueada` quando resolvida a causa, **com nova aprovação
quando necessário**. Não inferir `concluída` de testes automáticos aprovados
se QA manual obrigatório ou handoff sincronizado estiver pendente. Em specs
exclusivamente documentais, `implementada` significa entregáveis produzidos.

Aprovação deve indicar **ID da spec, revisão vigente, manifestação inequívoca,
autor e data quando identificáveis**, registrada de forma consistente nos três
artefatos. O texto “pode implementar a proposta apresentada” pode ser aceite
explícito no contexto; mera ausência de objeção, aprovação antiga ou criação
de documentos não é. Questionamento crítico ainda aberto impede aprovação
válida. Se o usuário editar spec/plano/tasks fora do chat, confronte mudanças
com a revisão aprovada antes de executar, registre a revisão material e peça
novo aceite quando necessário.

## 5. Execução, evidência e QA

- Executar uma task por vez, respeitando dependências e operações permitidas.
- Após conclusão técnica, registrar: task/IDs de aceite, código/artefatos
  afetados, decisões, comandos e resultados efetivos, limitações e testes
  pendentes. Não declarar testes que não ocorreram.
- QA manual é separado: `não realizado`, `realizado` com evidência de
  confirmação, ou `não aplicável` com justificativa. O mesmo vale para testes
  automáticos quando não aplicáveis.
- Mudança inesperada de regra, arquitetura, segurança, dados ou contrato:
  registrar desvio, suspender a parte afetada e submeter revisão/novo aceite.
  Não atualizar `spec.md` para mascarar divergência da implementação.
- Sincronizar spec/plano quando **uma decisão aprovada** afetar requisitos ou
  estratégia; mudanças no progresso ficam em tasks/handoff. Não alterar
  requisitos a cada task se permanecerem corretos.

## 6. Handoff curto e recuperação de contexto

Conteúdo mínimo: spec/revisão ativa com link; estado e task atual; resultado
mais recente; decisão ou bloqueio relevante; QA/testes pendentes; próxima
etapa; referências para arquivos detalhados. Evitar logs longos e cópia das
specs. Não fixar limite rígido de linhas: priorizar clareza e recuperabilidade.

Para handoffs legados extensos, fazer inventário, preservar a fonte original,
classificar informações em docs/specs/tasks, produzir índice de referências e
conferir amostras de decisões, requisitos, evidências e pendências. Uma
redução de linhas, isoladamente, não comprova fidelidade da migração.

Se a aplicação/handoff estiver inacessível, registrar task de sincronização
pendente na base SDD; não anunciar sincronização ou conclusão completa.

## 7. Checagem de integridade antes de encerrar tarefa/spec

- IDs e links dos artefatos existem; não há duplicação de spec.
- `spec.md`, `plan.md` e `tasks.md` referem-se ao mesmo ID e revisão.
- Estado da spec e aprovação estão coerentes com execução observada.
- Cada requisito/entregável possui critério de aceite rastreável; tasks
  remetem às verificações necessárias.
- Evidências de testes e QA distinguem executado, pendente e não aplicável.
- Divergências e alterações de escopo estão visíveis, sem redefinição
  silenciosa do requisito.
- Handoff aponta para estado atual e próximo passo, ou a impossibilidade
  de atualizá-lo está registrada explicitamente.

## 8. Compatibilidade com legados

Não renomear IDs nem reformatar o acervo antigo na implantação da versão 0.2.
Ao ler uma spec legada sem `Revisão` ou com `Status: proposta` apesar de tarefas
executadas, **não inventar aprovação passada**: registrar inconsistência,
reconciliar com o histórico verificável e solicitar decisão quando necessário.
Migrar por projeto, após cópia de segurança, com relatório de alterações.

## 9. Status após apresentação

Depois que a proposta for efetivamente apresentada no chat para revisão,
marque os três artefatos como `em revisão`, sem registrar aprovação. Se ainda
faltarem decisões críticas, identifique claramente a pendência e não permita
que a etapa avance para `aprovada`. A aprovação válida sincroniza ID, revisão
e estado nos três arquivos antes da primeira task autorizada.
