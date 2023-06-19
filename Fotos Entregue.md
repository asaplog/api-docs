# Fotos Entregue

A API de fotos busca as fotos que o entregador parceiro tirou no momento de entrega do pedido ao consumidor final. As imagens irão vir em formato base64 no campo image64.

## Buscar fotos

GET https://app.asaplog.com.br/webservices/v1/fotosNFEntregue/[número da nota fiscal]Request

## Headers

Content-Type:application/json

Authorization:Basic [base64 de autenticação]

## Response

Fotos encontradas.

200

## Headers

Content-Type:text/plain

## Body

```
{
  "total": 2,
  "fotos": [
    {
      "id": "60787e0b53c294c26887e883",
      "caminhoRelativo": "https://asaplog-files.com/2021/04/15/60787e0b53c294c26887e883.jpg",
      "dateCreate": "2021-04-15T17:52:07Z",
      "image64": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAMCAgMCAgMDA...."
    },
    {
      "id": "60787e4053c294c26887e887",
      "caminhoRelativo": "https://asaplog-files.com/2021/04/15/60787e4053c294c26887e887.jpg",
      "dateCreate": "2021-04-15T17:52:59Z",
      "image64": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAMCAgMCAgMDA..."
    }
  ]
}
```

## Response

422

## Headers

Content-Type:application/json

## Body

```
[
  "CNPJ inválido: 11111111"
]
```
