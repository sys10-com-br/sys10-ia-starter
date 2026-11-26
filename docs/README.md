# docs/ — decidido

O que está aqui é regra: é o que se implementa. Entra por PR, e o merge de quem decide (PO, cliente) é a
aprovação. O que ainda está em conversa fica em `discovery/`.

| Pasta | O que tem |
|---|---|
| `telas/` | Uma ficha por tela (modelo: [`telas/_modelo-tela.md`](telas/_modelo-tela.md)). O caminho espelha a rota |
| `arquitetura/decisoes/` | ADRs (modelo: [`_modelo-adr.md`](arquitetura/decisoes/_modelo-adr.md)) |
| `projeto/mudancas.md` | Toda mudança em algo já aprovado (`MU-NNN`) e o que foi descontinuado |

## IDs

| Prefixo | O que é | Exemplo |
|---|---|---|
| `Dnn` | Decisão numa ata | `ata 10/03 · D07` |
| `EA-NNN` | Pendência em `discovery/em-aberto.md` | `EA-001` |
| `RN-NNNN` | Regra de negócio numa ficha | `RN-0012` |
| `MU-NNN` | Mudança em algo aprovado | `MU-003` |
| `ADR-AAMMDD-HHmm` | Decisão técnica, data e hora UTC | `ADR-260310-1442` |

**Toda regra cita a fonte.** Sem fonte, não é regra: é `EA`.
