---
id: ESTADOS-<ENTIDADE>
titulo: Máquina de estados de <entidade>
dono: <PO>
atualizado: AAAA-MM-DD
---

# Máquina de estados de <entidade>

Copie para `maquina-de-estados-<entidade>.md` para cada entidade com ciclo de vida.

```
Rascunho ──► Confirmada ──► Concluída
                 └──► Cancelada
```

## Status que o usuário vê

| Status | Estados internos | Onde aparece |
|---|---|---|
| Ativa | Confirmada | lista e agenda |

## Transições

| De → Para | O que a passagem exige | Quem dispara |
|---|---|---|
| Rascunho → Confirmada | Horário livre (RN-0001) | Cliente |

Estados terminais: <Concluída, Cancelada>. Não voltam.

## O que acontece sem mudar de estado

<Eventos que não são fase: ex.: "lembrete enviado". Evita criar estado para o que é evento.>

## Na tela

| Estado | O que a tela mostra |
|---|---|
| Confirmada | Botões Editar e Cancelar |
