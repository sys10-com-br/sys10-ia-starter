---
paths:
  - "src/**"
---

# Desempenho com volume de dados

Vale para todo código que lê, calcula, grava ou transfere dado que cresce com o uso: tabelas grandes, importação,
exportação, relatórios, sincronização e listas sem limite.

**Teste com dez linhas não mostra problema de volume.** Tudo que cresce é desenhado para o maior cliente real
multiplicado por 10 e medido com dado real antes do PR.

## 1. Saber o tamanho

Escreva no `CLAUDE.md` (§ Volumes de referência) os números do projeto, e atualize quando mudarem:

| Referência | Volume |
|---|---|
| <Maior cliente real: tabela principal> | <ex.: 50 mil linhas> |
| O mesmo ×4 / ×10 (o que o código tem que aguentar) | <ex.: 200 mil / 500 mil> |
| Memória disponível para a API em produção | <ex.: 512 MB, servidor compartilhado> |

No PR ou na ficha, diga **qual tabela cresce e até quanto** no ×10. Não sabe? Meça antes de desenhar
(`/sys10-07-desempenho-com-volume`).

## 2. Desenhar para o volume

- **Cálculo no banco, em conjunto.** Soma, agrupamento, comparação e status saem de uma consulta ou view, não de
  um laço no código sobre linhas carregadas.
- **A API não carrega a tabela na memória.** Selecione só as colunas que a tela usa, sem rastreamento do ORM;
  nada de trazer tudo para filtrar depois. Arquivo grande (exportação, relatório) sai em fluxo (streaming), não
  montado em memória.
- **Uma chamada, lista pronta, sem N+1:** nem uma requisição por linha no front, nem uma consulta num laço.
- **Lista sem limite tem paginação**, ou um motivo escrito para vir inteira (ex.: o app trabalha offline). Vir
  inteira é **uma** resposta, não centenas de páginas.
- **Índice para todo filtro, junção e ordenação** em tabela que cresce; chave estrangeira sempre indexada.
- **Escrita em lote.** Importação e gravação de muitas linhas: update/delete em conjunto ou cópia em lote
  (`COPY`, bulk insert), nunca um salvar por linha. Transação curta, só em escrita.
- **Front:** a tela não recalcula o que a API entrega pronto; tabela com milhares de linhas pagina ou rola sem
  travar o navegador; cache das leituras (React Query, SWR…) para não buscar de novo.

## 3. Medir antes do PR

Desenhar certo não dispensa medir. Antes do PR, rode `/sys10-07-desempenho-com-volume`: banco local com o maior
cliente ×1, ×4 e ×10, plano da consulta, tempo e memória antes → depois, teste de guarda e os números no PR.

## Como conferir

- Nenhum laço no código sobre linhas de tabela que cresce; nenhuma leitura dela sem filtro.
- Toda consulta nova em tabela que cresce tem índice para o filtro e a ordenação.
- A memória da API não cresce com o volume (o ×10 não usa 10× a memória).
