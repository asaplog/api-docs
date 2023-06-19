# Parceiros

A API de Parceiros da ASAP Log serve para que você possa abrir uma conta, cadastrar o endereço e receber um usuário para acesso com apenas uma chamada de API.

Você deve utilizar a URL: 
https://parceiros.api.asaplog.com.br/clienteComIntegracao

Os únicos campos não obrigatórios são grupoId e criarUsuario.

O campo grupoId serve para clientes grandes que necessitam agrupar os clientes em uma conta maior.

O campo criarUsuario serve para criar ou não um login de acesso para o https://painel.asaplog.com.br.



## Cadastrar uma loja

POST https://app.asaplog.com.br/webservices/v1/clienteComIntegracaoRequest

## Headers


Content-Type:application/json

Authorization:Basic [base64 de autenticação]

## Body
```
{
    "nome": "Loja Exemplo",
    "cnpj": "08.417.701/0001-32",
    "telefone": "(41) 99748-4158",
    "inscricaoEstadual": "Isento",
    "website": "https://asaplog.com.br",
    "nomeResponsavel": "Felipe Bocolowski",
    "emailResponsavel": "felipe-teste2@asaplog.com.br",
    "telefoneResponsavel": "(41) 99999-9999",
    "centroDistribuicao": {
        "logradouro": "Av. Água Verde",
        "numero": "1413",
        "complemento": "",
        "bairro": "Água Verde",
        "cidade": "Curitiba",
        "estado": "PR",
        "cep": "80620-200"
    },
    "criarUsuario": true,
    "grupoId": null"
}
```
## Response

Loja cadastrada com sucesso com login e senha de API.

201

## Headers

Content-Type:text/plain

## Body
```
{
  "clienteGuid": "60ca2ef87364aaafadd60846",
  "username": "e62cd3b6d1e2459fab6eb806kj3l189e",
  "password": "cc9f9d866f0f456i9j80363ee40f5889b0"
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