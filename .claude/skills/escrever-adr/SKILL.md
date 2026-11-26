---
name: escrever-adr
description: Use quando uma decisão técnica precisa virar ADR — um candidato do índice de docs/arquitetura/decisoes/ ou uma decisão que nasceu construindo uma tela e que outras partes vão herdar; também quando alguém pede "escreve o ADR de X" ou "isso precisa de ADR?".
---

# Escrever um ADR

**Decisão técnica relevante vira ADR, investigada antes de escrita.** O merge do PR é a aprovação.
Modelo: `docs/arquitetura/decisoes/_modelo-adr.md` (MADR).

## Precisa de ADR?

Sim, quando a decisão é **técnica** e outra parte do sistema vai herdar (formato de dados, contrato de API,
convenção) ou custa caro desfazer (modelo de dados com volume, biblioteca base). Não: ajuste local,
nome de variável. Na dúvida, escreva: ADR curto não custa nada.

**Regra de negócio não é ADR** (quem pode, quando bloqueia): é `EA` para quem decide. O ADR decide **como**
cumprir a regra, nunca **qual** é.

## Passos

1. **Problema.** Em duas ou três frases: o que precisa ser decidido e por que agora (o que trava). Liste
   os fatores: invariantes do `CLAUDE.md`, volume, offline, custo de mudar depois.
2. **Investigue.** Como o código trata isso hoje. No mínimo **duas opções reais**, cada uma com como
   funciona e o que muda no banco e no código. Dúvida de desempenho: spike descartável, medido com dado
   real; no ADR entram os números, não o spike.
3. **Decida** pelos fatores e diga por que as outras perderam. Se a escolha muda o que o usuário vê, pare e
   pergunte. ADR aceito não se edita: escreva um novo e marque o antigo `substituida-por-<ID>`.
4. **Escreva.** ID `ADR-AAMMDD-HHmm` gerado com `date -u +%y%m%d-%H%M` na hora (nunca escolhido nem
   arredondado: evita colisão entre branches). Arquivo `ADR-AAMMDD-HHmm-<assunto>.md`. Atualize o índice e
   feche o `EA` de origem.
5. **PR.** Branch `docs/adr-<assunto>`, commit `docs: ADR-AAMMDD-HHmm <título>`. Se trava uma tela, vai em PR
   próprio, antes dela. Pergunte o destino antes de abrir.

## Como conferir

- Problema, fatores e pelo menos duas opções, cada uma com o porquê.
- Nenhuma regra de negócio decidida; nenhum invariante quebrado.
