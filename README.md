# Tic-Tac-Toe
Projeto de uma API RESTful para um Jogo da velha que será implementado em Node+Express.

# Rooms

## Cadastro
Para o cadastro de uma sala, deve ser feito uma requisição do tipo `POST`, enviando dados sobre a sala. O retorno deverá ser um `room-id` válido que será atrelado a essa sala.

**Request:** `POST /room`

**Body:**
```javascript
{
    token: vjDaryJkR7fLRqff4SsmdidrFRrIBh1h,
    room-name: "challenge"
}
```

**Response:**
```javascript
{
    room-id: 6
}
```

**Exceptions:**
* Se já existir uma sala com esse nome
* Se o token não for válido para essa requisição
* Se o usuário já for dono de outra sala

## Consulta
Para a consulta de uma sala, deve ser feito uma requisição do tipo `GET`, onde o `room-id` é especificado no request. O retorno deverá conter informações sobre a sala consultada.

**Request:** `GET /room/{room-id}`

**Body:**
```javascript
{
    token: vjDaryJkR7fLRqff4SsmdidrFRrIBh1h
}
```

**Response:**
```javascript
{
    room-name: "challenge",
    board-status: [['X', ' ', ' '], 
                   [' ', ' ', ' '],
                   [' ', ' ', ' ']],
    owner-id: 5,
    challenger-id: 3,
    turn: 'X'
}
```

**Exceptions:**
* Se o `room-id` consultado não existir
* Se o token não for válido para essa requisição

## Deletar
Para deletar uma sala, deve ser feito uma requisição do tipo `DELETE`, onde o `room-id` é especificado no request.

**Request:** `DELETE /room/{room-id}`

**Body:**
```javascript
{
    token: vjDaryJkR7fLRqff4SsmdidrFRrIBh1h
}
```

**Exceptions:**
* Se o `room-id` consultado não existir
* Se o token não for válido para essa requisição

## Entrar
Para entrar em uma sala, deve ser feito uma requisição do tipo `PUT`, onde o `room-id` é especificado no request.

**Request:** `PUT /room/{room-id}`

**Body:**
```javascript
{
    token: vjDaryJkR7fLRqff4SsmdidrFRrIBh1h
}
```

**Exceptions:**
* Se o `room-id` consultado não existir
* Se o token não for válido para essa requisição
* Se ela já estiver cheia (`challenger-id` da sala estiver com um valor de `id` válido)
* Se o usuário for o próprio dono da sala ele não pode entrar como desafiante

## Pontuação
Para obter o ranking com as 10 maiores pontuações (vitórias) e seus respectivos detentores, deve ser feita uma requisição do tipo `GET`, enviando apenas o token do usuário que está realizando a requisição. O retorno deverá ser uma list de tamanho 10 na qual cada elemento é uma das posições com informações sobre o jogador, sua pontuação, seu ranking e seu id.

**Request:** `GET /highscores`

**Body:**
```javacript
{
    token: "rR0aOq1Q7M4GcXwzYi6FHthUPVJoRtPA"
}
```

**Response:**
```javascript
[
  {
    rank: 1,
    id: 23,
    user: {
      nickname: "vivi123",
      score-wins: 43,
      id: 2,
    }
  },
  {
    rank: 2,
    id: 42,
    user: {
      nickname: "starlord000",
      score-wins: 22,
      id: 13
    }
  },
  {
    rank: 3,
    id: 1,
    user: {
      nickname: "FRZ Drako",
      score-wins: 17,
      id: 17
    }
  },
]
```

**Exceptions:**
  * Se o token fornecido não possuir autoridade para solicitar a tabela de highscores
