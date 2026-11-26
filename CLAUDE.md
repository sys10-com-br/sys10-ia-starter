# CLAUDE.md

Guia para o Claude Code neste repositório. Preencha os `<...>` e apague o que não se aplica.

## Estado do repositório

<O que é o sistema, para quem, em uma ou duas frases. O que já tem código e o que ainda não tem.>

- **Stack:** <ex.: .NET 10 + Postgres no backend, React + Vite no web>
- **Idioma do código:** <ex.: inglês nos identificadores; mensagens ao usuário em português>

### Comandos

```bash
<comando de build>
<comando para rodar a aplicação>       # ex.: http://localhost:5173
<comando de teste>
<comando de teste isolado>
<comando de lint/format do CI>
```

## Onde está cada coisa

| Pasta | Etapa | O que tem |
|---|---|---|
| `discovery/` | **Em discussão** | Reuniões, transcrições, atas e pendências (`em-aberto.md`). Não é regra |
| `docs/` | **Decidido** | Fichas de tela (`docs/telas/`), ADRs, mudanças (`docs/projeto/mudancas.md`) |
| `src/` | **Código** | <pastas do backend, web, app> |
| Protótipo | **Decidido** | <onde fica o protótipo aprovado: link do Figma/Claude Design> |

- Pendências: `discovery/em-aberto.md` (`EA-NNN`).
- Decisões técnicas: `docs/arquitetura/decisoes/` (`ADR-AAMMDD-HHmm`).
- Decisões mortas que não podem voltar: `docs/projeto/mudancas.md` § "Descontinuado — não usar".

## Regras de trabalho

- **Só implemente regra que está em `docs/`.** Regra sem fonte (ata, protótipo, doc) vira `EA-NNN` em
  `discovery/em-aberto.md` e pergunta a <quem decide: PO, cliente>. Nunca suponha.
- **Teste rodando antes de dizer pronto.** Teste automatizado não basta: suba a aplicação e use a tela no
  navegador (Playwright) ou o app no emulador, no fluxo que mudou, e compare com o protótipo por captura.
  Se não der para rodar, diga isso com todas as letras e o que ficou sem teste.
- **Nada direto na `main`.** Toda mudança entra por branch `<tipo>/<assunto-em-kebab-case>` e PR. Commit
  `<tipo>: <descrição>` (`feat`, `fix`, `docs`, `refactor`, `test`, `chore`). Pergunte o destino antes de
  abrir o PR.
- **Mudou regra, atualiza o doc no mesmo PR.** O código que cria, altera ou remove uma regra de negócio
  atualiza a ficha, os critérios de aceite e registra um `MU-NNN` em `docs/projeto/mudancas.md`. O PR lista
  as regras mudadas (antes → depois, com a fonte).
- **ID de ADR pela data e hora UTC:** `ADR-AAMMDD-HHmm`, gerado com `date -u +%y%m%d-%H%M` na hora em que o
  ADR nasce. Número sequencial colide entre branches em paralelo.
- **Tela segue o protótipo.** Abra o protótipo no mesmo estado e copie a estrutura: ordem, textos literais,
  botões. Diferença vai no PR como "Diferença do design", com o porquê.
- **Desempenho com volume: desenhe e meça para o maior cliente ×10.** Tudo que lê, calcula, grava ou transfere
  dado que cresce segue a instrução `.claude/rules/desempenho-com-volume.md` (cálculo no banco, nada da tabela
  inteira na memória da API, índice para filtro e ordenação, escrita em lote) e é medido com
  `/sys10-07-desempenho-com-volume` (dado real ×1, ×4 e ×10, teste de guarda, números no PR).
- <Regra do seu projeto. Ex.: "Migrations com timestamp até o minuto, nunca número redondo.">

## Volumes de referência

| Referência | Volume |
|---|---|
| <Maior cliente real: tabela principal> | <ex.: 50 mil linhas> |
| O mesmo ×10 (o que o código tem que aguentar) | <ex.: 500 mil linhas> |
| Memória da API em produção | <ex.: 512 MB> |

## Invariantes

O que o código nunca pode quebrar, com a fonte. Cada invariante tem um teste de guarda.

<!-- Exemplo (apague e escreva os seus):
- **Pedido faturado não volta para rascunho.** Estado terminal. Fonte: ata 10/03 D07.
  Guarda: `OrderStateTests.InvoicedIsTerminal`.
-->

## Erros que viraram regra

Cada vez que o Claude errar, escreva aqui a regra, a data e o teste de guarda, para não repetir.

<!-- Exemplo:
- **Leitura não abre transação** (15/03): o pool de conexões travou em produção.
  Guarda: `QueryHandlerTransactionTests`.
-->
