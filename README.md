# Starter kit: trabalhar com IA (Claude Code)

Modelo de repositório para começar um projeto com o Claude Code do jeito que funciona: o que foi decidido
fica escrito, o processo que se repete vira skill e nada fica pronto sem rodar.

> Revisado em 27/11/2026. As ferramentas mudam a cada um ou dois meses: confira a data e a última
> [release](../../releases/latest).

**Para usar:** clique em **Use this template** (ou baixe o zip da
[última release](../../releases/latest)), copie as pastas para o seu projeto e preencha o `CLAUDE.md`.

## Como começar hoje

### 1. Escreva um `CLAUDE.md`

É o que o Claude lê no início de toda sessão: o que é o projeto, os comandos, onde está cada coisa e as
regras que ele não pode quebrar. Parta do [`CLAUDE.md`](CLAUDE.md) deste repo e preencha os `<...>`.
Curto e direto: regra de produto que precisa de um parágrafo mora em `docs/`; regra técnica longa sobre um
tema vira **instrução** em `.claude/rules/<tema>.md`, que o Claude carrega junto com o `CLAUDE.md` (com `paths:`,
só quando mexe nos arquivos daquele caminho). Este repo traz nove: verificação, git e PR, segurança,
autonomia, trabalho em paralelo, código, telas, banco e migrations, e desempenho com volume. Ajuste os
`paths:` e os `<...>` ao seu projeto.

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
`.claude/skills/<nome>/SKILL.md`. Este repo traz oito, numeradas na ordem do processo (o número
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
| `/sys10-08-nova-regra` | Erro corrigido ou "nunca mais": vira regra no lugar certo, com guarda |

### 4. Verifique rodando, não só com teste

Teste verde não é pronto. O Claude sobe a aplicação e **usa a tela** no navegador (Playwright), ou o app
no emulador, compara com o protótipo por captura e só então diz que terminou. Se não deu para rodar, ele
tem que dizer isso com todas as letras. Com volume de dados, o mesmo vale: teste com dez linhas não mostra
lentidão; meça com o maior cliente real ×10 (`/sys10-07-desempenho-com-volume`).

### 5. Cada erro vira regra, com um teste de guarda

O Claude errou? Não corrija só o código: rode `/sys10-08-nova-regra`. A regra vai para o lugar certo (`CLAUDE.md`
ou `.claude/rules/`), com o porquê, a data e quem pediu, e ganha uma guarda quando der: um teste, um lint ou um
hook que quebra se o erro voltar. Lição que ficou só na memória de alguém sobe para o projeto por PR. É assim que o
projeto aprende e o erro não se repete na próxima sessão de ninguém (detalhes: "Como as regras evoluem" no
`CLAUDE.md`).

## Não é dev? Comece pelo Claude desktop

O kit é para projetos de código, mas a ideia vale para qualquer trabalho. Sem Git nem terminal:

1. **Crie um projeto** no Claude e escreva nas instruções dele o que escreveria no `CLAUDE.md`: o que é o
   trabalho, onde estão as coisas, as regras e o que nunca pode acontecer.
2. **Conecte as ferramentas** que você usa (Jira, Google Drive, Gmail, Agenda…) nas configurações de
   conectores. Algumas, como o WhatsApp, exigem instalar algo na sua máquina: peça ajuda a quem já fez.
3. **O que você repete vira skill:** escreva os passos uma vez, salve como skill e chame com `/`.
4. **Dado de cliente:** siga a receita de [`seguranca.md`](.claude/rules/seguranca.md) (amostra fictícia, a IA
   gera um programa, o dado real passa só pelo programa).

## Primeiros prompts

- "Vou fazer <tarefa>, que me toma <X horas> por <semana>. Como você pode me ajudar? Pergunte o que precisar."
- "Leia <pasta/arquivo> e me diga o que falta para um `CLAUDE.md` deste projeto."
- "Faço isto toda semana: <passos>. Transforme em uma skill."

**Contexto é por conversa:** cada conversa tem a própria memória, que enche. Assunto novo, conversa nova; o que
precisa valer sempre vai para o `CLAUDE.md`, para as instruções do projeto ou para uma skill. Tarefa grande, peça
para dividir em subagentes: cada um começa do zero e faz só a sua parte.

## Abrir no Claude Code

```bash
# instale: https://code.claude.com/docs
cd meu-projeto
claude
```

- **Use o modo auto:** `Shift+Tab` até aparecer "auto mode", ou `claude --permission-mode auto`. Ele segue
  sozinho no que é seguro e pergunta no que é arriscado. Para abrir sempre nele, ponha
  `"permissions": { "defaultMode": "auto" }` no seu `~/.claude/settings.json` (no `.claude/settings.json` do
  projeto essa chave não vale para o modo auto).
- Na primeira vez, aceite os plugins de `.claude/settings.json` (superpowers, context7, playwright). Se
  não aparecer o convite, instale com `/plugin`.
- Para usar uma skill, digite `/sys10` e escolha: `/sys10-02-ata`, `/sys10-05-implementar-tela`. O Claude
  também chama a skill sozinho quando o pedido bate com a descrição dela ("faz a ata da reunião de hoje").
- `/init` gera um rascunho de `CLAUDE.md` lendo o código, se o projeto já existe.

## Plugins e MCPs

Tudo o que é necessário já vem em [`.claude/settings.json`](.claude/settings.json). Ao abrir o projeto, o
Claude Code oferece instalar os plugins:

| Plugin | O que traz |
|---|---|
| `superpowers` | Skills de processo: brainstorming, plano, TDD, depuração, verificação antes de dizer pronto |
| `playwright` | **MCP do Playwright**: abrir, usar e capturar a aplicação no navegador (passo 4) |
| `context7` | **MCP do Context7**: documentação atual das bibliotecas, em vez da memória do modelo |
| `claude-md-management` | `/revise-claude-md` (leva o que a sessão ensinou para o `CLAUDE.md`) e a auditoria do `CLAUDE.md` |

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
.claude/rules/                    # instruções por tema (verificação, git, segurança, código, telas, banco, desempenho)
.claude/skills/                   # as oito skills, numeradas, e _comum/regras.md (vale para todas)
.github/pull_request_template.md  # o contrato do PR
.mcp.json.example                 # Jira/Confluence, opcional
.editorconfig                     # formatação comum a qualquer editor
discovery/                        # README do ciclo, modelo de ata, em-aberto.md
docs/projeto/                     # visão geral, mudanças, riscos
docs/produto/                     # glossário, regras transversais, parâmetros, estados, RNF
docs/telas/, docs/arquitetura/    # modelo de ficha de tela e de ADR
docs/superpowers/                 # specs e planos
src/                              # seu código
```

## Dúvidas e ajuda

Trave em alguma coisa (conectar uma ferramenta, montar uma skill, saber se um dado pode ir para a IA)? Fale com
<canal ou pessoa de referência do time>. Monte o primeiro caso de uso junto com alguém que já usa: é o jeito mais
rápido de aprender.

## Licença

[MIT](LICENSE): use, copie e adapte à vontade.
