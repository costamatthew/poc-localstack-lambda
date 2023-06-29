# Criação e Execução de Lambda Function a partir do Localstack

### Instale as dependencias:

- <code>npm install</code> <br/>

### Zipar nossa função:

- <code>zip -r function.zip .</code> <br/>

### Exemplo da nossa função atual:

- <code>zip -r function.zip index.js package.json package-lock.json node_modules/</code> <br/>

### Rodar localstack:

- <code>docker-compose up</code> <br/>

### Em um novo terminal, rodar esse comando para criação da nossa lambda no localstack:

- <code>aws --endpoint-url=http://localhost:4566 \
  lambda create-function --function-name my-lambda \
  --zip-file fileb://lambda-src/function.zip \
  --handler index.handler --runtime nodejs12.x \
  --role arn:aws:iam::000000000000:role/lambda-role</code> <br/>

### Verificar se nossa lambda foi criada:

- <code>aws --endpoint-url=http://localhost:4566 lambda get-function --function-name my-lambda</code> <br/>

### Criar roles da nossa lambda:

- <code>aws --endpoint-url=http://localhost:4566 iam create-role --role-name lambda-role --assume-role-policy-document file://trust-policy.json</code> <br/>
- <code>aws --endpoint-url=http://localhost:4566 iam attach-role-policy --role-name lambda-role --policy-arn arn:aws:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole</code> <br/>

## Testar lambda:

- <code>aws --endpoint-url=http://localhost:4566 lambda invoke --function-name my-lambda output.txt</code> <br/>
