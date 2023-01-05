
<h1 align="center">Habitum - API</h1>

<p align="center">Este é o backend da aplicação Habitum - Um hub para quem quer criar e manter seu habito!</p>


<p align="center">
  <a href="#endpoints">Endpoints</a>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</p>


## **Endpoints**


A API tem um total de 4 endpoints

O url base da API é https://habitum-fakeapi-v1.onrender.com

<h2 align ='center'> Cadastrando Usúarios </h2>

`POST /register -  FORMATO DA REQUISIÇÃO`
```json
{
 "img": "",
 "name": "Jorge Rodrigo",
 "userName": "Jorge",
 "email": "jorge2@mail.com",
 "password": "******"
}
```

Se tudo der certo essa sera a resposta:

`FORMATO DA RESPOSTA - STATUS 201`
```json
{
   "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImpvcmdlMkBtYWlsLmNvbSIsImlhdCI6MTY3Mjc3NTg4MiwiZXhwIjoxNjcyNzc5NDgyLCJzdWIiOiIzIn0.eNXzswCHD94jtXsBALvBfldkaLGmWtLo4II9bSU04_M",
   "user": {
	"email": "jorge2@mail.com",
	"img": "",
	"name": "Jorge Rodrigo",
	"userName": "Jorge",
	"id": 3
    }
}
```

<h2 align ='center'> Possíveis erros </h2>

Caso você acabe errando e mandando algum campo errado, a resposta de erro será assim:

No exemplo a requisição foi feita usando o email que ja esta cadastrado no banco de dados.

`` FORMATO DA RESPOSTA - STATUS 400``
```json
"Email already exists"
```

Nesse outro exemplo a requisição foi feita com um senha com menos que 6 caracteres.


`` FORMATO DA RESPOSTA - STATUS 400``
```json
"Password is too short"
```

Se caso a requisição foi feita sem o email ou senha essa sera a resposta.


`` FORMATO DA RESPOSTA - STATUS 400``
```json
"Email and password are required"
```

<h2 align ='center'> Fazendo Login </h2>

`POST /login - FORMATO DA REQUISIÇÃO`
```json
{
   "email": "jorge2@mail.com",
   "password": "******"
}
```

Caso dê tudo certo, a resposta será assim:

`POST /login -  FORMATO DA RESPOSTA - STATUS 200`
```json

{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImpvcmdlMkBtYWlsLmNvbSIsImlhdCI6MTY3Mjc3NzIwNywiZXhwIjoxNjcyNzgwODA3LCJzdWIiOiIzIn0.dYTSjaUDEO58Sgf6rD2fOVy1yDmLL_uFBg4rDbTqIBU",
    "user": {
	"email": "jorge2@mail.com",
	"img": "",
	"name": "Jorge Rodrigo",
	"userName": "Jorge",
	"id": 3
   }
}
```

<h2 align ='center'> Possíveis erros </h2>

Caso você acabe errando e mandando algum campo errado, a resposta de erro será assim:

No exemplo a requisição foi feita usando o email que não esta no banco de dados

`` FORMATO DA RESPOSTA - STATUS 400``
```json
"Cannot find user"
```

Nesse outro exemplo a requisição foi feita com um senha que esta incorreta.


`` FORMATO DA RESPOSTA - STATUS 400``
```json
"Incorrect password"
```

## Rotas que necessitam de autorização

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

> Authorization: Bearer {token}


<h2 align ='center'> Visualizar usuários</h2>

Para mostrar todos os usuários: 

`GET /users -  FORMATO DA REQUISIÇÃO`

`FORMATO DA RESPOSTA - STATUS 200`

```json
[
   {
	"email": "mariano@mail.com",
	"password": "$2a$10$W5xwM74rWL67bAU/68EHhuRbr876OGwWdbKOveYgyzZOWBhhdCkR2",
	"img": "",
	"name": "Mariano Andrade",
	"userName": "Mariano",
	"id": 1,
	"habits": []
  },
  {
	"email": "jorge@mail.com",
	"password": "$2a$10$BrqxsGhj/JoTFgEsY.Uq7OjCdrHOeXyjpXeRtOyUicPaQIWhlYC46",
	"img": "",
	"name": "Jorge Rodrigo",
	"userName": "jorge",
	"id": 2,
	"habits": []
   }
]
```


