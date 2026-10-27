# Decisão sobre saídas de comandos e uso do RTK

**Versão do RTK avaliada historicamente:** 1.0.1  
**Data do registro histórico:** 2026-10-17  
**Fonte normativa vigente:** [`../AGENTS.md`](../AGENTS.md)

Este documento compartilha a decisão de reduzir ruído de comandos sem perder
ambiente, evidência ou status real da execução. A política vigente está em
`SDD/AGENTS.md`; este registro preserva contexto, exemplos e limitações do
levantamento histórico.

## Política

- Limite a consulta ao necessário e prefira saída nativa concisa que preserve o resultado.
- RTK é opcional: use-o explicitamente apenas quando houver ganho líquido e cobertura compatível.
- Preserve interpretador, ambiente virtual, argumentos, semântica e código de saída.
- Em falhas, preserve alvo, erro, diferenças esperadas/obtidas e contexto da exceção.
- Remova progresso, banners e repetições sem filtrar texto exato ou sequência necessária.
- Em saídas extensas, guarde stdout e stderr completos em arquivo temporário e informe seu caminho.
- Recupere trechos específicos por caminho ou `rtk recall` quando faltar evidência; use `rtk bypass` somente quando necessário.
- Agrupe verificações relacionadas mantendo comando e resultado identificáveis.

## Exemplos históricos

Os exemplos abaixo são ilustrativos e não representam execuções desta
atualização. A captura mantém a saída integral e o status original:

```bash
log_path=$(mktemp /tmp/django-test.XXXXXX.log)
if python manage.py test app.tests.TesteAlvo --verbosity 0 >"$log_path" 2>&1; then
    test_status=0
else
    test_status=$?
fi
tail -n 40 "$log_path"
printf 'relatorio completo: %s status original: %s\n' "$log_path" "$test_status"
exit "$test_status"
```

Para pytest, a seleção pode reduzir ruído sem alterar o ambiente:

```bash
python -m pytest caminho/para/teste.py -q --tb=short
```

Comandos de saída já curta podem ser executados diretamente:

```bash
python manage.py check
journalctl -u nome-do-servico --since '2026-10-17 10:00' --until '2026-10-17 11:00' --no-pager
rg -n -C 3 'padrao' caminho/para/arquivo.py
```

Quando houver hash real disponível, a recuperação pode ser específica:

```bash
rtk log "$log_path"
rtk recall "$recall_hash" --grep 'error|erro|fail|traceback|exception'
```

`recall_hash` é um placeholder e deve ser substituído pelo hash real.

## Limitações conhecidas do levantamento histórico

Em testes sintéticos registrados em 2026-10-17, o RTK 1.0.1 reescreveu algumas
saídas de `git status` e pytest; `manage.py test/check` e `journalctl` não foram
reescritos. Filtros `test`/`err` preservaram status 1, mas omitiram diagnósticos;
uma saída longa de `rtk test` ficou nas últimas cinco linhas; e o recall SQLite
não tinha entradas. Não foram executados testes reais Django ou banco, e a
integração automática de hooks não foi confirmada. Essas limitações são
históricas e não afirmam a versão ou comportamento atuais.
