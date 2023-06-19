# Carga

A API de consuta de carga da ASAP Log serve para rastrear em quais roteiros os pedidos com aquele código de carga se encontram. Você deve fazer um GET em nosso endpoint seguido do código da carga que os pedidos pertencem.

As respostas podem ser validadas pelos status HTTP 200 (Consulta de carga rcebida com sucesso) ou HTTP 404 (Carga ainda não roteirizada).

Caso o status seja 200, você receberá uma lista (array) com as informações separada por pedido.

| Parâmetro            | Descrição                                                             |
|----------------------|-----------------------------------------------------------------------|
| idPedido             | ID do pedido internamente no sistema (apenas para referência)         |
| codigoCarga          | O código da carga que foi consultado                                  |
| numeroDocumento      | O número informado no campo numeroNf                                  |
| tipoDocumento        | O tipo de documento informado ao cadastrar o pedido (PVE, STD ou OSE) |
| sequenciaAtendimento | A sequencia de entrega daquele pedido dentro do roteiro               |
| cubagem              | Cubagem do veículo utilizado para o roteiro                           |
| codigoRoteiro        | Código do roteiro no sistema                                          |
| placa                | Placa do veículo que irá executar o roteiro                           |
| cnpjTransportadora   | CNPJ da transportadora responsável pela execução daquele roteiro      |

## Consulta de carga

GET: https://app.asaplog.com.br/webservices/v1/carga/[CÓDIGO DA CARGA]Request

### Response

Consulta recebida com sucesso

200

## Headers

Content-Type:application/json

## Body
```
[
  {
    "idPedido": "602ffb6f0eecad604ab5033a",
    "codigoCarga": "23081989",
    "numeroDocumento": "35117",
    "tipoDocumento": "PVE",
    "sequenciaAtendimento": 3,
    "cubagem": 22.5,
    "codigoRota": "DIR_20210302_212",
    "placa": "DIR7221",
    "cnpjTransportadora": "16.750.494/0001-61"
  },
  {
    "idPedido": "602ffb6f0eecad604ab5033a",
    "codigoCarga": "23081989",
    "numeroDocumento": "35117",
    "tipoDocumento": "STD",
    "sequenciaAtendimento": 1,
    "cubagem": 22.5,
    "codigoRota": "DIR_20210302_212",
    "placa": "DIR7221",
    "cnpjTransportadora": "16.750.494/0001-61"
  },
  {
    "idPedido": "602ffb6f0eecad604ab5033a",
    "codigoCarga": "23081989",
    "numeroDocumento": "35117",
    "tipoDocumento": "OSE",
    "sequenciaAtendimento": 2,
    "cubagem": 22.5,
    "codigoRota": "DIR_20210302_212",
    "placa": "DIR7221",
    "cnpjTransportadora": "16.750.494/0001-61"
  }
]
```

### Response

404

## Headers

Content-Type:application/json

## Body

Carga ainda não roteirizada