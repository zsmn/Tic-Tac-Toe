# Tic-Tac-Toe
Projeto de uma API RESTful para um Jogo da velha que será implementado em Node+Express.

## Projeto das requisições API
### Requisições de Cadastro/Edição/Remoção de Usuários.

### Requisições de Login/Logout de Usuários.

### Requisições para Criar/Consultar/Deletar/Entrar em uma Sala.

### Requisição para obter as 10 maiores pontuações.
* Linha de requisição na mensagem HTTP: ```GET /highscores```
* Mensagem de requisição:
```
{
Token: "rR0aOq1Q7M4GcXwzYi6FHthUPVJoRtPA"
}
```
* Mensagem de resposta:
```
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

### Requisições para realização de jogadas em uma Sala por um Usuário.
