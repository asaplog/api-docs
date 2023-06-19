# Rastreio

A API de Rastreio de Pedido da ASAP Log serve para que você possa rastrear um pedido de entrega. Você deve fazer um GET para nosso endpoint, seguido do código de rastreio que você recebeu ao fazer o Pedido de Entrega.

As respostas podem ser validadas pelos status HTTP 200 (Rastreio recebido com sucesso) ou HTTP 404 (Pedido não encontrado).

Caso o status seja 200, você pode ler todos os dados do rastreio para armazenar e exibir em seu sistema.


## Dados Recebidos do Rastreio:

| Parâmetro              | Descrição                         |
|------------------------|-----------------------------------|
| numeroNfe              | Número da Nota Fiscal             |
| documentoConsumidor    | Documento do Consumidor           |
| origem                 | Dados do Endereço de Origem       |
| destino                | Dados do Endereço de Destino      |
| dataEnviada            | Data em que o Pedido foi coletado |
| previsaoEntrega        | Data de Previsão de Entrega       |
| prazoMaximo            | Prazo Máximo de Entrega           |
| etapas                 | Todas Etapas de Entrega           |
| tentativasEntrega      | Tentativas de Entrega             |
| status                 | Status Atual do Pedido            |
| statusMessage          | Status                            |
| statusMessageDetalhada | Status detalhado                  |


Tipos de Etapas:
- COLETA_CLIENTE
- ENTREGA_HUB_TRANSPORTADORA
- COLETA_HUB_TRANSPORTADORA
- ENTREGA_CONSUMIDOR

Tipos de Status de Pedido:
- NAO_COLETADO
- COLETADO_LOJA
- EMABARCAR_PARA_TRANSPORTE
- EM_VIAGEM
- TENTATIVA_ENTREGA
- EM_ROTA
- PROGRAMADO_ROTA
- ENTREGUE
- PROBLEMA_COM_ENTREGA


# Rastrear um pedido

GET https://app.asaplog.com.br/webservices/v1/rastrearPedidoEntrega/[CÓDIGO DE RASTREIO]

## Request

## Response

Rastreio recebido com sucesso.

200

## Headers

Content-Type:application/json

## Body
```
{
  "numeroNfe": "25992381",
  "documentoConsumidor": "99999999985",
  "origem": {
    "logradouro": "Rua Andre",
    "numero": "255",
    "bairro": "Bronx",
    "cidade": "Curitiba",
    "cep": "09835290",
    "uf": "PR",
    "complemento": "Apto 945",
    "codigoMunicipio": "4106902"
  },
  "destino": {
    "logradouro": "Rua Andre",
    "numero": "255",
    "bairro": "Bronx",
    "cidade": "Curitiba",
    "cep": "09835290",
    "uf": "PR",
    "complemento": "Apto 945",
    "codigoMunicipio": "4106902"
  },
  "dataEnviada": "2018-06-15T08:48:26Z",
  "previsaoEntrega": "2018-06-21",
  "prazoMaximo": "2018-06-26",
  "etapas": [
    {
      "dataRealizada": "2018-06-15T08:48:26Z",
      "dataPrevista": "2018-06-15",
      "status": "COLETA_CLIENTE",
      "statusMessage": "Coletado na loja"
    },
    {
      "dataRealizada": "2018-06-15T12:48:26Z",
      "dataPrevista": "2018-06-15",
      "status": "ENTREGA_HUB_TRANSPORTADORA",
      "statusMessage": "Unidade de origem da transportadora"
    },
    {
      "dataRealizada": "2018-06-15T12:48:26Z",
      "dataPrevista": "2018-06-15",
      "status": "COLETA_HUB_TRANSPORTADORA",
      "statusMessage": "Unidade de destino da transportadora"
    },
    {
      "dataRealizada": null,
      "dataPrevista": "2018-06-18",
      "status": "ENTREGA_CONSUMIDOR",
      "statusMessage": "Entregue"
    }
  ],
  "tentativasEntrega": [
    {
      "dataRealizada": "2018-06-20T08:48:26Z",
      "ocorrencia": "Destinatário Ausente",
      "nome": null,
      "documento": null
    },
    {
      "dataRealizada": "2018-06-21T08:48:26Z",
      "ocorrencia": "Destinatário Ausente segunda tentativa",
      "nome": null,
      "documento": null
    },
    {
      "dataRealizada": "2018-06-22T08:48:26Z",
      "ocorrencia": "Entregue",
      "nome": "Jose Alves",
      "documento": "98741565825"
    }
  ],
  "status": "NAO_COLETADO",
  "statusMessage": "Em breve será coletado na loja",
  "statusMessageDetalhada": "Seu pedido foi entregue! A pessoa que recebeu foi Jose Alves com número de documento 98741565825"
}
```