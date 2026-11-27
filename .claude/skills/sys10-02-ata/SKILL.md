---
name: sys10-02-ata
description: Use quando uma reunião já tem a transcrição em discovery/ e a ata está "a fazer"; também quando alguém pede "faz a ata", "o que decidimos na reunião de X" ou "lista as decisões da transcrição".
---

# Escrever a ata

Leia primeiro `.claude/skills/_comum/regras.md`.

Modelo: `discovery/_modelos/ata.md`.

## Entrada

A pasta da reunião. Sem ela, liste as reuniões com ata "a fazer" em `discovery/README.md` e pergunte.

## Passos

1. **Leia a transcrição inteira**, até o fim. Transcrição grande vai para um subagente, que devolve o
   checklist abaixo; nunca resuma sem ler tudo. Decida cada ponto **pela fala**, nunca pelo resumo
   automático da ferramenta.
2. **Extraia as decisões.** Para cada uma: ID (`D01`…), tipo (MUDAR, CONFIRMADO, REMOVER, NOVO,
   EM ABERTO), natureza (`produto/tela` ou `técnica`), o que foi decidido (concreto e checável), quem
   disse, o minuto e um trecho literal curto. Ambíguo vira EM ABERTO. Defina com o time quem tem a palavra
   final em ponto ambíguo e escreva no `CLAUDE.md`.
3. **Converta o vocabulário.** A transcrição vem com os termos falados; a ata usa os termos do sistema
   (glossário do projeto, se houver).
4. **Preencha a ata** no modelo: Pauta, Decidido (com "Afeta": `tela › fluxo`, `transversal`, `EA-NNN`,
   `design` ou `ADR`), Enviado ao design, Não vira tela, Pendências, Próxima reunião.
5. **Marque a ata como feita** na tabela de `discovery/README.md`.
6. **Git:** na branch da reunião, commit `docs: ata da reunião de DD/MM`. Push; PR se ainda não houver.

## Como conferir

- Toda linha de "Decidido" tem minuto, tipo e natureza.
- Nenhum "a definir" sem `EA novo` ou `EA-NNN`.
- Próximo passo: `/sys10-03-propagar-ata`.
