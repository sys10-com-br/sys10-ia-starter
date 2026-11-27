# Trabalho em paralelo

Vale quando várias pessoas, ou várias sessões do Claude, trabalham no mesmo repositório ao mesmo tempo.

- **Uma worktree por tarefa** (`git worktree add ../<repo>-<assunto> -b <tipo>/<assunto> origin/main`). Duas
  sessões no mesmo checkout se atropelam.
- **Não mexa na branch nem na worktree de outra sessão.** Precisa de algo de lá? Peça, ou parta da branch dela.
- **Nada de `git stash` puro:** a pilha é compartilhada entre worktrees. Prefira um commit temporário.
- **ID que nasce no código é gerado na hora, nunca "o próximo da sequência":** ADR por data e hora UTC
  (`date -u +%y%m%d-%H%M`), migration por timestamp real, GUID por `uuidgen`. Duas branches escolhem o mesmo
  "próximo" e o merge ou o deploy quebra.
- **O andamento sai do código e do Git**, não do quadro de tarefas: o que está na `main`, o que está em branch
  aberta, o que tem PR. O card pode estar desatualizado; quando divergir, diga.
- **Merge frequente, PR pequeno:** branch que vive dias acumula conflito com todas as outras.
- **Arquivo muito disputado** (`CLAUDE.md`, rotas, registro de dependências): mude pouco por PR e faça o merge
  rápido.
