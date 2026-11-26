# Starter kit: trabalhar com IA (Claude Code)

Modelo de repositório para começar um projeto com o Claude Code do jeito que funciona: o que foi decidido
fica escrito, o processo que se repete vira skill e nada fica pronto sem rodar.

**Para usar:** clique em **Use this template** (ou baixe o zip da
[última release](../../releases/latest)), copie as pastas para o seu projeto e preencha o `CLAUDE.md`.

## Como começar hoje

### 1. Escreva um `CLAUDE.md`

É o que o Claude lê no início de toda sessão: o que é o projeto, os comandos, onde está cada coisa e as
regras que ele não pode quebrar. Parta do [`CLAUDE.md`](CLAUDE.md) deste repo e preencha os `<...>`.
Curto e direto: regra de produto que precisa de um parágrafo mora em `docs/`; regra técnica longa sobre um
tema vira **instrução** em `.claude/rules/<tema>.md`, que o Claude carrega junto com o `CLAUDE.md` (com `paths:`,
só quando mexe nos arquivos daquele caminho). Este repo traz uma: `desempenho-com-volume.md`.

### 2. Separe o decidido do que está em discussão

| Pasta | Etapa | O que tem |
|---|---|---|
| `discovery/` | **Em discussão** | Reuniões, transcrições, atas, pendências (`em-aberto.md`). Não é regra |
| `docs/` | **Decidido** | Fichas de tela, regras, ADRs, mudanças, specs e planos. É o que se implementa |
| `src/` | **Código** | Só implementa o que está em `docs/` |

O Claude só implementa regra que está em `docs/`. Regra sem fonte vira pendência (`EA-NNN`) e pergunta a
quem decide, nunca suposição.

### 3. O processo que se repete vira skill

Instrução diz **o que vale sempre**; skill diz **como fazer** um processo, passo a passo, quando ele é chamado.

Fez a mesma coisa três vezes (registrar reunião, escrever ata, implementar tela)? Escreva os passos em
`.claude/skills/<nome>/SKILL.md`. Este repo traz sete, numeradas na ordem do processo (o número
mostra onde cada uma entra; o prefixo `sys10-` separa as nossas das que vêm de plugins):

| Skill | Quando |
|---|---|
| `/sys10-01-registrar-reuniao` | A reunião acabou: salva a transcrição e o link do protótipo |
| `/sys10-02-ata` | Transcrição salva: extrai as decisões (`D01`, `D02`…) com minuto e fonte |
| `/sys10-03-propagar-ata` | Ata pronta: pendências viram `EA`, decisões técnicas viram candidato a ADR |
| `/sys10-04-ficha-de-tela` | Tela aprovada: vira ficha em `docs/telas/` com regras, mensagens e aceites |
| `/sys10-05-implementar-tela` | Ficha pronta: portão → mapa → TDD → rodar no navegador → PR |
| `/sys10-06-escrever-adr` | Decisão técnica que outras partes vão herdar |
| `/sys10-07-desempenho-com-volume` | Dado que cresce: mede com o maior cliente ×1, ×4 e ×10 e põe os números no PR |

### 4. Verifique rodando, não só com teste

Teste verde não é pronto. O Claude sobe a aplicação e **usa a tela** no navegador (Playwright), ou o app
no emulador, compara com o protótipo por captura e só então diz que terminou. Se não deu para rodar, ele
tem que dizer isso com todas as letras. Com volume de dados, o mesmo vale: teste com dez linhas não mostra
lentidão; meça com o maior cliente real ×10 (`/sys10-07-desempenho-com-volume`).

### 5. Cada erro vira regra, com um teste de guarda

O Claude errou? Não corrija só o código: escreva a regra no `CLAUDE.md` (com o porquê e a data) e, quando
der, um teste que quebra se o erro voltar. É assim que o projeto aprende e o erro não se repete na
próxima sessão.

## Abrir no Claude Code

```bash
# instale: https://docs.claude.com/claude-code
cd meu-projeto
claude
```

- Na primeira vez, aceite os plugins de `.claude/settings.json` (superpowers, context7, playwright). Se
  não aparecer o convite, instale com `/plugin`.
- Para usar uma skill, digite `/sys10` e escolha: `/sys10-02-ata`, `/sys10-05-implementar-tela`. O Claude
  também chama a skill
  sozinho quando o pedido bate com a descrição dela ("faz a ata da reunião de hoje").
- `/init` gera um rascunho de `CLAUDE.md` lendo o código, se o projeto já existe.

## Plugins e MCPs

Tudo o que é necessário já vem em [`.claude/settings.json`](.claude/settings.json). Ao abrir o projeto, o
Claude Code oferece instalar os plugins:

| Plugin | O que traz |
|---|---|
| `superpowers` | Skills de processo: brainstorming, plano, TDD, depuração, verificação antes de dizer pronto |
| `playwright` | **MCP do Playwright**: abrir, usar e capturar a aplicação no navegador (passo 4) |
| `context7` | **MCP do Context7**: documentação atual das bibliotecas, em vez da memória do modelo |

Em `permissions.allow` ficam liberadas só as ferramentas que **leem** a página (snapshot, captura,
console, redimensionar, esperar). Navegar, clicar, digitar, executar JavaScript e consultar o Context7
pedem confirmação: uma página maliciosa pode tentar instruir o Claude a mandar dados para fora (prompt
injection). Para trabalhar sem tanta confirmação na sua máquina, libere no seu
`.claude/settings.local.json`, que não vai para o Git:

```json
{
  "permissions": {
    "allow": ["mcp__plugin_playwright_playwright", "mcp__plugin_context7_context7"]
  }
}
```

**Jira/Confluence (opcional):** copie [`.mcp.json.example`](.mcp.json.example) para `.mcp.json` na raiz
(é onde o Claude Code lê MCP de projeto). Ele pede login na Atlassian na primeira vez. Nunca coloque token
ou senha no `.mcp.json`: use variável de ambiente.

## O que tem aqui

```
CLAUDE.md                         # modelo a preencher
.claude/settings.json             # plugins (com os MCPs) e permissões
.claude/rules/                    # instruções por tema (desempenho com volume)
.claude/skills/                   # as sete skills, numeradas
.github/pull_request_template.md  # o contrato do PR
.mcp.json.example                 # Jira/Confluence, opcional
discovery/                        # README do ciclo, modelo de ata, em-aberto.md
docs/                             # README, modelo de ficha, modelo de ADR, mudancas.md, specs e planos
src/                              # seu código
```

## Licença

[MIT](LICENSE): use, copie e adapte à vontade.
