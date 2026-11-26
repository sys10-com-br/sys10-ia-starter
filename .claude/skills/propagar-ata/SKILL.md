---
name: propagar-ata
description: Use depois que a ata está escrita e as pendências e decisões técnicas dela ainda não viraram EA ou candidato a ADR; também quando alguém pede "registra as pendências da ata" ou "atualiza o em-aberto com a reunião de X".
---

# Propagar a ata

Leva da ata o que **não é de uma tela só**: pendências, regras transversais, vocabulário e decisões
técnicas. O que é de uma tela fica na ata e entra na ficha pela `/ficha-de-tela`. A mudança vai direto para
`docs/` numa branch: **o merge de quem decide é a aprovação**.

## Entrada

O caminho da `ata.md`. Trabalhe só com "Decidido", "Não vira tela" e "Pendências".

## Passos

1. **Último EA:** `grep -o "EA-[0-9]*" discovery/em-aberto.md | sort -u | tail -1`.
2. **Pendências → EA.** Cada linha de "Pendências" e cada EM ABERTO: se já existe um EA sobre o assunto,
   acrescente a fonte nova; senão, crie `EA-<próximo>` em `discovery/em-aberto.md` com pergunta objetiva,
   dono, impacto e fonte (`ata DD/MM · Dnn`). Se trava um fluxo, escreva "bloqueia: <tela> › <fluxo>".
3. **Regra de mais de uma tela → `docs/`**, no arquivo de regras transversais do projeto, com a fonte.
   Regra de uma tela só não entra aqui.
4. **Mudou algo aprovado → MU.** Se a decisão contradiz o que está em `docs/`, altere o trecho e registre
   `MU-<próximo>` em `docs/projeto/mudancas.md` (e em "Descontinuado — não usar", se a regra antiga morreu).
5. **Natureza `técnica` → candidato a ADR.** Uma linha no índice de `docs/arquitetura/decisoes/` com status
   `candidato` e ID `ADR-AAMMDD-HHmm` (`date -u +%y%m%d-%H%M`), mais um EA apontando para ela. **Não escreva
   o ADR**: é da `/escrever-adr`.
6. **Feche o laço na ata:** troque `EA novo` pelo ID criado.
7. **Git:** um commit por arquivo tocado (`docs: pendências da reunião de DD/MM (EA-NNN a EA-NNN)`). No PR,
   liste o que mudou em `docs/`.

## Como conferir

- `grep -o "EA-[0-9]*" discovery/em-aberto.md | sort | uniq -d` vazio (sem ID repetido).
- A ata não tem mais `EA novo`; toda mudança em algo aprovado tem MU com fonte.
