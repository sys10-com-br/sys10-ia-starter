---
name: sys10-07-desempenho-com-volume
description: Use para medir o desempenho de código que lê, calcula, grava ou transfere dado que cresce com o uso, antes do PR, ou para comparar formas de fazer com números. Também quando alguém diz "está lento", "isso aguenta o cliente grande?", "a API caiu por memória", "mede isso" ou "qual opção é mais rápida?".
---

# Medir desempenho com volume

Leia primeiro `.claude/skills/_comum/regras.md`.

As regras de desenho (o tamanho dos dados e como escrever o código para ele) estão na instrução
`.claude/rules/desempenho-com-volume.md`. Esta skill é o passo a passo de **medir** com dado real, **comparar**
opções e **mostrar os números** no PR.

## 1. Medir com dado real

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

## 2. Mais de um jeito? Compare e decida em ADR

Dúvida real entre formas (memória × banco, uma chamada × paginação, cache ou não): meça cada uma no mesmo banco.
Opções independentes podem ir para **subagentes em paralelo**, cada um com uma forma, devolvendo tempo e memória
nos três tamanhos. A escolha, com a tabela de números, vira ADR (`/sys10-06-escrever-adr`). Os spikes não entram no
PR; os números entram.

## 3. No PR

- **Volume:** a tabela que cresce e o tamanho no ×10.
- **Números:** tempo e memória antes → depois, nos três tamanhos, e como foram medidos.
- **Guarda:** o teste e o orçamento, ou o porquê de não ter.
- **Plano:** índice novo e o `EXPLAIN` que justifica.

## Como conferir

- Medido nos três tamanhos (real, ×4, ×10) com dado real, antes e depois, em banco local.
- Toda consulta nova em tabela que cresce foi vista no plano.
- Teste de guarda com orçamento, ou o porquê de não ter, no PR.
- Opções comparadas com números viraram ADR.
