# TMS API ASAP Log

**Ambiente Staging (squad Operações)**

**POST** `https://app.tatooine.asaplog.com.br/webservices/v1/pedido`

**Ambiente PreProd**

**POST** `https://app.preprod.asaplog.com.br/webservices/v1/pedido`

**Ambiente Produção**

**POST** `https://app.asaplog.com.br/webservices/v1/pedido`

**Autenticação**

Tipo: `Basic Auth`

- Username: `<user-name>`

- Password: `<pass-word>`

Content: `application/json`

Body:

```json
{
   "idServico": "MINIHUB_VV",
   "numeroNf":"232399900",
   "serieNf":"001",
   "chaveAcesso":"99980999065189990194550010025153811211328157",
   "identificacaoCliente":"2323999",
   "descricaoProduto": "Descricao do produto na NFe",
   "qtdVolumes":2,
   "pesoTotal":60.8,
   "cubagemTotal":0.0293,
   "totalNota":1080.00,
   "valorICMS":309.20,
   "codigoCarga":"12062017",
   "tipoProduto": "LINHA_BRANCA",
   "tipoEntrega": "NORMAL",
   "tipoDocumento":"PVE",
   "idTipoDocumento":"NFE",
   "origem":"VIA",
   "dataPrevisaoEntrega":"2022-07-02T03:00:00.000Z",
   "agendamento":{
      "dataAgendamento":"2022-07-02T03:00:00.000Z",
      "periodo":"MANHA"
   },
   "consumidor":{
      "cpf":"3681983917",
      "cnpj":"",
      "nome":"DOUGLAS FERREIRA DA ROCHA",
      "razaoSocial":null,
      "inscricaoEstadual":"Isento",
      "telefone":"41996239624",
      "email":"XXXXXXXXXXXX@gmail.com",
      "cep":"82980470",
      "logradouro":"R PROF LEONI I F NASCIMENTO",
      "numero":"95",
      "complemento":"CASA",
      "pontoReferencia":"UNICESUMAR",
      "bairro":"CAJURU",
      "cidade":"CURITIBA",
      "uf":"PR",
      "codMun":"4106902",
      "codigoMicro":"PRP0364",
      "codigoRegiao":"1447"
   },
   "emitente":{
      "cpf":null,
      "cnpj":"33041260/1842-06",
      "nome":"1475 - CD São José dos Pinhais",
      "razaoSocial":null,
      "inscricaoEstadual":"123456789",
      "telefone":"(99) 99999-9999",
      "email":"XXXXXXXXXXXX@gmail.com",
      "cep":"83085058",
      "logradouro":"Rodovia Contorno Leste BR-116",
      "numero":"7000",
      "complemento":"",
      "pontoReferencia":null,
      "bairro":"Quississana",
      "cidade":"São José dos Pinhais",
      "uf":"PR",
      "codMun":"4125506"
   },
   "tomadorServico":{
      "cpf":null,
      "cnpj":"33041260078007",
      "nome":"S.JOSE PINHAIS-PL.QU",
      "razaoSocial":null,
      "inscricaoEstadual":"9062297813",
      "telefone":"11 4588-0000",
      "email":"XXXXXXXXXXXX@gmail.com",
      "cep":"83085058",
      "logradouro":"RUA CONTORNO LESTE BR 116",
      "numero":"7000",
      "complemento":"",
      "pontoReferencia":null,
      "bairro":"PL.QUISSISSANA",
      "cidade":"SAO JOSE DOS PINHAIS",
      "uf":"PR",
      "codMun":"4125506"
   },
   "expedidorServico":{
      "cpf":null,
      "cnpj":"33041260078007",
      "nome":"S.JOSE PINHAIS-PL.QU",
      "razaoSocial":null,
      "inscricaoEstadual":"9062297813",
      "telefone":"11 4588-0000",
      "email":"XXXXXXXXXXXX@gmail.com",
      "cep":"83085058",
      "logradouro":"RUA CONTORNO LESTE BR 116",
      "numero":"7000",
      "complemento":"",
      "pontoReferencia":null,
      "bairro":"PL.QUISSISSANA",
      "cidade":"SAO JOSE DOS PINHAIS",
      "uf":"PR",
      "codMun":"4125506"
   },
   "volumes":[
      {
         "id":0,
         "etiqueta":"VV011194822BR",
         "codigoBarras":null,
         "peso":11.3,
         "cubagem":0.115943,
         "altura":0.71,
         "largura":0.71,
         "profundidade":0.23
      },
      {
         "id":1,
         "etiqueta":"VV011194825BR",
         "codigoBarras":null,
         "peso":11.3,
         "cubagem":0.115943,
         "altura":0.71,
         "largura":0.71,
         "profundidade":0.23
      }
   ],
   "itens":[
      {
         "id":0,
         "etiqueta":"VV011194825BR",
         "codigoBarras":null,
         "descricao":"Fogão Brastemp",
         "peso":60.8,
         "cubagem":1.2,
         "altura":0.87,
         "largura":0.5,
         "profundidade":0.6,
         "codigo":null,
         "tipo":null,
         "qtde":1
      }
   ]
}
```

## Descrição de enums

**idServico** (**pode sofrer alterações futuras**)

- MINIHUB_VV - Entrega Mini Hub
- ENTREGA_CONVENCIONAL - Entrega ENTREGA_CONVENCIONAL
- ENTREGA_PESADA( - Entrega ENTREGA_PESADA
- ENTREGA_B2B - Entrega ENTREGA_B2B
- ENTREGA_P2P - Entrega ENTREGA_P2P
- SELLER_VV - Entrega seller vv
- ENTREGA_LEVE - Entrega Leve

**periodo**

- MANHA
- TARDE
- NOITE

**idTipoDocumento**

- DECLARACAO
- DUTOVIARIO
- CFE_SAT
- NFCE
- NOTA_FISCA

**tipoDocumento**

- PVE
- STD
- OSE
- OSC

**tipoProduto**

- LINHA_BRANCA
- MOVEIS 
- OUTROS

**tipoEntrega**

- NORMAL
- SAME_DAY
- SAME_HOUR

## Resposta

Content: application/json

**Sucesso**

Motivo: tudo certo.

HTTP Status: *200*

```json
{
    "status": "SUCESSO",
    "mensagem": [
        "Solicitação efetuada com sucesso."
    ],
    "codigoInternoPedido": "23068925"
}
```

**Erro de validação**

Motivo: falta de campos obrigatórios.

HTTP Status: *400*

```json
{
    "status": "ERRO",
    "mensagem": [
        "consumidor.logradouro: não pode estar em branco",
        "numeroNf: não pode estar em branco"
    ],
    "codigoInternoPedido": null
}
```

**Erro de autorização**

Motivo: falha na validação de username ou password.

HTTP Status: *403*

```json
{
    "status": "ERRO",
    "mensagem": [
        "Usuário não encontrado ou não autorizado."
    ],
    "codigoInternoPedido": null
}
```

### Últimas atualizações

- Novo campo tipoEntrega diferenciar pedidos Mini Hub de normal, same day e same hour. 
- Padronização das respostas da API, agora o campo mensagem é uma lista e podem vir mais de uma mensagem por resposta.
- Utilização de exception handlers para tratamento de erros.
