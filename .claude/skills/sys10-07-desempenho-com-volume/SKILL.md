---
name: sys10-07-desempenho-com-volume
description: Use quando o código lê, calcula, grava ou transfere dados que crescem com o uso — tabelas grandes, importação, exportação, relatórios, sincronização, listas sem limite. Também quando alguém diz "está lento", "isso aguenta o cliente grande?", "a API caiu por memória", "precisa de índice?" ou "mede isso".
---

# Desempenho com volume de dados

**Teste com dez linhas não mostra problema de volume.** Tudo que cresce com o uso é desenhado para o maior cliente
real multiplicado por 10, **medido** com dado real antes do PR, e ganha um teste de guarda com orçamento de tempo.

## 1. Saber o tamanho

Escreva no `CLAUDE.md` (§ Volumes de referência) os números do projeto, e atualize quando mudarem:

| Referência | Volume |
|---|---|
| <Maior cliente real: tabela principal> | <ex.: 50 mil linhas> |
| O mesmo ×4 / ×10 (o que o código tem que aguentar) | <ex.: 200 mil / 500 mil> |
| Memória disponível para a API em produção | <ex.: 512 MB, servidor compartilhado> |

No PR ou na ficha, diga **qual tabela cresce e até quanto** no ×10. Não sabe? Meça antes de desenhar.

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

## 3. Medir com dado real

1. **Banco local** com uma cópia do maior cliente (anonimizada se precisar), nunca o de produção. Gere o ×4 e o
   ×10 multiplicando os dados reais, não inventando.
2. **Plano da consulta:** `EXPLAIN (ANALYZE, BUFFERS)` (Postgres) ou o equivalente do seu banco. Em tabela que
   cresce, varredura completa só com motivo.
3. **Tempo e memória** nos três tamanhos, **antes e depois** da mudança: tempo da consulta e do endpoint com a
   aplicação aquecida; pico de memória da API (`docker stats` ou o profiler da plataforma).
4. **Teste de guarda** com orçamento (ex.: até 1 s no real, até 3 s no ×10 para leitura de tela), num projeto de
   testes de desempenho que roda contra o banco com o volume. Mudou a forma de calcular uma regra? Um teste confere
   item a item que a forma nova bate com a antiga.

Não deu para medir? Diga no PR com todas as letras o que ficou sem medida.

## 4. Mais de um jeito? Compare e decida em ADR

Dúvida real entre formas (memória × banco, uma chamada × paginação, cache ou não): meça cada uma no mesmo banco.
Opções independentes podem ir para **subagentes em paralelo**, cada um com uma forma, devolvendo tempo e memória
nos três tamanhos. A escolha, com a tabela de números, vira ADR (`/sys10-06-escrever-adr`). Os spikes não entram no
PR; os números entram.

## 5. No PR

- **Volume:** a tabela que cresce e o tamanho no ×10.
- **Números:** tempo e memória antes → depois, nos três tamanhos, e como foram medidos.
- **Guarda:** o teste e o orçamento, ou o porquê de não ter.
- **Plano:** índice novo e o `EXPLAIN` que justifica.

## Como conferir

- Nenhum laço no código sobre linhas de tabela que cresce; nenhuma leitura dela sem filtro.
- Toda consulta nova em tabela que cresce tem índice, visto no plano.
- Medido nos três tamanhos com dado real, com teste de guarda; números no PR.
- A memória da API não cresce com o volume (o ×10 não usa 10× a memória).
