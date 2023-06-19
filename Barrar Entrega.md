# Barrar Entrega

API para solicitar impedir que o pedido seja entregue por qualquer motivo. Recebemos 3 campos obrigatórios para localizar o pedido: numeroNf, serieNf e cnpjEmitente. É possível enviar um motivo em texto, não obrigatório, para a solicitação de barrar.

| Parâmentro   | Obrigatório | Tipo   | Descrição                              |
| ------------ | ----------- | ------ | -------------------------------------- |
| numeroNF     | Sim         | String | Número da Nota Fiscal                  |
| sérieNF      | Sim         | String | Série da Nota Fiscal                   |
| cnpjEmitente | Sim         | String | CNPJ de quem emitiu o pedido           |
| motivo       | Não         | String | Motivo para solicitar barrar a entrega |

## Solicitar barrar entrega de pedidos

POST: https://app.asaplog.com.br/webservices/v1/webservices/v1/nfe/barrar-entrega

## Request

### Headers

Content-Type:application/json

Authorization:Basic [base64 de autenticação]

### Body

```
{
  "numeroNf": "2308198900",
  "serieNf": "1",
  "cnpjEmitente": "33041260184206",
  "motivo": "Pedido com suspeita de fraude."
}
```

## Response

200

## Headers

Content-Type:application/json

## Body

```
{
  "status": "SUCESSO",
  "mensagem": "Solicitação efetuada com sucesso.",
  "idSolicitacao": "6321936fffa2923eed662a6b"
}
```

## Response

400

## Headers

Content-Type:application/json

## Body

```
{
  "errorMsgs": [
    "numeroNf: não pode estar em branco",
    "cnpjEmitente: não pode estar em branco",
    "serieNf: não pode estar em branco"
  ]
}
```

## Response

403

## Headers

Content-Type:application/json

## Body

```
{
  "status": "ERRO",
  "mensagem": "Request API aberta - usuário não encontrado ou não autorizado.",
  "idSolicitacao": null
}
```

## Response

500

## Headers

Content-Type:application/json

## Body

```
{
  "status": "ERRO",
  "mensagem": "NullPointerException",
  "idSolicitacao": null
}
```
