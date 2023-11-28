# Pedidos

A API de Pedidos da ASAP Log serve para que você possa registrar um pedido de entrega. Você deve fazer um POST com os dados da Nota Fiscal em JSON para nosso endpoint.

As respostas podem ser validadas pelos status HTTP 200 (Pedido cadastrado com sucesso) ou HTTP 400 (Erro ao cadastrar Pedido).

Caso o status seja 200, você deve guardar o valor do parâmetro codigoRastreio dado no JSON de resposta.

Caso o status seja 400, você pode capturar uma lista dos erros que ocorreram no parâmetro errorMsgs dado no JSON de resposta.

## Parâmetros do Pedido de Entrega:

| Parâmetro            | Obrigatório | Tipo    | Tamanho (máx. caracteres) | Descrição                                                                                        |
|----------------------|-------------|---------|---------------------------|--------------------------------------------------------------------------------------------------|
| numeroNf             | Sim         | String  | 20                        | Número da Nota Fiscal                                                                            |
| serieNf              | Sim         | String  | 5                         | Série da Nota Fiscal                                                                             |
| chaveAcesso          | Sim         | String  | 50                        | Chave de Acesso da Nota Fiscal                                                                   |
| pesoTotal            | Sim         | Double  | -                         | Peso Bruto da Nota Fiscal                                                                        |
| totalNota            | Sim         | Double  | -                         | Valor Total da Nota Fiscal                                                                       |
| qtdVolumes           | Sim         | Integer | -                         | Quantidade de Volumes da Nota Fiscal                                                             |
| descProd             | Não         | String  | 200                       | Descrição dos Produtos da Nota Fiscal                                                            |
| tpMed                | Não         | String  | 50                        | Tipo de Medida/Embalagem da Nota Fiscal                                                          |
| identificacaoCliente | Não         | String  | 50                        | Código de identificação do pedido para o cliente                                                 |
| tipoProduto          | Não         | String  | 50                        | Tipo do Produto (LINHA_BRANCA, MOVEIS ou OUTROS)                                                 |
| altura               | Não         | Double  | -                         | Altura (em metro, ex: 1 metro é 1.0) do Produto da Nota Fiscal                                   |
| largura              | Não         | Double  | -                         | Largura (em metro, ex: 75cm é 0.75) do Produto da Nota Fiscal                                    |
| profundidade         | Não         | Double  | -                         | Profundidade (em metro, ex: 30cm é 0.3) do Produto da Nota Fiscal                                |
| consumidor           | Sim         | -       | -                         | Dados do Consumidor da Nota Fiscal. Objeto descrito na seção "Parâmetros do Consumidor/Emitente" |
| emitente             | Sim         | -       | -                         | Dados do Emitente da Nota Fiscal. Objeto descrito na seção "Parâmetros do Consumidor/Emitente"   |
| itens                | Não         | -       | -                         | Dados dos itens. Array de objetos descrito abaixo na seção "Parâmetros dos Itens"                |
| codigoCarga          | Não         | String  | 50                        | Código da carga que o pedido irá pertencer                                                       |
| tipoDocumento        | Não         | String  | 20                        | Tipo do documento (PVE, STD ou OSE)                                                              |
| origem               | Não         | String  | 20                        | Origem do pedido (VIA ou UX). Usado para endereçar as ocorrências                                |
| dataEntregaPrevista  | Não         | Data    | -                         | Data prevista para entrega segundo a Via                                                         |

Parâmetros do Consumidor/Emitente:

Atenção: O consumidor/emitente deve ter CPF ou CNPJ.

| Parâmetro         | Obrigatório | Tipo   | Tamanho (máx. caracteres) | Descrição                                            |
|-------------------|-------------|--------|---------------------------|------------------------------------------------------|
| cnpj              | Sim para PJ | String | 20                        | CNPJ do Consumidor                                   |
| cpf               | Sim para PF | String | 20                        | CPF do Consumidor                                    |
| nome              | Sim         | String | 200                       | Nome Completo do Consumidor                          |
| logradouro        | Sim         | String | 200                       | Logradouro do Endereço do Consumidor                 |
| numero            | Sim         | String | 15                        | Número do Endereço do Consumidor                     |
| bairro            | Sim         | String | 50                        | Bairro do Endereço do Consumidor                     |
| cidade            | Sim         | String | 50                        | Cidade do Endereço do Consumidor                     |
| cep               | Sim         | String | 10                        | CEP do Endereço do Consumidor                        |
| uf                | Sim         | String | 2                         | UF do Endereço do Consumidor                         |
| complemento       | Não         | String | 200                       | Complemento do Endereço do Consumidor                |
| codMun            | Não         | String | 10                        | Código do Município do Endereço do Consumidor (IBGE) |
| telefone          | Não         | String | 50                        | Telefone para Contato do Consumidor                  |
| inscricaoEstadual | Não         | String | 20                        | Inscrição Estadual do Consumidor                     |

