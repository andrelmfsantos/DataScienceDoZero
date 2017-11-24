# DataScienceDoZero
Improvement Python Script for Data Science Zero Book

### Encontrando conectores chaves - Livro Data Science do Zero, pg.3
## Obs.: O código original foi mudado pois foi encontrado erro no script devido a incompatibilidade com o Python 3.0

# Lista de usuários
users = [
    { "id": 0, "name": "Hero" },
    { "id": 1, "name": "Dunn" },
    { "id": 2, "name": "Sue" },
    { "id": 3, "name": "Chi" },
    { "id": 4, "name": "Thor" },
    { "id": 5, "name": "Clive" },
    { "id": 6, "name": "Hicks" },
    { "id": 7, "name": "Devin" },
    { "id": 8, "name": "Kate" },
    { "id": 9, "name": "Klien" },
]

# Lista de pares de IDs (i,j), ou seja o par (0, 1) representa a relação do "id:0" com "id:1". Por exemplo, a tupla (0, 1) indica que Hero e Dunn são amigos.
friendships = [(0, 1), (0, 2), (1, 2), (1, 3), (2, 3), (3, 4),
               (4, 5), (5, 6), (5, 7), (6, 8), (7, 8), (8, 9)]

# Lista vazia de friends
for user in users:
    user["friends"] = []
    
# Lista povoada com dados de friends
for i, j in friendships:
    users[i]["friends"].append(users[j])
    users[j]["friends"].append(users[i])
    
# Encotra o total de conexões
def number_of_friends(user):
    return len(user["friends"])  #tamanho da lista friend_ids

total_connections = sum(number_of_friends(user) for user in users)

print(total_connections)

import math   # pacote para fazer divisão, é possível também utilizar "__future__"

num_users = len(users)   # tamanho da lista de usuários
avg_connections = total_connections / num_users   # deve dar como resultado 2.4

print(avg_connections)   # imprime o resultado 2.4 que é a média de conexões por usuário

# cria uma lista (user_id, number_of_friends)
num_friends_by_id = [(user["id"], number_of_friends(user)) for user in users]

print(num_friends_by_id) # imprime como resultados a lista: [(0, 2), (1, 3), (2, 3), (3, 3), (4, 2), (5, 3), (6, 2), (7, 2), (8, 3), (9, 1)]. Obs: O 1º numero no par representa o id e o 2º o total de conexões.

many_friends = sorted(num_friends_by_id, key=lambda innerListItems: innerListItems[1], reverse=True)   # ordena os amigos com muitas para os com poucas conexões

print(many_friends) # imprime a lista: [(1, 3), (2, 3), (3, 3), (5, 3), (8, 3), (0, 2), (4, 2), (6, 2), (7, 2), (9, 1)]

few_friends = sorted(num_friends_by_id, key=lambda innerListItems: innerListItems[1], reverse=False)  # imprime dos amigos com menos para os com mais conexões

print(few_friends)   #imprime a lista: [(9, 1), (0, 2), (4, 2), (6, 2), (7, 2), (1, 3), (2, 3), (3, 3), (5, 3), (8, 3)]

