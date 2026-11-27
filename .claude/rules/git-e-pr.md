# Git e pull requests

- **Nada direto na `main`.** Toda mudança, inclusive de documentação, entra por branch e PR.
- **Branch** `<tipo>/<assunto-em-kebab-case>`, sem acento. **Commit** `<tipo>: <descrição>`, com o mesmo tipo:
  `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `perf`, `ci`.
- **Um commit por tarefa:** se a branch junta várias, cada uma vira um commit.
- **Pergunte o destino antes de abrir o PR** (ou de fazer merge). Nunca escolha sozinho.
- **PR pelo modelo** (`.github/pull_request_template.md`): o porquê, regras antes → depois com a fonte,
  diferenças do design, como foi testado rodando, link do card.
- **Link clicável** sempre que citar PR, commit, card ou documento; nunca só o número.
- **Ao terminar, deixe tudo sincronizado** no mesmo trabalho: docs da regra (`MU-NNN`), protótipo se a tela final
  mudou por decisão de quem decide, card com o link do PR, e o que precisa subir junto no deploy, escrito no PR.
