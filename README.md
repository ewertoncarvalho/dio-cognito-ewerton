# dio-cognito-ewerton
Roteiro para o desenvolvimento da atividade prática do DIO Live Coding

Segurança em APIs na AWS com Amazon Cognito

![Arquitetura](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/2aaf323d-e877-41e2-b803-776fb012dd0c)

## Etapas do desenvolvimento

### Criando uma API REST no Amazon API Gateway

- API Gateway Dashboard -> Create API -> REST API -> Build
- **Choose the protocol** - REST -> Create new API -> **Settings →** API name [dio_live_api] -> Endpoint Type - Regional -> Create API

![Untitled 10](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/f1c76b4b-5300-4ad9-be03-1ef4c459b64b)

Resources -> Actions -> Create Resource -> Resource Name [Items] -> Create Resource

![Untitled 11](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/c67ba91e-0e6a-4bb6-9712-f4602ba5e7eb)

/item Methods criado

![Untitled 12](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/283d0b0d-13d7-48c5-8bec-4ad6b0e45b63)

### No Amazon DynamoDB

- DynamoDB Dashboard -> Tables -> Create table -> Table name [Items] -> Partition key [id] -> Create table
- DIOitems
- Partition key = id

![Untitled 13](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/8d94629d-d47c-4e32-99f5-9eadbce6cbf4)

![Untitled 14](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/13eb1a19-8caf-4514-9432-fa6efad16310)

### No AWS Lambda

### Função para inserir item

- Lambda Dashboard -> Create function -> Name [put_item_function] -> Create function

![Untitled 15](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/f6b90041-eb21-47e6-a716-3e46a3d8a0d3)

Inserir código da função put_item_function.js disponível na pasta /src -> Deploy

Configuration -> Permission → Execution role -> Abrir a Role no console do IAM
![Untitled 16](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/1a573939-107d-46e9-afe2-7cfe2e0c1c46)

IAM -> Roles -> Role criada no passo anterior -> Permissions -> Add inline policy

![Untitled 17](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/7bc590ac-72a7-49e7-93f6-168b4c34db4c)

