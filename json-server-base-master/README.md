# 1- json-server-base a API.

Essa API é o backend da aplicação de venda de lanches online. As informações produzidas e repassadas poderão ser compartilhadas de forma pública ou restrita aos usuários cadastrados. Uma ferramenta de pedidos, elaboração de carrinho.

# 2- Endpoints

Esta API conta com 7 Endpoints.
USUÁRIO:
-Cadastro    post   /users
-Login   post   /users

Comentários em ESPAÇO ABERTO:
-Envio de opiniões sobre o restaurante    post e get /restComments
-Acesso às opiniões sobre o restaurante    post e get /restComments

Cardápio e comentários em ESPAÇO RESTRITO:
-pratos e componentes disponíveis no cardápio      get /meals
-Envio de opiniões sobre os pratos     post /mealsComments
-Acesso às opiniões sobre os pratos     get /mealsComments




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




# e)Cardápio - Espaço restrito - acesso 

Endpoint de retorno com todos os pratos disponíveis.

Para requisição:
GET /meals



# f)Espaço restrito - envio

Área de opiniões assinadas.
Usuários logados poderão enviar informações para esse endpoint.

Para requisição:
POST /congress

No header da requisição deve conter o token de acesso do usuário logado no portador

Bearer *acess token* 

e no corpo da requisição as informações no campo "myopinion" e o número do id do usuário em "userId".

Exemplo: 
            {
                "myopinion": "Temos que promover o alistamento militar obrigatório",
                "userId": 4
                
            }

Deve retornar:

            {
            "myopinion": "Temos que promover o alistamento militar obrigatório",
            "userId": 4,
            "id": 2
            }




# g)Espaço restrito - acesso

Área de opiniões emitidas por usuários inscritos.
Somente usuários logados podem acessar as informações.

Para requisição:
GET /congress

No header da requisição deve conter o token de acesso do usuário logado no portador

Bearer *acess token* 


Não é necessário informação no corpo da requisição.

Deve retornar:
            [
            {
                "myopinion": "Temos que promover o alistamento militar obrigatório",
                "userId": 4,
                "id": 1
            }
            ]
