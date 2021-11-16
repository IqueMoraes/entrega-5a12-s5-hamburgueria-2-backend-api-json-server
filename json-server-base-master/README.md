# 1- json-server-base a API.

Essa API é o backend da aplicação de venda de lanches online. As informações produzidas e repassadas poderão ser compartilhadas de forma pública ou restrita aos usuários cadastrados. Uma ferramenta de pedidos, elaboração de carrinho.

# 2- Endpoints

Esta API conta com 4 Endpoints.
USUÁRIO:
-Cadastro post /users
-Login post /users

Cardápio e Comentários em ESPAÇO ABERTO:
-Envio de opiniões sobre o restaurante post e get /restComments
-Acesso às opiniões sobre o restaurante post e get /restComments
-pratos e componentes disponíveis no cardápio get /meals

Carrinho em ESPAÇO RESTRITO:
-Envio de itens para o carrinho post /cart
-Acesso aos itens do carrinho get /cart
-Deleção de itens do carrinho delete /cart

# a) Cadastro

O endpoint de cadastro fica acessível com:
POST /signup

Onde no corpo do cadastro devem conter as informações de nome do usuário, função, email e senha.
O nome do usuário pode ser escrito com letras maíusculas e minúsculas, números e espaços.
A função deve ser escrita apenas em letras.
O email deve ter formatação própria de e-mail.
A senha podem conter números e letras.

Exemplo:
{ "name": "Machado de Assis",
"email": "machado.da@abl.com.br",
"senha": "benculpado",
}

e deve retornar:

            {
            "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im1hY2hhZG8uZGFAYWJsLmNvbS5iciIsImlhdCI6MTYzNTI2MDMyMiwiZXhwIjoxNjM1MjYzOTIyLCJzdWIiOiIzIn0.B6byz7WgpWmEfi6ZCsCixmKDkKyhjkwb9mARNClrWz4",
            "user": {
                "email": "machado.da@abl.com.br",
                "name": "Machado de Assis",
                "id": 3
            }
            }

# b) Login

O endpoint de login fica acessível com:
POST /signin

Para o Login devem conter no corpo da requisição o e-mail e senha.

Exemplo:
{
"email": "machado.da@abl.com.br",
"senha": "benculpado",
}

Deve retornar:
{
"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im1hY2hhZG8uZGFAYWJsLmNvbS5iciIsImlhdCI6MTYzNTI2MDQ2NSwiZXhwIjoxNjM1MjY0MDY1LCJzdWIiOiIzIn0.7XlndFvlVKgjp5fJoObGKXZAqccouLRoeJggEKbPic4",
"user": {
"email": "machado.da@abl.com.br",
"name": "Machado de Assis",
"id": 3
}
}

# c)Espaço aberto - envio

Área de opiniões assinadas sobre o restaurante
Somente usuários logados poderão enviar informações para esse endpoint.

Para requisição:
POST /restComments

No corpo da requisição deve conter a informação no campo "myopinion" e o campo "speaker" é opcional.

Exemplo:
{
"myreview": "Ótimos hambúrgueres!",
"author": "Machado de Assis",
"date": 'Thu Oct 28 2021 16:27:01 GMT-0300 (Horário Padrão de Brasília)'
}

Deve retornar a informação enviada com o número de id atribuído:

            {
            "myreview": "Ótimos hambúrgueres!",
            "author": "Machado de Assis",
            "date": 'Thu Oct 28 2021 16:27:01 GMT-0300 (Horário Padrão de Brasília)',
            "id": 7
            }

# d)Espaço aberto - acesso

Área de opiniões emitidas por usuários inscritos.
Usuários sem cadastro podem acessar as informações.

Para requisição:
GET /restComments

Não é necessário informação no corpo da requisição.

Deve retornar:
[
{
"myreview": "Ótimos hambúrgueres!",
"author": "Machado de Assis",
"date": 'Thu Oct 28 2021 16:27:01 GMT-0300 (Horário Padrão de Brasília)',
"id": 7
},
{
"myreview": "As batatas fritas são super crocantes!",
"author": "Jose",
"date": 'Thu Oct 28 2021 16:27:01 GMT-0300 (Horário Padrão de Brasília)',
"id": 8
}
]

# e)Cardápio - Espaço aberto - acesso

Endpoint de retorno com todos os pratos disponíveis.

Para requisição:
GET /meals


# f)Espaço restrito - envio

Itens do menu a serem enviados para o banco de dados.
Usuários logados poderão enviar informações para esse endpoint.

Para requisição:
POST /cart

No header da requisição deve conter o token de acesso do usuário logado no portador

Bearer _acess token_

e no corpo da requisição as informações do item a ser adicionado(objeto da lista do menu + quantidade) e o número do id do usuário em "userId".

Exemplo:
{
      "userId": 5,
      "order": [
        {
          "title": "Filé de peixe com molho de manjericão, brócolis ao alho e tomate ao forno",
          "category": "food",
          "meat": "fish",
          "price": 38.5,
          "discount": 0,
          "id": 5,
          "quantity":1
        }
      ]
}

Deve retornar:

    {
            "userId": 5,
            "order": [
                {
                "title": "Filé de peixe com molho de manjericão, brócolis ao alho e tomate ao forno",
                "category": "food",
                "meat": "fish",
                "price": 38.5,
                "discount": 0,
                "id": 5,
                "quantity":1
                }
            ],
            "id": 1
    },

# g)Espaço restrito - acesso

Lista de itens adicionados ao carrinho.
Somente usuários proprietários e logados podem acessar as informações do seu carrinho.

Para requisição:
GET /cart?userId={id do usuário}

No header da requisição deve conter o token de acesso do usuário logado no portador

Bearer _acess token_

Não é necessário informação no corpo da requisição.

Deve retornar:
{
            "userId": 5,
            "order": [
                {
                "title": "Filé de peixe com molho de manjericão, brócolis ao alho e tomate ao forno",
                "category": "food",
                "meat": "fish",
                "price": 38.5,
                "discount": 0,
                "id": 5,
                "quantity":1
                }
            ],
            "id": 1
    },

# h)Espaço restrito - adição/exclusão

Adição e exclusão de itens do carrinho.
Somente usuários proprietários e logados podem adicionar e excluir as informações do seu carrinho.

Para requisição:
patch /cart/{id do carrinho}

No header da requisição deve conter o token de acesso do usuário logado no portador

Bearer _acess token_

e no corpo da requisição as informações do item a ser excluído(filtrado) (objeto da lista do menu + quantidade) e o número do id do usuário em "userId".

Exemplo:
{
      
      "order": [ 
        {
          "title": "Filé de peixe com molho de manjericão, brócolis ao alho e tomate ao forno",
          "category": "food",
          "meat": "fish",
          "price": 38.5,
          "discount": 0,
          "id": 5,
          "quantity": 3
        }
      ]
}

