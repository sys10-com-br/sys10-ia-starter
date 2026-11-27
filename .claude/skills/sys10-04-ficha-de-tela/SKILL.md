---
name: sys10-04-ficha-de-tela
description: Use quando uma tela tem protótipo aprovado e atas com decisões e precisa virar ficha em docs/telas/ para ser implementada; também quando alguém pede "faz a ficha da tela X" ou "atualiza a ficha com a reunião de X".
---

# Ficha de tela

Leia primeiro `.claude/skills/_comum/regras.md`.

**É aqui que a tela vira regra.** Uma ficha por tela, em `docs/telas/`, a partir das atas e do protótipo.
Entra por PR; **o merge de quem decide é a aprovação**. Modelo: `docs/telas/_modelo-tela.md`.

## Entrada

A tela (nome, rota ou link do protótipo) e, se houver, as atas. Sem atas indicadas, use todas em que a
coluna "Afeta" cita a tela.

## Passos

1. **Portão.** A tela está aprovada no protótipo? Se ainda está em rodada com o cliente, avise e só siga
   com o "sim" de quem decide.
2. **Ache a ficha.** O caminho espelha a rota (`/orders/:id` → `docs/telas/orders/{id}.md`). Se existe,
   **atualize**: não reescreva o que já foi aprovado sem registrar um `MU-NNN`.
3. **Leia o protótipo** no estado de cada fluxo (popups, abas, passos). Arquivo grande, por subagente.
   Anote textos literais e os selos de "a validar": o que está atrás de selo não está aprovado.
4. **Leia as decisões.** Cada regra da ficha cita a fonte (`ata DD/MM · Dnn`, protótipo). Sem fonte, não
   entra: vira EA (como na `/sys10-03-propagar-ata`).
5. **Fatie em fluxos.** Um fluxo é o que um dev entrega sozinho e quem decide testa sozinho: "Ver …" e
   depois cada ação (criar, editar, excluir…). Para cada fluxo: quem, quando aparece, regras com fonte,
   mensagens literais e aceite em "Dado / quando / então" **com valores concretos**.
6. **Não repita.** Regra de mais de uma tela mora num arquivo transversal de `docs/`; a ficha aponta.
7. **Git:** branch `docs/tela-<slug>`, commit `docs: ficha da tela <Título>`, PR com "Por quê", fluxos e
   regras, "Em aberto" e "Como conferir". Diga que **o merge aprova a ficha**.

## Como conferir

- Todo fluxo tem aceite com valores concretos; toda regra tem fonte.
- Nenhum "a definir" sem EA.
- Próximo passo: `/sys10-05-implementar-tela`.
