# Epicfy

O **Epicfy** é uma plataforma inovadora que melhora a interação entre usuários e a empresa, possibilitando a coleta eficiente de ideias e feedbacks. Com um design modular e tecnologias modernas, o projeto está preparado para escalar e atender a uma base crescente de usuários.

## Membros

- [x] Cristian Prochnow
- [x] Gustavo Henrique Dias
- [x] Lucas Willian de Souza Serpa 
- [x] Marlon de Souza 
- [x] Ryan Gabriel Mazzei Bromati

## Requisitos Funcionais

1. **Cadastro de Usuários:**
   - Usuários podem se cadastrar na plataforma como clientes ou funcionários da empresa.

2. **Postagem de Ideias:**
   - Usuários podem criar e submeter ideias de melhorias, funcionalidades ou correções.

3. **Votação em Ideias:**
   - Usuários podem votar nas ideias, utilizando upvotes e downvotes.

4. **Comentários em Ideias:**
   - Usuários podem comentar nas ideias para discutir sugestões e melhorias.

5. **Fixação de Ideias:**
   - A empresa pode fixar ideias no topo da lista, garantindo destaque às sugestões mais relevantes.

6. **Notificações por E-mail:**
   - A empresa recebe notificações por e-mail sempre que uma nova ideia é cadastrada.

7. **Visualização de Ideias:**
   - Usuários podem visualizar todas as ideias cadastradas, incluindo suas descrições, status e interações.

## Requisitos Não-Funcionais

1. **Desempenho:**
   - A aplicação deve suportar pelo menos 1000 usuários simultâneos sem degradação de performance.

2. **Escalabilidade:**
   - O sistema deve ser escalável para permitir o crescimento do número de usuários e ideias.

3. **Segurança:**
   - Todos os dados sensíveis, como senhas e informações pessoais, devem ser criptografados.

4. **Usabilidade:**
   - A interface do usuário deve ser intuitiva e responsiva, permitindo uma experiência de navegação fluida.

5. **Manutenibilidade:**
   - O código deve ser modular e bem documentado, facilitando a manutenção e futuras atualizações.

## Diagrama de Arquitetura

``` mermaid
%%{init: {'theme': 'dark'}}%%
flowchart TD
    subgraph ClientSide [Client Side - React Application]
        FE[React Client - User Interface]
    end

    subgraph ServerSide [Server Side - Node.js API]
        API[API Gateway - Node.js] 
        subgraph Controllers [Controllers]
            IdeasCtrl[Ideas Controller - Features, Improvements, Bug Fixes] 
            VotesCtrl[Vote Controller] 
            CommentsCtrl[Comments Controller]
            PinCtrl[Pin Controller - Pin Idea]
        end
        DB[(PostgreSQL Database)]
    end

    subgraph NotificationSystem [Notification System - C#]
        NotifyService[Notification Service - C#]
        Email[Email System - SMTP Server]
    end

    %% Connections
    FE -->|Submit Improvements, Bug Fixes, Vote, Comment| API
    FE -->|Pin Idea| PinCtrl
    API -->|Route to Controller| IdeasCtrl
    API -->|Route to Controller| VotesCtrl
    API -->|Route to Controller| CommentsCtrl
    API -->|Route to Controller| PinCtrl

    %% Database interactions
    IdeasCtrl -->|Store/Retrieve Ideas| DB
    VotesCtrl -->|Store/Retrieve Votes| DB
    CommentsCtrl -->|Store/Retrieve Comments| DB
    PinCtrl -->|Pin/Unpin Idea| DB

    %% Notification flow
    IdeasCtrl -->|New Idea Trigger| NotifyService
    NotifyService -->|Send Email Notification| Email
    Email -->|Notify Company| CompanyEmail[Company Email System]
```

## Diagrama do Banco de Dados

``` mermaid
%%{init: {'theme': 'dark'}}%%
erDiagram
    Usuário {
        int id PK "Identificador único"
        string nome "Nome do usuário"
        string email "E-mail do usuário"
        boolean isEmpresa "Indica se é funcionário da empresa"
    }

    Ideia {
        int id PK "Identificador único"
        string titulo "Título da ideia"
        string descricao "Descrição detalhada da ideia"
        string status "Status da ideia (nova, em desenvolvimento, concluída)"
        boolean isPinned "Indica se a ideia está fixada"
        int userId FK "Identificador do usuário que postou a ideia"
    }

    Voto {
        int id PK "Identificador único"
        int userId FK "Identificador do usuário que votou"
        int ideaId FK "Identificador da ideia votada"
        boolean isUpvote "Indica se é um upvote (true) ou downvote (false)"
    }

    Comentário {
        int id PK "Identificador único"
        int userId FK "Identificador do usuário que comentou"
        int ideaId FK "Identificador da ideia comentada"
        string conteudo "Conteúdo do comentário"
    }

    %% Relações
    Usuário ||--o{ Ideia : posta
    Usuário ||--o{ Voto : realiza
    Usuário ||--o{ Comentário : escreve
    Ideia ||--o{ Voto : recebe
    Ideia ||--o{ Comentário : tem
```