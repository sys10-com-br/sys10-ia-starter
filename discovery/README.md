# discovery/ — em discussão

Tudo aqui é **conversa em andamento**, não regra. O que vale para implementar está em `docs/`.

## O ciclo

```
reunião → transcrição → ata → protótipo ajustado → nova rodada … → aprovação → docs/
```

1. **Reunião** com o cliente. Grave e transcreva (Meet, Read AI, Teams…).
2. **Transcrição** salva como veio, em `discovery/reunioes/<AAAA-MM-DD>-<tipo>/` (skill `/registrar-reuniao`).
3. **Ata** com cada decisão numerada (`D01`…), com quem disse, o minuto e o trecho (skill `/ata`).
4. **Protótipo** ajustado com o que a ata mandou para o design. Volta para a próxima reunião.
5. **Aprovação**: o cliente aprovou a tela. Ela vira ficha em `docs/telas/` (skill `/ficha-de-tela`), por
   PR. O merge de quem decide é a aprovação.

Pendências de qualquer reunião vão para [`em-aberto.md`](em-aberto.md) (skill `/propagar-ata`).

## Reuniões

| Data | Reunião | Transcrição | Ata | Protótipo |
|---|---|---|---|---|
| <DD/MM> | <nome> | <link> | a fazer | <link> |
