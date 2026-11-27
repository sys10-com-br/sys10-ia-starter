---
paths:
  - "src/**"
---

# Código

Ajuste o `paths:` acima para a pasta do código do seu projeto.

- **Siga o formatador e o linter do projeto** (`<comando de format/lint>`) antes de commitar. O que eles não
  cobrem está abaixo.
- **Linhas até `<120>` colunas**, inclusive comentários.
- **Chamada ou assinatura longa, um argumento por linha.** A partir de `<4>` argumentos, ou quando não cabe na
  linha. Nada de agrupar vários por linha "até encher".
- **Argumentos nomeados** quando a chamada tem dois ou mais booleanos, números soltos ou nulos em sequência, para
  não dar para trocar a ordem sem perceber (ex.: `send(order, notify: true, retry: false)`).
- **Nunca abrevie nomes** (`quantity`, não `qty`; `configuration`, não `cfg`). Exceção: siglas que viraram palavra
  (`id`, `url`, `api`, `http`, `json`) e nomes impostos por biblioteca.
- **O nome diz o que é.** Nada de ID de requisito ou de card no nome (`rule12`, `ticket345`); o ID vai no
  comentário.
- **Funções pequenas** (até ~50 linhas), arquivos focados (até ~400), no máximo 4 níveis de aninhamento.
- **Sem mutação escondida:** crie um objeto novo em vez de alterar o recebido.
- **Erro tratado em todo nível:** mensagem clara para o usuário, log com contexto no servidor, nunca engolido em
  silêncio.
- **Valide na borda:** toda entrada externa (usuário, API, arquivo) é validada antes de usar, de preferência por
  schema.
- **Biblioteca consolidada antes de helper caseiro** para o que é genérico (data, moeda, máscara, validação).
- **Nada fixo no código** que deveria ser configuração (URL, limite, chave): constante ou configuração.
