# Starwritter — Distribuição Desktop (Electron)

Este repositório contém a versão desktop do Starwritter, empacotada com Electron. A aplicação carrega a SPA (`home.html`) localmente e utiliza um proxy interno para contornar CORS e permitir o uso da FreeAstrologyAPI sem expor a chave no frontend.

## Arquitetura

- O `main.js` inicia um servidor Express local.
- O servidor:
  - serve os arquivos estáticos da aplicação;
  - expõe endpoints `/api/*` que fazem proxy para `https://json.freeastrologyapi.com/*`.
- No frontend, o `home.html` consome a API via `/api`, evitando problemas de CORS e mantendo a chave fora do código cliente.

## Execução local (recomendado para testes)

### Opção one-click (Windows)

Dê duplo clique em `run-starwritter.bat`, na raiz do projeto.

O script:
- verifica se Node.js / NPM estão instalados (abre o instalador se não estiverem);
- executa `npm install` automaticamente, se necessário;
- inicia o app com `npm start` em uma janela do PowerShell.

### Execução manual

1. Instale as dependências:

```bash
cd starwritter
npm install
