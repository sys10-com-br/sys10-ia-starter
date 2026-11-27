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
| `docs/` | **Decidido** | Fichas de tela (`telas/`), regras do sistema (`produto/`), projeto (`projeto/`), ADRs |
| `src/` | **Código** | <pastas do backend, web, app> |
| Protótipo | **Decidido** | <onde fica o protótipo aprovado: link do Figma/Claude Design> |

- **Leia antes de qualquer trabalho de domínio:** `docs/projeto/visao-geral.md`, `docs/produto/glossario.md`
  (como cada coisa se chama), `docs/produto/regras-de-negocio.md`, `docs/produto/parametros.md` e as máquinas de
  estados em `docs/produto/`.
- Os três livros: o que falta decidir (`discovery/em-aberto.md`, `EA-NNN`), o que mudou depois de decidido
  (`docs/projeto/mudancas.md`, `MU-NNN`) e o que pode dar errado (`docs/projeto/riscos.md`, `RI-NNN`).
- Decisões técnicas: `docs/arquitetura/decisoes/` (`ADR-AAMMDD-HHmm`).
- Specs e planos do Claude Code: `docs/superpowers/specs/` e `docs/superpowers/plans/` (registros datados, não se
  editam depois).
- Decisões mortas que não podem voltar: `docs/projeto/mudancas.md` § "Descontinuado — não usar".

## Regras de trabalho

- **Só implemente regra que está em `docs/`.** Regra sem fonte (ata, protótipo, doc) vira `EA-NNN` em
  `discovery/em-aberto.md` e pergunta a <quem decide: PO, cliente>. Nunca suponha.
- **Mudou regra, atualiza o doc no mesmo PR.** O código que cria, altera ou remove uma regra de negócio
  atualiza a ficha, os critérios de aceite e registra um `MU-NNN` em `docs/projeto/mudancas.md`. O PR lista
  as regras mudadas (antes → depois, com a fonte).
- **ID de ADR pela data e hora UTC:** `ADR-AAMMDD-HHmm`, gerado com `date -u +%y%m%d-%H%M` na hora em que o
  ADR nasce. Número sequencial colide entre branches em paralelo.
- <Regra do seu projeto.>

## Instruções por tema (`.claude/rules/`)

O Claude carrega estes arquivos junto com este. Os que têm `paths:` só entram quando ele mexe naqueles arquivos.

| Arquivo | Quando vale |
|---|---|
| `verificacao.md` | Sempre: pronto é rodando, não só teste verde |
| `git-e-pr.md` | Sempre: branch, commit, PR e "deixe tudo sincronizado" |
| `seguranca.md` | Sempre: segredos, dado pessoal, ação externa com confirmação |
| `codigo.md` | No código: formatação, nomes, erros, validação |
| `telas.md` | No front: protótipo, design system, estados |
| `banco-e-migrations.md` | No backend: migrations, IDs, transação |
| `trabalho-em-paralelo.md` | Sempre: worktrees, IDs gerados na hora, andamento pelo Git |
| `autonomia.md` | Sempre: plano aprovado vai até o fim; quando parar |
| `discovery.md` | Em `discovery/` e `docs/`: 1:1 nunca é fonte, vocabulário pelo glossário, histórico |
| `desempenho-com-volume.md` | No código que mexe com dado que cresce (medir com `/sys10-07-desempenho-com-volume`) |

## Como as regras evoluem

Cada erro vira regra, e a regra sobe de degrau até não depender de alguém lembrar:

1. **Conversa:** a correção vale só para aquela sessão.
2. **Memória pessoal:** vale para quem corrigiu, em todas as sessões dele.
3. **Instrução do projeto** (`CLAUDE.md` ou `.claude/rules/`, por PR): vale para o time todo.
4. **Guarda automática** (teste, lint, hook): vale mesmo se ninguém ler a instrução.

- **Formato:** `**<regra>** <porquê> (<quem pediu>, <AAAA-MM-DD>) · Guarda: <teste/lint/hook>`.
- **Onde mora:** este arquivo é o mapa (o que é, onde está, regras de produto); regra técnica de um tema vai para
  `.claude/rules/<tema>.md`; processo que se repete vira skill; regra de negócio vai para `docs/`.
- **Revisão:** a cada <mês>, e quando este arquivo passar de ~200 linhas. Use `/sys10-08-nova-regra` para registrar
  e revisar, e `/revise-claude-md` no fim de uma sessão que ensinou algo.

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