Para mostrar apenas o usuário logado: 


`GET /users/{id do usuário} -  FORMATO DA REQUISIÇÃO`

`FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "email": "jorge2@mail.com",
  "password": "$2a$10$VDeQ5PrB0qKwDZnePtXb5OvROP3P1hOe13ti0hJMk8ex6..4Rwneu",
  "img": "",
  "name": "Jorge Rodrigo",
  "userName": "Jorge",
  "id": 3
}
```

<b>Para Editar um Usuário:</b>

Só é necessario mandar a alteração que quiser fazer, não precisa mandar todo o corpo de requisição novamente.

`PATCH /habits/{id do usuário} - FORMATO DA REQUISIÇÃO`
```json
{
  "bits": 10
}
```

`FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "email": "jorge@mail.com",
  "password": "$2a$10$qukuz7y3/9I.pUDVPS/UH.Bc9/BvE4q4dgzF/9iJgQfDmO99tAhW.",
  "img": "",
  "name": "Jorge Rodrigo",
  "userName": "Jorge",
  "id": 3,
  "bits": 10
}
```

<p>Visualizar usuário com os habitos</p>

`POST /users/{id do usuário}?_embed=habits -  FORMATO DA REQUISIÇÃO`

`FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "email": "jorge2@mail.com",
  "password": "$2a$10$VDeQ5PrB0qKwDZnePtXb5OvROP3P1hOe13ti0hJMk8ex6..4Rwneu",
  "img": "",
  "name": "Jorge Rodrigo",
  "userName": "Jorge",
  "id": 3,
  "habits": []
}
```

<h2 align ='center'> Criar Habitos para o seu perfil </h2>

Sempre que for criar ou editar um habito sempre é preciso colocar o userId

`POST /habits - FORMATO DA REQUISIÇÃO`
```json
{
    "title": "Arrumar a casa",
    "description": "Arrumando a casa",
    "personal_reward": "Bolo de chocolate",
    "dificulty": "medio",
    "userId": 3
}
```

O nivel de dificuldade sera dividido em 3 sendo eles: 

  - Fácil
  - Médio 
  - Difícil
  
  
`FORMATO DA RESPOSTA - STATUS 201`

```json
{
    "title": "Arrumar a casa",
    "description": "Arrumando a casa",
    "personal_reward": "Bolo de chocolate",
    "dificulty": "medio",
    "userId": 3,
    "id": 2
}
```
 
 Para editar um Habito: 

`PATCH /habits/{id do habito} - FORMATO DA REQUISIÇÃO`
```json
{
    "title": "Arrumar",
    "description": "Arrumando a casa",
    "personal_reward": "Bolo de chocolate",
    "dificulty": "medio",
    "userId": 3
}
```

`FORMATO DA RESPOSTA - STATUS 200`

```json
{
    "title": "Arrumar",
    "description": "Arrumando a casa",
    "personal_reward": "Bolo de chocolate",
    "dificulty": "medio",
    "userId": 3,
    "id": 2
}
```

Para ver todos o habitos: 

`GET /habits -  FORMATO DA REQUISIÇÃO`

`FORMATO DA RESPOSTA - STATUS 200`

```json
[
  {
	"userId": 3,
	"id": 1
  },
  {
	"title": "Arrumar",
	"description": "Arrumando a casa",
	"personal_reward": "Bolo de chocolate",
	"dificulty": "medio",
	"userId": 3,
	"id": 2
   }
]
```

Ver Apenas um habito em especifico: 

`GET /habits/{id do habito} -  FORMATO DA REQUISIÇÃO`

`FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "title": "Arrumar",
  "description": "Arrumando a casa",
  "personal_reward": "Bolo de chocolate",
  "dificulty": "medio",
  "userId": 3,
  "id": 2
}
```

Para deletar um habito: 

`DELETE /habits/{id do habito} -  FORMATO DA REQUISIÇÃO`

```json
{
  "userId": 3,
}
```

`FORMATO DA RESPOSTA - STATUS 200`
```json
[]
```
