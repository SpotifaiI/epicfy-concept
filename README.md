# Epicfy

Aplicação para sugestões de melhorias para soluções ao redor do mundo.

# Membros

- [x] Cristian Prochnow
- [x] Gustavo Henrique Dias
- [x] Lucas Willian de Souza Serpa 
- [x] Marlon de Souza 
- [x] Ryan Gabriel Mazzei Bromati

# Documentação

## Requisitos Funcionais

## Requisitos Não-Funcionais

## Diagrama da Arquitetura

``` mermaid
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
    FE -->|Submit Features, Improvements, Bug Fixes, Vote, Comment| API
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

## Diagrama do Banco de dados

``` mermaid

%%{init: {'theme': 'dark'}}%%
erDiagram
    Idea {
        int id PK "Identificador único da ideia"
        string title "Título da ideia"
        string description "Descrição da ideia"
        string status "Status da ideia (e.g., nova, em desenvolvimento, concluída)"
        boolean isPinned "Indica se a ideia está fixada no topo"
        timestamp createdAt "Data e hora de criação da ideia"
        timestamp updatedAt "Data e hora da última atualização da ideia"
    }

    User {
        int id PK "Identificador único do usuário"
        string username "Nome de usuário"
        string email "E-mail do usuário"
        boolean isCompany "Indica se o usuário é uma empresa"
        timestamp createdAt "Data e hora de criação do usuário"
    }

    Vote {
        int id PK "Identificador único do voto"
        int userId FK "Identificador do usuário que votou"
        int ideaId FK "Identificador da ideia votada"
        boolean isUpvote "Indica se é um upvote (true) ou downvote (false)"
        timestamp createdAt "Data e hora do voto"
    }

    Comment {
        int id PK "Identificador único do comentário"
        int userId FK "Identificador do usuário que comentou"
        int ideaId FK "Identificador da ideia comentada"
        string content "Conteúdo do comentário"
        timestamp createdAt "Data e hora do comentário"
    }

    %% Relationships
    Idea ||--o{ Vote : "Recebe"
    Idea ||--o{ Comment : "Possui"
    User ||--o{ Vote : "Vota"
    User ||--o{ Comment : "Comenta"



```


