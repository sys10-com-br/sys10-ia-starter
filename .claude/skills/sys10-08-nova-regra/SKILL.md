---
name: sys10-08-nova-regra
description: Use quando o Claude errou e foi corrigido, quando alguém diz "isso não pode acontecer de novo", "guarda isso como regra", "sempre faça X", "nunca faça Y", quando uma lição da memória pessoal vale para o time, ou na revisão periódica das instruções (.claude/rules e CLAUDE.md).
---

# Registrar uma regra nova (ou revisar as que existem)

Leia primeiro `.claude/skills/_comum/regras.md` e a seção "Como as regras evoluem" do `CLAUDE.md`.

**Cada erro vira regra, e a regra sobe de degrau até não depender de lembrar.**

## Entrada

O erro ou o pedido (o que aconteceu, o que devia ter acontecido) e quem pediu. Na revisão periódica: nada.

## Passos para uma regra nova

1. **É regra de quê?**
   - **Produto** (o que o sistema aceita, recusa, calcula): não é instrução. Vai para a ficha da tela ou para
     `docs/produto/`, com fonte; sem fonte, `EA`. Pare aqui.
   - **Pessoal** (gosto de quem pediu, vale só na máquina dele): memória pessoal ou `CLAUDE.local.md`. Pare aqui.
   - **Técnica ou de processo que vale para o time:** siga.
2. **Já existe?** Procure em `CLAUDE.md` e `.claude/rules/` pelo termo. Se existe e não foi seguida, o problema é
   onde ela está ou como está escrita: mova para um lugar que carregue na hora certa (`paths:`) ou reescreva mais
   claro. Não duplique.
3. **Onde mora.** Uma linha de mapa ou de processo vale sempre → `CLAUDE.md`. Regra de um tema → o arquivo do tema
   em `.claude/rules/`, com `paths:` se só vale para uma parte do código. Tema novo com 3 ou mais regras → arquivo
   novo, e uma linha na tabela de instruções do `CLAUDE.md`.
4. **Escreva no formato:**
   ```
   - **<A regra, no imperativo.>** <O porquê, numa frase: o que deu errado.> (<quem pediu>, <AAAA-MM-DD>)
     Guarda: <teste, lint, hook ou "nenhuma ainda">.
   ```
5. **Suba um degrau, quando der.** A regra mais forte é a que a máquina confere:
   - **teste de guarda** que falha se o erro voltar (ex.: um teste que procura transação em leitura);
   - **lint ou formatador** (`.editorconfig`, regra do linter);
   - **hook** do Claude Code em `.claude/settings.json` que bloqueia a ação (ex.: commit direto na `main`).
   Proponha a guarda; escreva o teste se for pequeno.
6. **Memória pessoal que vale para o time:** se a lição estava só na memória de alguém, traga para cá e diga a essa
   pessoa que pode apagar a dela.
7. **Git:** branch `docs/regra-<assunto>`, commit `docs: regra <resumo>`, PR. O merge é a aprovação do time.

## Revisão periódica (a cada <mês> ou quando o `CLAUDE.md` passar de ~200 linhas)

- Regra que ninguém mais precisa ou que a guarda já cobre por inteiro: saia, e ganhe uma linha em
  `docs/projeto/mudancas.md` § "Descontinuado — não usar" se alguém pode querer voltar a ela.
- Regra repetida em dois lugares: fica em um, o outro aponta.
- Arquivo de `.claude/rules/` com mais de ~60 linhas: divida por tema ou por `paths:`.
- Rode o `/revise-claude-md` e o `claude-md-improver` (plugin `claude-md-management`) para o `CLAUDE.md`.

## Como conferir

- A regra está em um lugar só, no formato, com porquê, data e quem pediu.
- Regra de produto não entrou em `.claude/rules/`.
- A guarda foi escrita ou proposta.
