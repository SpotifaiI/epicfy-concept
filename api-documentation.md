# 1. Criar Ideia

## Request
``` http
POST /api/ideas
Content-Type: application/json

{
    "title": "Nova Feature",
    "description": "Adicionar um botão de compartilhamento nas redes sociais.",
    "status": "nova",
    "isPinned": false,
    "userId": 1  // ID do usuário que está criando a ideia
}
```
## Response
``` http
201 Created
Content-Type: application/json

{
    "id": 1,
    "title": "Nova Feature",
    "description": "Adicionar um botão de compartilhamento nas redes sociais.",
    "status": "nova",
    "isPinned": false,
    "createdAt": "2024-10-02T12:00:00Z",
    "updatedAt": "2024-10-02T12:00:00Z",
    "userId": 1
}
```
# 2. Obter Ideias
## Request
``` http
GET /api/ideas
```
## Response
``` http
200 OK
Content-Type: application/json

[
    {
        "id": 1,
        "title": "Nova Feature",
        "description": "Adicionar um botão de compartilhamento.",
        "status": "nova",
        "isPinned": false,
        "createdAt": "2024-10-02T12:00:00Z",
        "updatedAt": "2024-10-02T12:00:00Z",
        "userId": 1
    },
    {
        "id": 2,
        "title": "Melhoria na Performance",
        "description": "Otimizar o carregamento da página inicial.",
        "status": "nova",
        "isPinned": true,
        "createdAt": "2024-10-01T11:00:00Z",
        "updatedAt": "2024-10-01T11:00:00Z",
        "userId": 2
    }
]
```
# 3. Votar em uma Ideia
## Request
``` http
POST /api/votes
Content-Type: application/json

{
    "userId": 1,
    "ideaId": 1,
    "isUpvote": true
}
```
# Response
```http
201 Created
Content-Type: application/json

{
    "id": 1,
    "userId": 1,
    "ideaId": 1,
    "isUpvote": true,
    "createdAt": "2024-10-02T12:00:00Z"
}
```
	
# 4. Comentar em uma Ideia
## Request
``` http
POST /api/comments
Content-Type: application/json

{
    "userId": 1,
    "ideaId": 1,
    "content": "Acho que essa ideia é ótima!"
}
```
## Response
``` http
201 Created
Content-Type: application/json

{
    "id": 1,
    "userId": 1,
    "ideaId": 1,
    "content": "Acho que essa ideia é ótima!",
    "createdAt": "2024-10-02T12:00:00Z"
}
```
# 5. Fixar uma Ideia
``` http
PATCH /api/ideas/1/pin
Content-Type: application/json

{
    "isPinned": true
}
```
## Response
``` http
200 OK
Content-Type: application/json

{
    "id": 1,
    "title": "Nova Feature",
    "description": "Adicionar um botão de compartilhamento nas redes sociais.",
    "status": "nova",
    "isPinned": true,
    "createdAt": "2024-10-02T12:00:00Z",
    "updatedAt": "2024-10-02T12:00:00Z",
    "userId": 1
}
```
