# Regras comuns das skills

Toda skill `sys10-*` lê este arquivo antes do primeiro passo. Vale para todas.

## Onde cada skill escreve

| Skill | Escreve em |
|---|---|
| `sys10-01-registrar-reuniao` | `discovery/reunioes/<AAAA-MM-DD>-<tipo>/` (transcrição, `prototipo.md`), `discovery/README.md` |
| `sys10-02-ata` | `ata.md` da reunião, `discovery/README.md` |
| `sys10-03-propagar-ata` | `discovery/em-aberto.md`, `docs/produto/`, `docs/projeto/mudancas.md`, índice de ADRs |
| `sys10-04-ficha-de-tela` | `docs/telas/`, `docs/produto/` (o que vale para mais de uma tela) |
| `sys10-05-implementar-tela` | `docs/telas/` (mapa), `src/` |
| `sys10-06-escrever-adr` | `docs/arquitetura/decisoes/` |
| `sys10-07-desempenho-com-volume` | testes de desempenho, corpo do PR |
| `sys10-08-nova-regra` | `.claude/rules/`, `CLAUDE.md` |

## Fonte sempre

Toda regra cita de onde veio: `ata AAAA-MM-DD · Dnn`, protótipo (versão), `docs/...`. Frase decisiva vai literal,
entre aspas, com o minuto. Sem fonte: não entra; vira `EA-NNN` em `discovery/em-aberto.md`.

## Desempate

Se as falas divergem, vale `<papel que aprova: PO, cliente>`. Se ele não falou: `EM ABERTO · validar com <papel>`.
Nunca escolha um lado.

## Tipos de decisão

`MUDAR` · `CONFIRMADO` · `REMOVER` · `NOVO` · `EM ABERTO`. Natureza: `produto/tela` ou `técnica` (técnica vira
candidato a ADR).

## Vocabulário

Antes de gravar, converta os termos pela tabela "Termos proibidos" de `docs/produto/glossario.md`. Transcrição vem
com os termos falados, não os do sistema. Todo subagente que lê transcrição recebe essa tabela no prompt.

## Arquivo grande

Transcrição, protótipo e export de design são lidos por subagente, que devolve o resumo. Nunca no contexto
principal.

## Git

Branch `<tipo>/<assunto>` a partir da `main` atualizada, um commit por tarefa, PR. O merge de quem decide é a
aprovação: nada vai para `docs/` sem PR. Com `sem git` no pedido: só edita e lista o que mudou.

## Nunca entra no repo

Senha, token, PIN (mascare com `***`), dado pessoal de cliente, valor comercial.

## Forma

Frases curtas. Tabela com cabeçalho. Nada de "a definir" sem um `EA` ao lado.
