# awsDynamoDB -comandos para execução no DynamoDB AWS

## Comando para criar tabela:
aws dynamodb create-table \
    --table-name livro \
    --attribute-definitions \
        AttributeName=Autor,AttributeType=S \
        AttributeName=Titulo,AttributeType=S \
 	AttributeName=Editora,AttributeType=S \
    --key-schema \
        AttributeName=Autor,KeyType=HASH \
        AttributeName=Titulo,KeyType=RANGE \
    --provisioned-throughput \
        ReadCapacityUnits=10,WriteCapacityUnits=5

## Comando para adicionar registro:
aws dynamodb put-item \
    --table-name Music \
    --item file://livro.json \

## Comando para adicionar múltiplos registros:
aws dynamodb batch-write-item \
    --request-items file://livros.json
