## Barrar Entrega via Asaplog API
API para solicitar o barramento do pedido.

### Biblioteca dos campos
| Campo        | Obrigatório | Tipo   | Descrição                              |
| ---          | ---         | ---    | ---                                    |
| numeroNf     | Sim         | String | Número da Nota Fiscal                  |
| serieNf      | Sim         | String | Série da Nota Fiscal                   |
| cnpjEmitente | Sim         | String | CNPJ de quem emitiu o pedido           |
| motivo       | Não         | String | Motivo para solicitar barrar a entrega |

### Request

POST https://api.asaplog.com.br/nfe/barrar-entrega

#### Header
    
```
Content-Type: application/json
X-ASAP-Log-API-Key: (API Key gerada)
```

#### Body
```
{
  "numeroNf": "2308198900",
  "serieNf": "1",
  "cnpjEmitente": "33041260184206",
  "motivo": "Pedido com suspeita de fraude."
}
```

### Response

#### Sucesso - 200 - Success
```
{
  "status": "SUCESSO",
  "mensagem": "Solicitação efetuada com sucesso.",
  "idSolicitacao": "6321936fffa2923eed662a6b"
}
```

#### Campos faltantes - 400 - Bad Request
```
{
  "errorMsgs": [
    "numeroNf: não pode estar em branco",
    "cnpjEmitente: não pode estar em branco",
    "serieNf: não pode estar em branco"
  ]
}
```

#### API Key inválida - 401 - Unauthorized
```
{
    "message": "API Key inválida"
}
```

#### Problema interno - 500 - Internal Server Error
```
{
    "status": "ERRO",
    "mensagem": "Cannot invoke ..."
}
```
