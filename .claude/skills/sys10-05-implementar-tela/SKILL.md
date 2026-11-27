---
name: sys10-05-implementar-tela
description: Use quando uma tela vai ser implementada, entregue ou revisada — do portão ao PR, rodando a aplicação no navegador e conferindo com o protótipo; também quando alguém pede "implementa a tela X", "a tela está pronta?" ou "o que falta para abrir o PR?".
---

# Implementar uma tela

Leia primeiro `.claude/skills/_comum/regras.md`.

**Da tela aprovada até o PR.** Teste verde não é tela pronta: a tela está pronta quando foi **usada no
navegador** e bate com o protótipo em todas as larguras.

Leia primeiro o `CLAUDE.md` e as instruções de `.claude/rules/` (`verificacao.md`, `telas.md`, `codigo.md`;
valem acima desta skill) e a ficha da tela em
`docs/telas/`, se já existir.

## 1. Portão

| Situação | O que fazer |
|---|---|
| Tela aprovada no protótipo | Siga |
| Tela ainda em rodada com o cliente | **Pare e pergunte** a quem decide |
| Regra que nem ata, nem `docs/`, nem protótipo respondem | `EA` em `discovery/em-aberto.md`; se trava o fluxo, pergunte antes de codar |

Branch `feat/<slug-da-tela>` a partir da `main` atualizada.

## 2. Mapa da tela

Antes do código, a ficha em `docs/telas/` (como na `/sys10-04-ficha-de-tela`), na própria branch:

- **Para quem usa:** fluxos, regras com fonte, mensagens literais, aceites "Dado / quando / então".
- **Por dentro ("Notas técnicas"):** componentes → endpoint → handler → tabelas, por fluxo; os estados
  (carregando, vazio, erro, sem permissão); dados e migrations novos; premissas rotuladas `Premissa:`.
- **Decisão técnica que outras partes vão herdar** (formato de dados, contrato de API, biblioteca base):
  pare e rode `/sys10-06-escrever-adr` se ela trava o fluxo; senão, aponte o candidato no PR.

Leia também a tela vizinha já pronta: componente que existe é reaproveitado.

## 3. Implementar com TDD

- Um passo por fluxo, backend antes do front. Tela com mais de dois fluxos ganha um plano em
  `docs/superpowers/plans/` (`superpowers:writing-plans`).
- **Cada critério de aceite vira teste com os mesmos valores** da ficha: vermelho, depois verde.
- Cor, fonte, botão e ícone saem do design system, nunca de decisão na tela.
- **Volume:** fluxo sobre dado que cresce segue `.claude/rules/desempenho-com-volume.md` e é medido com
  `/sys10-07-desempenho-com-volume` (×1, ×4 e ×10, teste de guarda, números no PR).
- Build, testes e lint verdes antes do passo 4.

## 4. Rodar e usar no navegador (obrigatório)

1. Suba a aplicação (comandos no `CLAUDE.md`) com dados reais de teste, nunca inventados.
2. Com o **Playwright**, percorra cada fluxo e cada aceite como o usuário faria. Provoque cada estado:
   carregando, vazio, erro, sem permissão. Console do navegador sem erro novo.
3. **Compare com o protótipo, lado a lado, por captura**, no mesmo estado: ordem, espaçamento, textos
   literais, botões, cores. Diferença achada é bug: corrija e capture de novo.
4. Repita em **1440 × 900, 820 × 1180 e 390 × 844**. A página nunca rola para o lado; nada cortado.
5. App mobile: o mesmo no emulador.
6. Capturas fora do repo; anexe no PR.

Não deu para rodar (sem banco, sem login, sem emulador)? Diga isso com todas as letras e o que ficou sem
teste. Nunca diga "pronto" só com testes automatizados.

## 5. PR com contrato

**Pergunte o destino antes de abrir.** O corpo segue `.github/pull_request_template.md`. Falta um item,
o PR não está pronto:

1. Todos os fluxos da ficha, com todos os estados.
2. Um teste por critério de aceite, com os mesmos valores.
3. Usado no navegador e comparado com o protótipo nas três larguras, com capturas.
4. Premissas declaradas; dúvida de produto virou `EA`.
5. Regras mudadas (antes → depois, com fonte), com a ficha e o `MU-NNN` atualizados no mesmo PR.
6. Diferenças do design, com o porquê.
7. Link do card.

## 6. Revisão

Quem revisa roda a [`checklist.md`](checklist.md) inteira, com o PR, a ficha e o protótipo. Com CRITICAL ou HIGH, o PR
volta ao autor.

## Como conferir

- Mapa escrito antes do código; todo aceite com teste; toda premissa rotulada.
- Tela usada no navegador nas três larguras, batendo com o protótipo.
