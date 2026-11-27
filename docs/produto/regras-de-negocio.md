---
id: REGRAS
titulo: Regras de negócio transversais e índice
dono: <PO>
atualizado: AAAA-MM-DD
---

# Regras de negócio

A regra de uma tela fica na ficha dela (`docs/telas/`). Aqui ficam as regras que valem para o sistema inteiro e um
índice para achar qualquer regra.

## Regras transversais

| ID | Regra | Fonte |
|---|---|---|
| RN-0001 | Uma sala não pode ter duas reservas sobrepostas | ata AAAA-MM-DD · D02 |

## Índice por assunto

| Assunto | Regra em uma linha | Onde está | Telas que atravessa |
|---|---|---|---|
| Reservas | Sem sobreposição | RN-0001 | reservas, agenda |

## Manutenção

Uma regra tem um ID e um lugar só. Regra escrita em dois lugares é erro: deixe o texto onde ela mora e só o ponteiro
aqui. Mudou uma regra aprovada: `MU-NNN` em `docs/projeto/mudancas.md`.
