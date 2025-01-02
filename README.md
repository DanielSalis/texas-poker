# Texas Poker Project

Este projeto é composto por três repositórios que juntos criam uma aplicação de poker online com suporte a canais via WebSocket.Instruções abaixo para clonar, configurar e executar o ambiente.

---

## Clonando os Repositórios

1.  **Clone o repositório `texas_poker`:**

        bash

        `git clone https://github.com/DanielSalis/poker_api.git

    cd texas_poker`

2.  **Clone o repositório `poker_api`:**

        bash

        `git clone https://github.com/DanielSalis/poker_api.git

    cd poker_api`

3.  **Clone o repositório `poker_client`:**

        bash

        `git clone https://github.com/DanielSalis/poker_client.git

    cd poker_client`

---

## Executando o Projeto

1.  **Execute o Docker Compose**\
    Certifique-se de estar no diretório raiz do projeto `texas_poker` e rode o comando:

    `docker compose up`

2.  **Acesse a aplicação:**

    - A API estará disponível em: `http://localhost:3000`
    - O cliente estará disponível em: `http://localhost:3001`

---

## Executando os Testes

1.  **Acesse o contêiner da API:**

    bash

    `docker compose run api bash`

2.  **Execute os testes do Rails:**

    bash

    `rails test`

---

## Sobre o Projeto

### Uso de Action Cable (Rails Channels)

O projeto utiliza o **Action Cable** do Rails para implementar comunicação em tempo real. Os canais permitem que eventos sejam enviados para os clientes conectados sempre que ações específicas acontecem no backend, como:

- **Criação de Salas:** Sempre que uma sala é criada, os clientes são notificados.
- **Ações dos Jogadores:** Quando um jogador realiza uma ação (como `check`, `raise`, ou `fold`), mensagens são enviadas para o canal.
- **Mudança de Fase:** Sempre que a fase do jogo muda, os clientes recebem atualizações via actioncable consumer.

### Funcionalidades Principais

1.  **Criação de Salas:**\
    Os usuários podem criar salas para o jogo.

2.  **Entrar e Sair de Salas:**\
    Os jogadores podem se conectar a uma sala existente e sair quando quiserem. As informações do jogador são armazenadas no `sessionStorage` para controle.

3.  **Exibição de Cartas:**\
    Cada jogador pode ver apenas suas próprias cartas. As cartas comunitárias são exibidas para todos os jogadores na sala.

4.  **Atualizações em Tempo Real:**\
    Sempre que a fase muda ou um jogador realiza uma ação, as atualizações são enviadas para todos os jogadores conectados via WebSocket.

---

## Exemplos de Ações Disponíveis

- **Criar uma sala:**\
  Enviar uma solicitação POST para o endpoint `/rooms`.

- **Entrar em uma sala:**\
  Enviar uma solicitação POST para o endpoint `/rooms/:id/join`.

- **Sair de uma sala:**\
  Enviar uma solicitação DELETE para o endpoint `/rooms/:id/leave`.

- **Realizar ações no jogo:**\
  Enviar uma solicitação POST para o endpoint `/action` com a ação desejada (`check`, `raise`, `fold`, etc.).
  !!!ATENÇÃO NESSE ENDPOINT: Nos requisitos existia uma property no body chamada action, no entanto "action" é uma palavra reservada dos params do rails. Alterei para "action_type"

- **Avançar para a próxima fase:**\
  Enviar uma solicitação POST para o endpoint `/next-phase`.

- **Todas as chamas estão na collections do postman nesse repo:**\
  [Arquivo](/texas-poker.postman_collection.json)

---
