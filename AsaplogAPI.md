# API ASAP Log

Api com payload compatível da api de pedidos UX.

**Ambiente Staging (squad Operações)**

**POST** `https://app.tatooine.asaplog.com.br/api/v1/pedido`

**Ambiente PreProd**

**POST** `https://app.preprod.asaplog.com.br/api/v1/pedido`

**Ambiente Produção**

**POST** `https://app.asaplog.com.br/api/v1/pedido`

**Autenticação**

Tipo: `Basic Auth`

- Username: `<user-name>`

- Password: `<pass-word>`

Content: `application/json`

## Estrutura do Json das solictações

```json
{
  "idLote": null,
  "cnpjEmbarcadorOrigem":"99.999.999/9999-99",
  "cnpjTransportadorDestinto": null,
  "listaSolicitacoes": [
    {
      "idSolicitacaoInterno": "411683480013164401",
      "idServico": 4,
      "dtPrazoInicio": null,
      "dtPrazoFim": null,
      "tomadorServico": {
        "cpf": null,
        "cnpj": null,
        "inscricaoEstadual": null,
        "nome": "Nome",
        "razaoSocial": null,
        "telefone": null,
        "email": null,
        "Endereco": null
      },
      "remetente": {
        "cnpjRemetente": null,
        "cnpj": "99.999.999/9999-99",
        "inscricaoEstadual": null,
        "nome": "Nome",
        "razaoSocial": "Razão Social",
        "telefone": null,
        "email": null,
        "endereco": {
          "cep": "99999999",
          "logradouro": "Rua Brasil",
          "numero": "394",
          "complemento": "Serra Park  sala 15",
          "pontoReferencia": null,
          "bairro": "Taquara II",
          "nomeCidade": "Serra",
          "siglaEstado": "ES",
          "idCidadeIBGE": null
        }
      },
      "destinatario": {
        "cpf": "00090564081",
        "cnpj": null,
        "inscricaoEstadual": "ISENTO",
        "nome": "Nome",
        "razaoSocial": null,
        "telefone": null,
        "email": null,
        "endereco": { 
          "cep": "99999999",
          "logradouro": "Rua da Produção",
          "numero": "489",
          "complemento": null,
          "pontoReferencia": null,
          "bairro": "Várzea",
          "nomeCidade": "Jundiaí",
          "siglaEstado": "SP",
          "idCidadeIBGE": null
        }
      },
      "expedidor": null,
      "logisticaReversa": null,
      "dadosAgendamento": null,
      "listaOperacoes": [
        {
          "idTipoDocumento": 55,
          "nroNotaFiscal": 3432615,
          "serieNotaFiscal": 1,
          "dtEmissaoNotaFiscal": "2024-02-08T00:00:00",
          "chaveNotaFiscal": "32240208351293000910550010034326151240041162",
          "nroCarga": null,
          "nroPedido": "41168348001",
          "qtdeVolumes": 1.0,
          "qtdeItens": null,
          "pesoTotal": 6.0000,
          "cubagemTotal": 0.055936000000,
          "valorMercadoria": 639.9000,
          "valorICMS": null,
          "listaVolumes": [
            {
              "idVolume": null,
              "nroEtiqueta": "VV014312220BR",
              "codigoBarras": null,
              "pesoVolume": 6.0000,
              "cubagemVolume": 0.055936000000,
              "altura": 0.4600,
              "largura": 0.3800,
              "comprimento": 0.3200
            }
          ],
          "listaItens": [
            {
              "idItem": null,
              "nroEtiqueta": null,
              "codigoItem": null,
              "descricaoItem": "Purificador de Água Refrigerado Branco Bivolt PA335  Latina Bivolt",
              "tipoItem": null,
              "qtde": 1.0
            }
          ]
        }
      ],
      "chaveCTeAnterior": null,
      "linkCTe": null,
      "base64CTe": null
    }
  ]
}
```

## Informações obrigatórias

- cnpjEmbarcadorOrigem

- listaSolicitacoes[ ]
- listaSolicitacoes[ ].idSolicitacaoInterno
- listaSolicitacoes[ ].idServico

- listaSolicitacoes[ ].destinatario
- listaSolicitacoes[ ].destinatario.nome
- listaSolicitacoes[ ].destinatario.endereco
- listaSolicitacoes[ ].destinatario.endereco.cep
- listaSolicitacoes[ ].destinatario.endereco.logradouro

- listaSolicitacoes[ ].listaOperacoes[ ]
- listaSolicitacoes[ ].listaOperacoes[ ].idTipoDocumento
- listaSolicitacoes[ ].listaOperacoes[ ].nroNotaFiscal
- listaSolicitacoes[ ].listaOperacoes[ ].serieNotaFiscal
- listaSolicitacoes[ ].listaOperacoes[ ].qtdeVolumes

- listaSolicitacoes[ ].listaOperacoes[ ].listaVolumes[]

- listaSolicitacoes[ ].listaOperacoes[ ].listaItens[]
- listaSolicitacoes[ ].listaOperacoes[ ].listaItens[].qtde


## Descrição de enums

**idServico** (**informar apenas o código**)

- 4  - Entrega Convencional
- 16 - Entrega Leve
- 21 - Entrega Mar Aberto
- 24 - Entrega Fulfillment

**periodo** (**informar apenas o código**)

Determina o periodo para a realização da solicitação
- 0 - Integral
- 1 - Manhã
- 2 - Tarde
- 3 - Noite

**idTipoDocumento** (**informar apenas o código**)

Define o tipo do documento da entrega
- 00 - Declaracao
- 10 - Dutoviário
- 59 - CF-E SAT
- 65 - NFC-e
- 55 - NF-e

## HTTP Status Codes
- 200 -	Sucesso no processamento das solicitações
(Em "resultados" tera a solicitações que foram cadastradas e em "errosDetalhes" tera os detalhes das solicitações que tiveram algum erro no processamento)
- 400 -	Os dados informados são inválidos ou todas as solicitações enviadas são - inválidas
- 403 - Falha na autenticação da api
- 500 - Erro interno do sistema.

## Resposta

Content: application/json

```json
{ 
   "erro":false,
   "mensagem":"OK",
   "resultados":[ 
      { 
         "idSolicitacaoInterno":"456123456",
         "idSolicitacaoGerada":2119751,
         "listaVolumes": [
             {
                 "idVolume": 45425,
                 "nroEtiqueta": "938694734985",
                 "codigoRastreio": "BR892117779BR",
                 "protocoloEnvio": "12315587",
                 "linkEtiqueta": null
             },
             {
                 "idVolume": 45426,
                 "nroEtiqueta": "938694735586",
                 "codigoRastreio": "BR15524",
                 "protocoloEnvio": "12315587",
                 "linkEtiqueta": null
             }
         ]
      }
   ],
   "errosDetalhes":[ 
      { 
        "code": 409,
        "descricao": "Solicitação já esta cadastrada no sistema",
        "info": {
            "idSolicitacaoInterno": "411683480013164401"
        }
      }
   ]
}
```

## Código do status do processamento

Valores possíveis para 'errosDetalhes.code':
- 400 - Solicitação inválida, conferir os erros
- 409 - Solicitação já esta cadastrada no sistema
