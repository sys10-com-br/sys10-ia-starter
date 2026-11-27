---
name: sys10-01-registrar-reuniao
description: Use quando uma reunião com o cliente acabou e precisa entrar no repo (transcrição e link do protótipo mostrado); também quando alguém pede "salva a transcrição da reunião de hoje" ou "registra a reunião de X".
---

# Registrar a reunião

Leia primeiro `.claude/skills/_comum/regras.md`.

## Entrada

A data (ou "hoje"), o nome da reunião e, se houve, o link do protótipo mostrado. Pergunte o que faltar,
uma pergunta por vez.

## Passos

1. **Ache a transcrição.** Pela agenda do dia, pelo Drive ou pela ferramenta de gravação (Meet, Read AI,
   Teams). Se houver duas transcrições da mesma reunião, salve as duas: o reconhecimento de fala erra em
   lugares diferentes, e uma confere a outra. Se não houver nenhuma, **pare**: não crie arquivo vazio.
2. **Classifique.** Pergunte o tipo (`levantamento`, `validacao`, `apresentacao`, `ajustes`). A pasta é
   `discovery/reunioes/<AAAA-MM-DD>-<tipo>/`.
3. **Salve `transcricao.md`** como veio, sem editar, com um cabeçalho:
   ```
   ---
   titulo: <título da reunião>
   data: AAAA-MM-DD
   participantes: <nomes>
   fonte: <link do documento original>
   gravacao: <link>
   ---
   > Transcrição automática, copiada sem edição. Pode ter erros de reconhecimento de fala.
   ```
   **Mascare senhas:** o que vier depois de "senha", "password" ou "PIN" vira `***`.
4. **Referencie o protótipo, sem copiar.** `prototipo.md` com o link, a versão mostrada e a lista de
   telas. Sem protótipo: "Nenhum protótipo foi apresentado nesta reunião."
5. **Atualize a tabela** "Reuniões" de `discovery/README.md`: data, nome, link da transcrição, ata
   `a fazer`.
6. **Git:** branch `docs/reuniao-<AAAA-MM-DD>-<tipo>`, commit `docs: transcrição da reunião de DD/MM`, PR.

## Como conferir

- O cabeçalho tem `fonte:` preenchido; nenhuma senha em claro (`grep -i senha transcricao*.md`).
- A tabela de `discovery/README.md` tem a linha nova e os links abrem.
- Próximo passo: `/sys10-02-ata`.
