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

## Comando para pesquisar livro por autor:
aws dynamodb query \
    --table-name livro \
    --key-condition-expression "Autor = :autor" \
    --expression-attribute-values  '{":autor":{"S":"Machado de Assis"}}'

## Comando para pesquisar livro por autor e Titulo da obra:
aws dynamodb query \
    --table-name livro \
    --key-condition-expression "Autor = :autor and Titulo = :titulo" \
    --expression-attribute-values '{":autor":{"S":"José de Alencar"}, ":titulo":{"S":"O Guarani"}
}
