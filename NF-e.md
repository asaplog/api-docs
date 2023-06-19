# NF-e

A API de atualizar NF-e serve para alterar alguns dados de uma NF-e previamente cadastrada em um pedido. Você deve fazer um PUT em nosso endpoint seguido do código informado no campo identificacaoCliente no cadastro do pedido.

As respostas podem ser validadas pelos status HTTP 200 (OK) ou HTTP 404 (Pedido não encontrado).

Caso o status seja 200 virá OK no corpo da resposta.

## Parâmetros de envio

| Parâmetro   | Obrigatório | Tipo    | Tamanho (máx. caracteres) | Descrição                                                               |
|-------------|-------------|---------|---------------------------|-------------------------------------------------------------------------|
| numeroNf    | Sim         | String  | 20                        | Número da Nota Fiscal                                                   |
| serieNf     | Sim         | String  | 5                         | Série da Nota Fiscal                                                    |
| chaveAcesso | Sim         | String  | 50                        | Chave de Acesso da Nota Fiscal                                          |
| qtdVolumes  | Sim         | Integer | -                         | Quantidade de Volumes da Nota Fiscal                                    |
| box         | Sim         | String  | 5                         | Número do box para coleta no polo                                       |
| cnpj        | Não         | String  | 20                        | Número do CNPJ do emissor da nota. Pode ser enviado com o sem pontuação |

## Atualiza NF-e

PUT https://app.asaplog.com.br/webservices/v1/pedidoEntregas/nfe/[IDENTIFICAÇÃO CLIENTE]

## Request



## Headers

Content-Type:application/json
Authorization:Basic [base64 de autenticação]

## Body
```
{
  "numeroNf": "2515082",
  "serieNf": "1",
  "chaveAcesso": "41180679065181000194550010025150821445150819",
  "qtdVolumes": 1,
  "box": "23",
  "cnpj": "88397961000122"
}
```
## Response

200

## Body

Ok

## Response

404

## Body

Pedido não encontrado.