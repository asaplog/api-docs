# Receber Ocorrências

**Ambiente de Homologação**

**POST** `https://api-preprod.asaplog.com.br/api/v1/asaplog/ocorrencia`

**Ambiente de Produção**

**POST** `https://api.asaplog.com.br/api/v1/asaplog/ocorrencia`

Este serviço visa disponibilizar ao transportador, a possibilidade de enviar novas ocorrências de entregas/coletas,
acrescentando desta forma, novas informações ao histórico das solicitações.
Para que a API receba corretamente as informações, os dados devem ser enviados conforme padrões estabelecidos abaixo.
Em todas as requisições válidas, o sistema irá retornar uma estrutura de mensagem de retorno em formato JSON, conforme
listado nas definições abaixo.

**Autenticação**

Para ambos os ambientes, a autenticação é feita por meio de uma apiKey gerada previamente e enviada como HEADER nas
requisições HTTP como se
segue:

Tipo: `via HEADER`

Key: X-ASAP-Log-API-Key

Value: apiKey fornecida previamente para transportadora

Content: `application/json`

## Estrutura JSON das Ocorrências:

| Parâmetro        | Obrigatório | Tipo  | Descrição                                                           |
|------------------|-------------|-------|---------------------------------------------------------------------|
| flagProducao     | Sim         | bool  | Determina o ambiente para qual as ocorrências estão sendo enviadas. |
| listaOcorrencias | Sim         | array | Lista de Ocorrências. Objeto descrito na seção "listaOcorrencias"   |

## listaOcorrencias:

| Parâmetro           | Obrigatório | Tipo     | Descrição                                                                                                                                                                                               |
|---------------------|-------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| model               | Sim         | string   | remetente / tomador / expedidor                                                                                                                                                                         |
| cnpj                | Sim         | string   | CNPJ do citado no atributo 'model'                                                                                                                                                                      |
| servico             | Sim         | int      | 3 - Entrega Agendada / 4 - Entrega Convencional / 5 - Transfêrencia de carga / 8 - Entrega Expressa / 9 - Entrega B2B / 11 - Entrega Same Day / 12 - Logística Reversa B2B / 13 - Logística Reversa B2C |
| dtOcorrencia        | Sim         | dateTime | Data de Ocorrência                                                                                                                                                                                      |
| codigoOcorrencia    | Sim         | string   | Código da ocorrências registrada na tabela de De/Para                                                                                                                                                   |
| descricaoOcorrencia | Não         | string   | Descrição/observações da ocorrências                                                                                                                                                                    |
| nroNotaFiscal       | Sim         | int      | Número da NF da solicitação                                                                                                                                                                             |
| serieNotaFiscal     | Sim         | short    | Série da NF da solicitação                                                                                                                                                                              |
| nroPedido           | Não         | string   | Número do pedido registrado na Nota Fiscal da solicitação                                                                                                                                               |
| codigoRastreio      | Não         | string   | Código de rastreamento registrado no volume                                                                                                                                                             |
| latitude            | Não         | string   | Latitude registrada na ocorrência                                                                                                                                                                       |
| longitude           | Não         | string   | Longitude registrada na ocorrência                                                                                                                                                                      |
| unidadeOcorrencia   | Não         | string   | Unidade onde a ocorrência foi registrada                                                                                                                                                                |
| nomeCidade          | Sim         | string   | Cidade onde a ocorrência foi registrada                                                                                                                                                                 |
| uf                  | Sim         | string   | Estado (Unidade Federativa) onde a ocorrência foi registrada                                                                                                                                            |
| nomeCidadeDestino   | Não         | string   | Cidade de destino da Transferência                                                                                                                                                                      |
| ufDestino           | Não         | string   | Estado (Unidade Federativa) onde a ocorrência foi registrada                                                                                                                                            |
| nomeRecebedor       | Não         | string   | Nome do recebedor do pedido                                                                                                                                                                             |
| documentoRecebedor  | Não         | string   | Documento do recebedor do pedido                                                                                                                                                                        |
| listaEvidencias     | Não         | array    | Lista de evidências da ocorrência. Objeto descrito na seção "listaEvidencias"                                                                                                                           |

## listaEvidencias:

| Parâmetro | Obrigatório | Tipo   | Descrição                                      |
|-----------|-------------|--------|------------------------------------------------|
| url       | Não         | string | URL da evidência/foto registrada na ocorrência |

