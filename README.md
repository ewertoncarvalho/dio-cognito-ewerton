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

Service - DynamoDB -> Manual actions -> add actions -> putItem

![Untitled 18](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/e9f7b0d7-230a-4141-8df6-31de9b57287c)

![Untitled 19](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/8fa7f307-af16-4301-9705-ad795a4f9370)

Resources -> Add arn -> Selecionar o arn da tabela criada no DynamoDB -> Add

![Untitled 20](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/ed58f20e-13bd-4312-a530-90aae3d778e2)

![Untitled 21](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/e6fa566f-0d28-4670-9c01-abadc5fb4f75)

Review policy -> Name [lambda_dynamodb_putItem_policy] -> Review policy → Create policy

![Untitled 22](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/05605037-5eeb-4720-ba95-f6fc1414238e)

Criar nome da policy → putitem_policy

![Untitled 23](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/680b8338-e846-4674-b5a5-e65d991bad64)

### Integrando o API Gateway com o Lambda backend

- API Gateway Dashboard -> Selecionar a API criada -> Resources -> Selecionar o resource criado -> Action -> Create method - POST

![Untitled 24](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/b830585e-f68c-4633-ac4d-b9b479036952)

![Untitled 25](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/960d484f-69db-402f-9492-ccaca7c9a7af)

![Untitled 26](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/11832328-7f44-479c-8d18-81c88481d467)

Integration type -> Lambda function -> Use Lambda Proxy Integration -> Lambda function -> Selecionar a função Lambda criada -> Save

![Untitled 27](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/e999ca89-958e-4226-ad58-b66d364e9996)

Lambda function

![Untitled 28](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/db1840fd-ce41-4d07-8452-e80612ad2895)

Ok na permissão

![Untitled 29](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/d3966948-2ebb-4e09-879d-6f7780f54149)

Clique em Method Request

![Untitled 30](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/4da4ea47-8902-4d0d-bb03-5dce2933bb86)

Actions -> Deploy API -> Deployment Stage -> New Stage [dev] -> Deploy

![Untitled 31](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/859291ea-41c7-4960-b6b5-03796e3c8d0a)

![Untitled 32](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/41ef2eff-fc97-439e-b696-18454387acad)

Copie a url para inserir no postmam

![Untitled 33](https://github.com/ewertoncarvalho/dio-cognito-ewerton/assets/49257517/1b13569c-a5ae-4e52-aebc-8e2a975b9e3a)

### No POSTMAN

- Add Request -> Method POST -> Copiar o endpoint gerado no API Gateway
- Body -> Raw -> JSON -> Adicionar o seguinte body

{
  "id": "003",
  "price": 600
},

 Send

### No Amazon Cognito

- Cognito Dashboard -> Manage User Pools -> Create a User Pool -> Pool name [TestPool]
- How do you want your end users to sign in? - Email address or phone number -> Next Step
- What password strength do you want to require?
- Do you want to enable Multi-Factor Authentication (MFA)? Off -> Next Step
- Do you want to customize your email verification messages? -> Verification type - Link -> Next Step
- Which app clients will have access to this user pool? -> App client name [TestClient] -> Create App Client -> Next Step
- Create Pool
- App integration -> App client settings -> Enabled Identity Providers - Cognito User Pool
- Callback URL(s) [[https://example.com/logout](https://example.com/logout)]
- OAuth 2.0 -> Allowed OAuth Flows - Authorization code grant -Implicit grant
- Allowed OAuth Scopes - email - openid
- Save Changes
- Domain name -> Domain prefix [diolive] -> Save

### Criando um autorizador do Amazon Cognito para uma API REST no Amazon API Gateway

- API Gateway Dashboard -> Selecionar a API criada -> Authorizers -> Create New Authorizer
- Name [CognitoAuth] -> Type - Cognito -> Cognito User Pool [pool criada anteriormente] -> Token Source [Authorization]
- Resources -> selecionar o resource criado -> selecionar o método criado -> Method Request -> Authorization - Selecionar o autorizador criado

### No POSTMAN

- Add request -> Authorization
- Type - OAuth 2.0
- Callback URL [[https://example.com/logout](https://example.com/logout)]
- Auth URL [[https://diolive.auth.sa-east-1.amazoncognito.com/login](https://diolive.auth.sa-east-1.amazoncognito.com/login)]
- Client ID - obter o Client ID do Cognito em App clients
- Scope [email - openid]
- Client Authentication [Send client credentials in body]
- Get New Acces Token
- Copiar o token gerado
- Selecionar a request para inserir item criada -> Authorization -> Type - Bearer Token -> Inserir o token copiado
- Send










