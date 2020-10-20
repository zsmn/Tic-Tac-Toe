# Tic-Tac-Toe
Projeto de uma API RESTful para um Jogo da velha que será implementado em Node+Express.

# Login/Logout

## Login 
* Para que um usuário possa realizar o login, deve ser feito uma requisição do tipo `POST`, enviando seu login e a sua password. O retorno deverá ser apenas um código de status, no qual 1 indica que ocorreu tudo bem, enquanto 0 indica que houve um erro e vai retornar também um token correspondente ao usuário.

**Request:** `POST /userLogin`

**Body:**
```javascript
{
    user: "incarnati0n",
    password: "gonnaClapFaker"
}
```

**Response:**
```javascript
{
    status: 1,
    token: "rR0aOq1Q7M4GcXwzYi6FHthUPVJoRtPA"
}
```

**Exceptions:**
* Se o usuário que está tentando realizar o login não foi cadastrado previamente
* Se o usuário já estiver logado no sistema

## Logout
* Para que um usuário possa realizar o logout, deve ser feito uma requisição do tipo `GET`, enviando apenas o seu token. Não possui mensagem de retorno.

**Request:** `DELETE /userLogout`

**Body:**
```javascript
{
    token: "rR0aOq1Q7M4GcXwzYi6FHthUPVJoRtPA"
}
```

**Exceptions:**
* Se o token em questão é de um usuário que ainda nem fez o login no sistema
* Se o token em questão não é de um usuário válido


# Usuários

## Cadastro
Para o cadastro de um usuário, deve ser feito uma requisição do tipo `POST`, enviando dados sobre o usuário. O retorno deverá ser um `id` válido atrelado ao usuário novo criado.

**Request:** `POST /user`

**Body:**
```javascript
{
    user: "usuario",
    pass: "senha",
    nickname: "ticmastertoe",
    mail: "usuario@abc.com"
}
```

**Response:**
```javascript
{
    id: 3
}
```

**Exceptions:**
* Quando algum dado fornecido não é válido:
    * Usuário já usado
    * Senha fraca para o sistema
    * Nickname já usado
    * E-mail já utilizado

## Remoção
Para a remoção de um usuaŕio específico, optamos pela requisição `DELETE` já que ela permite deletar recursos do servidor. Na requisição devemos especificar o `id` do usuário a ser deletado.
Como essa operação é destrutiva, enviamos um token no corpo da requisição que será verificado pelo servidor antes de efetuar, de fato, a remoção do usuário.

**Request:** `DELETE /user/{id}`

**Body:**
```javascript
{
    token: "saw93USeczog3CDmdOv6K30cMtLWFxjz"
}
```

**Exceptions:**
* Quando o token fornecido não possui autoridade para fazer a remoção.
* Quando o `id` inserido não existe no sistema

## Consulta
Para a consulta de usuários, optamos pela requisição `GET` já que ela permite consultar recursos do servidor. Analogamente à remoção de usuários, também especificamos na requisição o `id` do usuário a ser alterado. No corpo devemos ter um token para garantir autenticidade.

**Request:** `GET /user/{id}`

**Body:**
```javascript
{
    token: "saw93USeczog3CDmdOv6K30cMtLWFxjz"
}
```

**Response:**
```javascript
{
    nickname: "Vitrugo",
    score-wins: 100
}
```

**Exceptions:**
* Quando o token fornecido não possui autoridade para fazer a edição.
* Quando o `id` inserido não existe no sistema

## Edição
Para a edição de usuários, optamos pela requisição `PUT` já que ela permite alterar recursos do servidor. Analogamente à remoção de usuários, também especificamos na requisição o `id` do usuário a ser alterado. No corpo devemos ter um token para garantir autenticidade e especificar os campos a serem alterados, juntamente com os novos valores.

**Request:** `PUT /user/{id}`

**Body:**
```javascript
{
    token: "saw93USeczog3CDmdOv6K30cMtLWFxjz",
    nickname: "ticmastertac"
}
```

**Exceptions:**
* Quando o token fornecido não possui autoridade para fazer a edição.
* Quando o `id` inserido não existe no sistema
* Quando os campos inseridos não existirem ou possuirem valores invalidos ou já usados por outro usuário

# Rooms

## Cadastro
Para o cadastro de uma sala, deve ser feito uma requisição do tipo `POST`, enviando dados sobre a sala. O retorno deverá ser um `room-id` válido que será atrelado a essa sala.

**Request:** `POST /room`

**Body:**
```javascript
{
    token: "vjDaryJkR7fLRqff4SsmdidrFRrIBh1h",
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
    token: "vjDaryJkR7fLRqff4SsmdidrFRrIBh1h"
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
    turn: 'O'
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
    token: "vjDaryJkR7fLRqff4SsmdidrFRrIBh1h"
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
    token: "vjDaryJkR7fLRqff4SsmdidrFRrIBh1h"
}
```

**Exceptions:**
* Se o `room-id` consultado não existir
* Se o token não for válido para essa requisição
* Se ela já estiver cheia (`challenger-id` da sala estiver com um valor de `id` válido)
* Se o usuário for o próprio dono da sala ele não pode entrar como desafiante

## Jogada

Para executar uma jogada, deve ser feito uma requisição do tipo `POST`, onde o `room-id` é especificado no request.

**Request:** `POST /room/{room-id}`

**Body:**
```javascript
{
    token: "UfvL8unRP2YQLv3E8CbJriBWVQlkYMtu",
    row: 1,
    column: 2
}
```

**Exceptions:**
* Se não for a vez de quem requisitou a jogada
* Se a linha ou coluna forem inválidas
* Se a posição requisitada já está marcada
* Se o token não for válido para essa requisição

# Highscores

## Obtendo ranking com os 10 melhores jogadores
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
