
<h1 align="center">Habitum - API</h1>

<p align="center">Este é o backend da aplicação Habitum - Um hub para quem quer criar e manter seu habito!</p>


<p align="center">
  <a href="#endpoints">Endpoints</a>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</p>


## **Endpoints**


A API tem um total de ...

O url base da API é https://habitum-fakeapi-v1.onrender.com

<h2 align ='center'> Cadastrando Usúarios </h2>

`POST /register -  FORMATO DA CORPO`
```json
 "img": 
 "name": 
 "userName":
 "email":
 "password":
```
`FORMATO DA RESPOSTA - STATUS 200`
```json
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImpvcmdlQG1haWwuY29tIiwiaWF0IjoxNjcyNzc0ODE5LCJleHAiOjE2NzI3Nzg0MTksInN1YiI6IjEifQ.Ysj_5jUeQ-TbzxkJpljoHAj7FLaT8B51wRa7UzWAK5o",
	"user": {
		"email": "jorge@mail.com",
		"name": "Jorge Rodrigo",
		"id": 1
	}
}
```
