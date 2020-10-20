# Tic-Tac-Toe
Projeto de uma API RESTful para um Jogo da velha que será implementado em Node+Express.


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
