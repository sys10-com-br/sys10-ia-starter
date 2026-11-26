---
tela: <slug-da-tela>
rota: </rota/:id>
prototipo: <link da tela aprovada e versão>
permissao: <feature/permissão, ou EA-NNN>
---

# <Título da tela>

<Para que serve, quem usa e em que momento, em duas linhas.>

## Fluxo: Ver <a lista/o detalhe>

**Quem:** <perfil>. **Quando aparece:** <condição>.

### Regras

| # | Regra | Fonte |
|---|---|---|
| 1 | <ex.: a lista abre filtrada em "Pendentes"> | ata DD/MM · D01 |
| 2 | <ex.: ordenada pela data, mais recente primeiro> | protótipo v3 |

### Mensagens

| Quando | Texto literal |
|---|---|
| Lista vazia | "<Nenhum pedido pendente.>" |
| Erro ao carregar | "<Não foi possível carregar. Tente de novo.>" |

### Critérios de aceite

- **Dado** 3 pedidos pendentes e 2 faturados, **quando** abro a tela, **então** vejo os 3 pendentes, do
  mais recente para o mais antigo.
- **Dado** nenhum pedido pendente, **quando** abro a tela, **então** vejo "Nenhum pedido pendente."

## Fluxo: <Ação: criar, editar, cancelar…>

<Mesma estrutura: quem, quando, regras com fonte, mensagens, aceites.>

## Em aberto

| EA | Pergunta | Fluxo |
|---|---|---|

## Notas técnicas

<Escritas pelo dev antes do código.>

- **Componentes → endpoint → handler → tabelas**, por fluxo.
- **Estados:** carregando, vazio, erro, sem permissão.
- **Dados:** tabelas, colunas e migrations novas.
- **Premissas:** lacuna pequena resolvida de forma conservadora, rotulada `Premissa:`.
