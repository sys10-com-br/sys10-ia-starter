# Git e pull requests

## Ambientes

| Ambiente | Branch | Endereço | Banco |
|---|---|---|---|
| Desenvolvimento | a da tarefa, na máquina de cada um | `localhost` | cópia local |
| <Staging> | `<staging>` | `<url>` | `<banco do staging>` |
| Produção | `main` | `<url>` | `<banco de produção>` |

- **Fluxo:** a branch nasce da `main`, o PR vai para a `<staging>`, e a `<staging>` é promovida para a `main` por
  PR. Nada chega em produção sem passar pelo staging. Hotfix: PR direto na `main`, depois `main` → `<staging>`.
- **Feature quebrada no staging é revertida** (`git revert` do merge), nunca com reset ou force push.
- **Produção é produção:** nada de escrever direto no banco de produção sem pedido explícito, e sempre com backup
  antes.

## Branches, commits e PRs

- **Nada direto na `main`.** Toda mudança, inclusive de documentação, entra por branch e PR.
- **Branch** `<tipo>/<assunto-em-kebab-case>`, sem acento. **Commit** `<tipo>: <descrição>`, com o mesmo tipo:
  `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `perf`, `ci`.
- **Um commit por tarefa:** se a branch junta várias, cada uma vira um commit.
- **Pergunte o destino antes de abrir o PR** (ou de fazer merge). Nunca escolha sozinho.
- **PR pelo modelo** (`.github/pull_request_template.md`): o porquê, regras antes → depois com a fonte,
  diferenças do design, como foi testado rodando, link do card.
- **Link clicável e resumo** sempre que citar PR, commit, card ou documento: `[#42](url) (Ana, filtro da agenda)`,
  nunca só "#42". Ninguém guarda o que é cada número.
- **Ao terminar, deixe tudo sincronizado** no mesmo trabalho: docs da regra (`MU-NNN`), protótipo se a tela final
  mudou por decisão de quem decide, card com o link do PR, e o que precisa subir junto no deploy, escrito no PR.
