---
paths:
  - "src/web/**"
---

# Telas

Ajuste o `paths:` acima para a pasta do front (web, mobile) do seu projeto.

- **O protótipo aprovado é o gabarito.** Antes de codar, abra a tela do protótipo no mesmo estado (cada popup,
  aba e passo) e copie a estrutura: ordem dos blocos, textos literais, botões, ícones, colunas. Nunca implemente
  "pelo espírito" do design nem por um resumo em texto.
- **Design system é obrigatório:** cor, fonte, botão, ícone, status e formato de valor saem dele (token e
  componente), nunca de uma decisão na tela.
- **O mesmo elemento usa o mesmo componente** em todas as telas. Mudou um, padronize os outros.
- **Todo estado existe:** carregando, vazio, erro, sem permissão, com o texto de cada um.
- **Só o aprovado vira código.** O que o protótipo marca como pendente ou "a validar" fica fora, e a tela nunca
  mostra dado inventado.
- **Toda tela tem endereço (rota)**, e filtro que vale compartilhar fica na URL.
- **Leitura com cache** pela biblioteca do projeto (`<ex.: React Query, SWR>`), nunca buscando a cada render.
- **Uma chamada por tela, lista pronta:** nada de uma requisição por linha.
- **Responsivo:** a página nunca rola para o lado; tabela larga rola dentro do próprio quadro.
