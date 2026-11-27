# Checklist de revisão de uma tela

Quem revisa roda tudo, na ordem, com o PR, a ficha e o protótipo abertos. O **Nível** é a gravidade quando o item
falha: vem desta tabela, não da opinião de quem revisa.

| Nível | O que acontece |
|---|---|
| CRITICAL, HIGH | Volta ao autor. O PR não segue |
| MEDIUM | Corrija quando der; se ficar, vai escrito no veredito |
| LOW | Registra e segue |

## 1. Portão e contrato do PR

| # | Item | Nível |
|---|---|---|
| 1.1 | A tela está aprovada no protótipo, ou o PR registra o "sim" de quem decide, com data | CRITICAL |
| 1.2 | O corpo do PR segue o modelo, sem seção apagada (vazia diz "—" e por quê) | HIGH |
| 1.3 | Link do card no PR | MEDIUM |

## 2. Fluxos e estados

| # | Item | Nível |
|---|---|---|
| 2.1 | Todo fluxo da ficha está implementado de ponta a ponta, ou o PR diz qual fica para depois e por quê | HIGH |
| 2.2 | Os estados existem: carregando, vazio, erro, sem permissão, com o texto da ficha | HIGH |
| 2.3 | Mensagens literais iguais às da ficha | MEDIUM |
| 2.4 | Cada critério de aceite tem um teste com os mesmos valores | HIGH |

## 3. Regra de negócio

| # | Item | Nível |
|---|---|---|
| 3.1 | Nenhuma regra sem fonte no código; lacuna virou `Premissa:` no PR ou `EA` | CRITICAL |
| 3.2 | Regra mudou: ficha, aceites, índice de regras e `MU-NNN` atualizados no mesmo PR | HIGH |

## 4. Permissões (preencha com as do seu projeto)

| # | Item | Nível |
|---|---|---|
| 4.1 | <ex.: endpoint novo exige a permissão certa; usuário sem permissão recebe 403> | HIGH |

## 5. Invariantes e arquitetura (preencha com os do `CLAUDE.md`)

| # | Item | Nível |
|---|---|---|
| 5.1 | <invariante do projeto> | CRITICAL |
| 5.2 | Sem N+1: a API devolve a lista pronta; nada de requisição por linha nem consulta num laço | HIGH |
| 5.3 | Dado que cresce: medido no ×10 (`.claude/rules/desempenho-com-volume.md`) | HIGH |

## 6. Tela rodando e protótipo

| # | Item | Nível |
|---|---|---|
| 6.1 | Usada rodando, fluxo a fluxo, com capturas app × protótipo no PR | HIGH |
| 6.2 | Igual ao protótipo (ordem, textos, botões, cores); diferença está no PR com o porquê | HIGH |
| 6.3 | Responsivo nas três larguras, sem rolagem para o lado | HIGH |
| 6.4 | Console do navegador sem erro novo | MEDIUM |

## 7. Vocabulário e código

| # | Item | Nível |
|---|---|---|
| 7.1 | Nenhum termo proibido do glossário na tela nem no código | MEDIUM |
| 7.2 | `.claude/rules/codigo.md` respeitado (colunas, nomes sem abreviar, erros tratados) | MEDIUM |
| 7.3 | Lint, format e testes verdes no CI | HIGH |

## Veredito

Todo achado tem arquivo, linha e o fluxo da ficha:

```
[HIGH] src/web/pages/rooms/RoomList.tsx:142
Fluxo "Ver salas", estado vazio. A ficha pede "Nenhuma sala cadastrada."; a tela mostra a tabela sem linhas.
```

Um de três, sempre com o porquê:

- **`volta ao autor`**: há CRITICAL ou HIGH.
- **`pronto para revisão final`**: nenhum CRITICAL nem HIGH; os MEDIUM e LOW que sobraram vão listados.
- **`falta decisão de produto`**: o mapa mostra uma pergunta que só quem decide responde. Escreva a pergunta no PR,
  abra o `EA` e pare a revisão do mérito até a resposta.
