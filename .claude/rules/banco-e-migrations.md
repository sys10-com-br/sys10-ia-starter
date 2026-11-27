---
paths:
  - "src/**"
  - "**/migrations/**"
---

# Banco e migrations

Ajuste o `paths:` acima para as pastas do backend e das migrations do seu projeto.

- **Migration aplicada não se edita.** Mudou de ideia? Migration nova.
- **Versão da migration é o timestamp real** (`date -u +%Y%m%d%H%M`), nunca um número redondo ou "o próximo":
  duas branches em paralelo escolhem o mesmo número e o deploy quebra.
- **ID fixo no código (seed, permissão, dado de teste) é gerado na hora** (`uuidgen`), nunca sequencial
  (`...0001`, `...0002`): pelo mesmo motivo.
- **Tipo e status com valores fixos** são enum do banco ou `CHECK`, nunca texto livre.
- **Transação só em escrita, e curta.** Leitura não abre transação.
- **Filtro, ordenação e paginação rodam no banco**, nunca carregando tudo para filtrar no código.
- **I/O assíncrono** quando a linguagem oferece (banco, HTTP, arquivo), com cancelamento.
- **Índice para todo filtro, junção e ordenação** em tabela que cresce; chave estrangeira indexada
  (ver `desempenho-com-volume.md`).
- **Seed e dado de teste:** prefira uma amostra real anonimizada; dado inventado esconde os casos que quebram.
- **Nunca rode uma migration nova no banco compartilhado ou de produção para testar**: use uma cópia local.
