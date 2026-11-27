# Verificação: pronto é rodando

Vale para toda mudança.

- **Teste primeiro.** Cada critério de aceite vira um teste com os mesmos valores; primeiro falha, depois passa.
- **Teste verde não é pronto.** Depois de build, testes e lint verdes (`<comandos>`), rode a aplicação e use o
  que mudou:
  - **web:** no navegador, pelo Playwright, fluxo a fluxo, nas larguras `<1440, 820 e 390 px>`;
  - **mobile:** no emulador ou no aparelho;
  - **API:** chamada de verdade ao endpoint, com os casos de erro;
  - **CLI/script:** executado com uma entrada real.
- **Tem protótipo?** Compare a tela com ele por captura, lado a lado, no mesmo estado. Diferença é bug, ou vai no
  PR como "Diferença do design", com o porquê.
- **Branch com migration:** teste contra uma cópia local do banco, nunca contra o banco compartilhado ou de
  produção.
- **Não deu para rodar** (sem banco, sem login, sem emulador)? Diga isso com todas as letras e o que ficou sem
  teste. Nunca diga "pronto" só com os testes automatizados.
- **Build de produção num comando sozinho, e conferido antes de publicar.** Nunca gere o artefato de produção (APK,
  pacote, imagem) no mesmo comando de um build de teste com configuração própria (URL de API, chave): a configuração
  vaza para o de produção. Antes de publicar, confira dentro do artefato a URL, a versão e a assinatura.
- **Evidência no PR:** o que foi usado, com que dados, e as capturas.
