# Guia para revisar e adotar a proposta v0.2

Esta distribuição é uma **proposta para revisão**, gerada em cópia separada.
Não altera seus projetos existentes e **não deve** substituir indiscriminadamente
a árvore SDD já em uso.

## Arquivos alterados na raiz compartilhada

- `AGENTS.md`, `README.md` e os quatro templates existentes em `templates/`.
- Adicionados: `CHANGELOG.md`, `docs/protocolo-operacional.md`,
  `docs/roteiro-validacao.md`, `docs/guia-atualizacao.md`.
- Incluído `docs/decisao-saidas-comandos-rtk.md` já existente no acervo de
  referência, mas não presente no ZIP mínimo original.

## Procedimento controlado

1. Faça backup/commit do repositório SDD existente. Compare os novos arquivos
   com os correspondentes da sua raiz SDD; preserve customizações.
2. Instale as instruções centrais e a documentação compartilhada somente após
   revisar decisões e links. Os projetos listados no README de exemplo devem
   apontar para diretórios realmente existentes na instalação efetiva.
3. **Não sobrescreva** automaticamente `SDD/<projeto>/templates/`: na
   inicialização original, modelos locais existentes são intencionalmente
   preservados. Para adotar os novos campos, faça comparação e migração
   explicitamente aprovada por projeto, com cópia de segurança.
4. Atualize o bloco delimitado por `<!-- SDD:BEGIN -->` e
   `<!-- SDD:END -->` no `AGENTS.md` da aplicação, preservando todas as
   instruções locais fora do bloco. Revalidar vínculos relativos e conflitos.
   A inicialização pode ajudar a atualizar o bloco, mas não deverá reescrever
   templates locais já personalizados.
5. Deixe specs e handoffs históricos intactos nesta fase. Teste primeiro com
   uma cópia de projeto e o roteiro `docs/roteiro-validacao.md`.
6. Só depois adote em produção e documente resultados reais por agente/IDE.

## Observações de compatibilidade

- O bloco AGENTS da aplicação é uma convenção; verifique como cada agente
  carrega instruções locais. Não presumir que todos leiam `AGENTS.md` da mesma
  maneira ou renderizem links de arquivo de modo idêntico.
- Não houve migração automática dos projetos nem execução de testes das
  aplicações nesta entrega.
