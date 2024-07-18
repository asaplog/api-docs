# Parceiros

Este serviço visa disponibilizar ao integrador a possibilidade de consultar ocorrências de entregas/coletas.
Para que a API realize a consulta corretamente, os dados devem ser enviados conforme padrões estabelecidos abaixo, utilizando o endpoint acima.
Em todas as requisições válidas, o sistema irá retornar uma estrutura de mensagem de retorno em formato JSON, conforme listado nas definições abaixo.


**Ambiente Homologação**

**POST** `https://api.tatooine.asaplog.com.br/api/v1/asaplog/consulta/ocorrencia`

**Ambiente Produção**

**POST** `https://api.asaplog.com.br/api/v1/asaplog/consulta/ocorrencia`

**Autenticação**

Tipo: `Bearer Authentication`

Content: `application/json`


## Body
```
{
    "cnpjEmbarcador" : string,
    "cnpjRemetente" : string,
    "cpfRemetente" : string,
    "dtInicioBusca" : "yyyy-MM-dd",
    "dtFimBusca" : string,
    "listaNotasFiscais" : [string],
    "listaPedidos" : [string]
}
```

ou
```
{
    "chaveNFe" : string
}
```

## Response

```
{
    "flagErro": boolean,
    "flagInfo": boolean,
    "listaMensagens": [string],
    "listaResultados": [
        {
            "idOcorrencia": string,
            "idNotaFiscal": string,
            "cnpj": string,
            "cnpjRemetente": string,
            "cpfRemetente": string,
            "servico": string,
            "dtOcorrencia": string,
            "codigoOcorrencia": string,
            "idStatusSolicitacao": string,
            "descricaoOcorrencia": null,
            "nroNotaFiscal": null,
            "serieNotaFiscal": null,
            "nroPedido": null,
            "latitude": null,
            "longitude": null,
            "unidadeOcorrencia": null,
            "nomeCidade": null,
            "uf": null,
            "prazoEntrega": null,
            "solicitacaoPessoa": null,
            "listaEvidencias": []
        }
    ],
    "info": null
}
```

200