## Exemplo de requisição:

```json
{
  "flagProducao": true,
  "listaOcorrencias": [
    {
      "model": "remetente",
      "cnpj": "12345678901234",
      "servico": 4,
      "dtOcorrencia": "2024-12-03 08:30:20",
      "codigoOcorrencia": "01",
      "descricaoOcorrencia": "Entrega realizada com sucesso",
      "nroNotaFiscal": "12345678",
      "serieNotaFiscal": "1",
      "nroPedido": "123456",
      "codigoRastreio": "1850610",
      "latitude": "-19.916681",
      "longitude": "-43.934493",
      "unidadeOcorrencia": "Filial BH",
      "nomeCidade": "Belo Horizonte",
      "uf": "MG",
      "nomeCidadeDestino": "Contagem",
      "ufDestino": "MG",
      "nomeRecebedor": "João da Silva",
      "documentoRecebedor": "09752957994",
      "listaEvidencias": [
        {
          "url": "https://app.asaplog.com.br/evidencias/1850610-1.jpg"
        },
        {
          "url": "https://app.asaplog.com.br/evidencias/1850610-2.jpg"
        }
      ]
    }
  ]
}
```

## Response

| Parâmetro  | Obrigatório | Tipo   | Descrição                                                                   |
|------------|-------------|--------|-----------------------------------------------------------------------------|
| flagError  | Sim         | bool   | Determina se houve o registro das ocorrências com erros ou não.             |
| listaErros | Sim         | array  | Lista de erros registrados para cada ocorrência.                            |
| info       | Sim         | string | O json contendo as informações das ocorrências enviadas no caso de sucesso. |

## Exemplo de response com sucesso em todas ocorrências:

```json
{
  "flagError": false,
  "listaErros": [],
  "info": {
    "flagProducao": true,
    "listaOcorrencias": [
      {
        "model": "tomador",
        "cnpj": "07430082000153",
        "servico": "4",
        "dtOcorrencia": "2018-08-22 10:00:00",
        "codigoOcorrencia": "10",
        "descricaoOcorrencia": "",
        "nroNotaFiscal": "27935",
        "serieNotaFiscal": "1",
        "nroPedido": "266923528603",
        "codigoRastreio": "PY123465789BR",
        "latitude": "",
        "longitude": "",
        "unidadeOcorrencia": "",
        "nomeCidade": "Su00E3o Paulo",
        "uf": "SP",
        "listaEvidencias": []
      },
      {
        "model": "tomador",
        "cnpj": "07430082000153",
        "servico": "4",
        "dtOcorrencia": "2018-08-22 10:00:00",
        "codigoOcorrencia": "10",
        "descricaoOcorrencia": "Descriu00E7u00E3o ok",
        "nroNotaFiscal": "27936",
        "serieNotaFiscal": "1",
        "nroPedido": "106896716403",
        "codigoRastreio": "",
        "latitude": "",
        "longitude": "",
        "unidadeOcorrencia": "",
        "nomeCidade": "Su00E3o Paulo",
        "uf": "SP",
        "listaEvidencias": [
          {
            "url": "https://app.asaplog.com.br/evidencias/1850610-1.jpg"
          },
          {
            "url": "https://app.asaplog.com.br/evidencias/1850610-2.jpg"
          }
        ]
      }
    ]
  }
}
```

## Exemplo de response com erro:

```json
{
  "flagError": true,
  "listaErros": [
    "Ocorrência 1: Model requerido",
    "Ocorrência 1: Cnpj requerido",
    "Ocorrência 1: Nome da cidade requerido",
    "Ocorrência 1: Data da ocorrência requerido",
    "Ocorrência 1: Código da ocorrência requerido",
    "Ocorrência 1: Série da nota fiscal requerido",
    "Ocorrência 1: Número da nota fiscal requerido",
    "Ocorrência 1: UF requerido",
    "Ocorrência 1: Serviço requerido"
  ],
  "info": null
}
```

## HTTP Status Codes

- 200 - Sucesso no processamento das ocorrências (Na resposta JSON em "info.listaOcorrencias" todas ocorrências
  cadastradas)
- 400 - Os dados informados são inválidos
- 403 - Falha na autenticação da api
- 500 - Erro interno do sistema.
