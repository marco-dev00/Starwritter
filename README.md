const README = `# Starwritter — Distribuição Desktop (Electron)

Este repositório contém a versão desktop do Starwritter, empacotada com Electron. A aplicação carrega a SPA (home.html) localmente e utiliza um proxy interno para contornar CORS e permitir o uso da FreeAstrologyAPI sem expor a chave no frontend.

## Arquitetura

- O main.js inicia um servidor Express local.
- O servidor:
  - serve os arquivos estáticos da aplicação;
  - expõe endpoints /api/* que fazem proxy para https://json.freeastrologyapi.com/*.
- No frontend, o home.html consome a API via /api, evitando problemas de CORS e mantendo a chave fora do código cliente.

## Execução local (recomendado para testes)

### Opção one-click (Windows)

Dê duplo clique em run-starwritter.bat, na raiz do projeto.

O script:
- verifica se Node.js / NPM estão instalados (abre o instalador se não estiverem);
- executa npm install automaticamente, se necessário;
- inicia o app com npm start em uma janela do PowerShell.

### Execução manual

1. Instale as dependências:

cd starwritter
npm install

2. Inicie o app em modo desenvolvimento:

npm start

Ao iniciar, o Electron abre uma janela apontando para http://localhost:<porta>/home.html.
A porta é escolhida automaticamente pelo servidor local.

## Chave da API (FreeAstrologyAPI)

A chave não fica embutida no frontend por questões de segurança. Existem duas formas de fornecê-la:

- Via interface: no modal “Preencher Mapa”, use o campo “Chave API alternativa”.
- Via variável de ambiente (recomendado para empacotamento):

Windows (PowerShell):
$env:FREEASTRO_API_KEY = 'SUA_CHAVE'
npm start

macOS / Linux:
export FREEASTRO_API_KEY='SUA_CHAVE'
npm start

Se definida no ambiente, a chave é utilizada diretamente pelo processo do Electron.

## Empacotamento

Para gerar instaladores ou binários distribuíveis, o projeto já está preparado para uso com electron-builder.

- Build disponível via npm run dist.
- Workflow em .github/workflows/build.yml executa o build em CI e anexa os artefatos como artifacts.

O build roda automaticamente ao fazer push para a branch main.

## Observações

- O proxy local encaminha o header x-api-key para a FreeAstrologyAPI.
- Se a chave for informada via interface, ela é repassada nas requisições.
- É possível publicar o app como site estático (ex.: GitHub Pages), mas nesse caso:
  - chamadas ficam sujeitas a CORS;
  - a chave da API ficará exposta no JavaScript.

## Status

- Estrutura Electron funcional
- Proxy local implementado
- Suporte a variável de ambiente para chave da API
- Build automatizado via GitHub Actions
- electron-builder configurado
`;
