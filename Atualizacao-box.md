## Atualização Box TMS

<details>     
<summary> Request </summary> 

### URL
> **PATCH** https://app.asaplog.com.br/webservices/v2/atualizar-box/{cod_roteiro}

### Path Parâmetros
> cod_roteiro | Código do roteiro que o pedido está incluído

### Headers Parâmetros 

> **Authorization** : Bearer Token \
> **Content-type**: application/json

### Body

> box | Integer
</details>     
<br>

<br>


<details>     
<summary> Responses </summary> 

### Status
 > **200** | Encontrou roteiro e irá processar \
 > **404** | Roteiro não encontrado



### RESPONSE BODY SCHEMA



> | Campo | TIPO | DESCRIÇÃO |
> |:---------------|:-------:|:------------------------------------------------:|
 | status | String | Status Code HTTP |
 | message | String | Mensagem de retorno |
 | data | Object | Objeto de retorno   (Representado abaixo) |


     
#### data:

 >| Campo      |     TIPO      |                    DESCRIÇÃO                     |
> |:---------------|:-------------:|:------------------------------------------------:|
 | box |    Integer    | Box enviado no request |
 | pedidosAtualizados        | List\<String> |        Pedido que estarão no box enviado       |
 | quantidadePedidosAtualizados           |    Integer    |         Quantidade de pedidos que foram alterados            |




</details>     
<br>
<br>

<details>     
<summary> Exemplos de retorno</summary> 

#### Status 200
```json
{
    "status" : "200",
    "message" :"Roteiro encontrado e atualizado"
    "data" : {
        "box" : 123,
        "pedidosAtualizados" : [
            "2039921","2039922","2039923"
        ],
        "quantidadePedidosAtualizados" : 3
    }
}
```


#### Status 404
```json
{
    "status" : "404",
    "message" :"Roteiro não encontrado"
    "data" : {
        "box" : 123,
        "pedidosAtualizados" : [],
        "quantidadePedidosAtualizados" : 0
    }
}
```

</details>     
