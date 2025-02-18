# Supermarket Price Tracker

Este projeto consiste em uma API Rails com PostgreSQL para capturar valores de etiquetas em gôndolas de supermercado e exibir a soma em tempo real em um aplicativo móvel desenvolvido em React Native. O objetivo é facilitar a soma dos valores gastos em tempo real e salvar o histórico de compras.

## Requisitos Funcionais

- **Captura de Valores:**
  - O usuário poderá escanear ou digitar o valor de etiquetas de produtos.
  - Cada valor capturado será adicionado a uma lista de itens.

- **Soma em Tempo Real:**
  - O sistema deve calcular e exibir a soma total dos valores capturados em tempo real.

- **Finalização da Compra:**
  - Ao finalizar a compra, o sistema deve salvar o valor total, a data da compra e o estabelecimento.

- **Histórico de Compras:**
  - O usuário poderá visualizar um histórico de compras anteriores, com detalhes como valor total, data e estabelecimento.

## Requisitos Não Funcionais

- **Performance:**
  - A soma dos valores deve ser feita em tempo real, sem atrasos perceptíveis.

- **Segurança:**
  - A API deve ser segura, com autenticação básica para evitar acesso não autorizado.

- **Escalabilidade:**
  - A arquitetura deve permitir futuras expansões, como adição de novos recursos ou integrações.

## Estrutura do Projeto

### API Rails

- **Models:**
  - `Purchase`: Armazena o valor total, a data da compra e o estabelecimento.
    - Campos: `total_amount` (decimal), `purchase_date` (datetime), `establishment` (string).
  - `Item`: Armazena os valores capturados de cada etiqueta.
    - Campos: `value` (decimal), `purchase_id` (foreign key).

- **Controllers:**
  - `PurchasesController`: Responsável por criar e listar compras.
    - Actions: `index`, `create`.
  - `ItemsController`: Responsável por adicionar itens a uma compra.
    - Actions: `create`.

- **Rotas:**
  - `POST /purchases`: Cria uma nova compra.
  - `GET /purchases`: Lista todas as compras.
  - `POST /items`: Adiciona um item a uma compra existente.

- **Autenticação:**
  - Usar `has_secure_password` para autenticação básica ou uma gem como `Devise` para autenticação mais robusta.

### React Native (Mobile)

- **Telas:**
  - **Tela de Captura:**
    - Campo para digitar ou botão para escanear o valor da etiqueta.
    - Exibição da lista de itens capturados e soma total em tempo real.
  - **Tela de Finalização:**
    - Botão para finalizar a compra, salvando os dados no backend.
  - **Tela de Histórico:**
    - Lista de compras anteriores, com detalhes como valor total, data e estabelecimento.

- **Integração com API:**
  - Usar `axios` ou `fetch` para fazer chamadas à API Rails.
  - Exemplo:
    - `POST /items`: Envia o valor capturado para a API.
    - `POST /purchases`: Finaliza a compra e salva os dados.
    - `GET /purchases`: Recupera o histórico de compras.

## Fluxo de Trabalho

- **Captura de Valores:**
  1. O usuário escaneia ou digita o valor da etiqueta.
  2. O valor é enviado para a API via `POST /items`.
  3. A API adiciona o item à compra atual e retorna a soma total atualizada.

- **Finalização da Compra:**
  1. O usuário finaliza a compra.
  2. A API salva a compra via `POST /purchases` e retorna uma confirmação.

- **Histórico de Compras:**
  1. O usuário acessa a tela de histórico.
  2. A API retorna a lista de compras via `GET /purchases`.

## Tecnologias

- **Backend:**
  - Ruby on Rails (API mode)
  - PostgreSQL (banco de dados)
  - Gems úteis: `devise` (autenticação), `active_model_serializers` (serialização de JSON)

- **Frontend (Mobile):**
  - React Native
  - Bibliotecas úteis: `axios` (chamadas HTTP), `react-navigation` (navegação)

## Próximos Passos

- **Configuração do Ambiente:**
  - Instalar Ruby, Rails e PostgreSQL.
  - Criar o projeto Rails em modo API: `rails new my_project --api -d postgresql`.

- **Desenvolvimento do MVP:**
  - Criar os models, controllers e rotas.
  - Implementar a lógica de captura e soma em tempo real.
  - Desenvolver as telas no React Native e integrar com a API.

## Considerações Futuras

- **Integração com Câmera:**
  - Implementar a captura de valores via câmera (OCR para ler etiquetas).

- **Sincronização Offline:**
  - Permitir que o usuário continue capturando valores mesmo sem conexão, sincronizando com a API posteriormente.

- **Relatórios e Análises:**
  - Adicionar funcionalidades para gerar relatórios de gastos por período ou estabelecimento.