Parâmetros dos Itens:

Atenção: Pode ser enviado nenhum, um ou mais itens. Em casos de itens que são exatamente o mesmo, deve ser repassado um objeto para cada item (Ex: dois itens "TV Samsung" precisa vir dois objetos dentro de "itens").

| Parâmetro    | Obrigatório | Tipo   | Tamanho (máx. caracteres) | Descrição                                       |
|--------------|-------------|--------|---------------------------|-------------------------------------------------|
| descricao    | Não         | String | 200                       | Descrição do Item                               |
| peso         | Não         | Double | -                         | Peso Bruto do Produto                           |
| altura       | Não         | Double | -                         | Altura do Item (em metro, ex: 1 metro é 1.0)    |
| largura      | Não         | Double | -                         | Largura do Item (em metro, ex: 75cm é 0.75)     |
| profundidade | Não         | Double | -                         | Profundidade do Item (em metro, ex: 30cm é 0.3) |
| cubagem      | Não         | Double | -                         | Cubagem do Item (em metros cúbicos, ex: 0.4501) |


## Registrar um Pedido

POST https://app.asaplog.com.br/webservices/v1/pedidoEntregas

## Headers

Content-Type:application/json

Authorization:Basic [base64 de autenticação]

## Body
```
{
  "numeroNf": "154823",
  "serieNf": "001",
  "chaveAcesso": "99980999065189990194550010025153811211328157",
  "pesoTotal": 1.943,
  "totalNota": 845.32,
  "qtdVolumes": 1,
  "descProd": "Livro",
  "tpMed": "Caixa",
  "identificacaoCliente": "22091989",
  "tipoProduto": "LINHA_BRANCA",
  "altura": 0.1,
  "largura": 0.2,
  "profundidade": 0.5,
  "codigoCarga": "23081989",
  "tipoDocumento": "PVE",
  "origem": "VIA",
  "dataEntregaPrevista": "2022-08-23T02:00:00.000Z"
  "consumidor": {
    "nome": "João da Silva",
    "telefone": "(99) 99999-9999",
    "inscricaoEstadual": "0293854738",
    "cpf": "09752957994",
    "logradouro": "Rua Riachuelo",
    "numero": "1351",
    "bairro": "Padre Eustáquio",
    "cidade": "Belo Horizonte",
    "cep": "31170000",
    "uf": "MG",
    "complemento": "Ap. 1005",
    "codMun": "4106902"
  },
  "emitente": {
    "cnpj": "33041260133393",
    "nome": "Casas Bahia - Venda Nova BH",
    "inscricaoEstadual": "79065181000194",
    "logradouro": "Rua Luiza Vieira",
    "numero": "123",
    "bairro": "Centro",
    "cidade": "Belo Horizonte",
    "cep": "31610110",
    "uf": "MG",
    "complemento": "Loja 1",
    "codMun": "3550308"
  },
  "itens": [
    {
      "descricao": "Geladeira Brastemp",
      "peso": 101.5,
      "altura": 1.71,
      "largura": 0.56,
      "profundidade": 0.61,
      "cubagem": 0.5841
    },
    {
      "descricao": "TV Samsung",
      "peso": 14.50,
      "altura": 0.72,
      "largura": 1.25,
      "profundidade": 0.25,
      "cubagem": 0.2250
    }
  ]
}
```
## Response

Pedido de Entrega cadastrado com sucesso.

200

## Headers

Content-Type:application/json

## Body
```
{
  "codigoRastreio": "1850610"
}
```
## Response

Campos obrigatórios ou inválidos.

400

## Headers

Content-Type:application/json

## Body
```
{
  "errorMsgs": [
    "numeroNf: não pode estar em branco",
    "totalNota: não pode ser nulo",
    "emitente.cnpj: não pode estar em branco",
    "emitente.cep: não pode estar em branco
    "consumidor: deve ser informado somente CPF ou CNPJ",
    "consumidor.nome: não pode estar em branco"
  ]
}
```
## Response

Dados do usuário utilizado inválido, inativo ou 
experirado.

403

## Headers

Content-Type:application/json

## Body

{}

## Response

Solicitações simultâneas de registrar um pedido com as 
mesmas informações.

409

## Headers

Content-Type:application/json

## Body
```
{
  "errorMsgs": [
    "Tentativa de registrar pedido ao mesmo tempo | NF: 154823 | Cliente: Casas Bahia - Venda"
  ]
}
```
