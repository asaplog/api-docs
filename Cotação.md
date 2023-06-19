# Cotação

A API de Rastreio de Pedido da ASAP Log serve para que você possa consultar a cotação de um frete. Para fazer uma cotação de frete, você deve fazer um GET para nosso endpoint, contendo os dados do pedido que será enviado.

As respostas podem ser validadas pelos status HTTP 200 (Cotação feita com sucesso), HTTP 400 (Valor, Peso e CEP são obrigatórios) ou HTTP 422 (Região de Entrega não atendida ou Negociação não encontrada para Peso ou Região).

| Parâmetro    | Obrigatório | Descrição               | Exemplo      |
|--------------|-------------|-------------------------|--------------|
| peso         | Sim         | Double                  | -            |
| valor        | Sim         | Double                  | -            |
| cep          | Sim         | CEP do local de destino | 81870120     |
| altura       | Não         | Altura do Produto       | 120 (120 cm) |
| largura      | Não         | Largura do Produto      | 45 (45 cm)   |
| profundidade | Não         | Profundidade do Produto | 60 (60 cm)   |

## Realizar cotação

GET https://app.asaplog.com.br/webservices/v1/consultarFrete?peso=[PESO]&valor=[VALOR]&cep=[CEP]&altura=[ALTURA]&largura=[LARGURA]&profundidade=[PROFUNDIDADE]

## Request

## Response

Cotação realizada com sucesso.

200

## Headers

Content-Type:application/json

## Body
```
{
  "preco": 8.72,
  "prazoMinimo": 1,
  "prazoMaximo": 3,
  "mensagem": null,
  "status": 200

}
```
## Response

Valor, Peso e CEP são obrigatórios.

400

## Headers

Content-Type:application/json

## Body
```
{
  "mensagem": "Valor e CEP são obrigatórios"
}
```
## Response

Região de Entrega não atendida ou Negociação não encontrada para Peso ou Região.

402

## Headers

Content-Type:application/json

## Body
```
{
  "mensagem": "Negociação não encontrada para Peso ou Região"
}
```