# Rastreio

A API de Rastreio de Pedido da ASAP Log serve para que você possa rastrear um pedido de entrega. Você deve fazer um POST para nosso endpoint, com o Código de rastreio no corpo da requisição.

As respostas podem ser validadas pelos status HTTP 200 (Rastreio recebido com sucesso) ou HTTP 404 (Pedido não encontrado).

Caso o status seja 200, você pode ler todos os dados do rastreio para armazenar e exibir em seu sistema.



## Dados Recebidos do Rastreio:

| Parâmetro              | Tipo                    | Descrição                                 |
|------------------------|-------------------------|:------------------------------------------|
| numeroNf               | String                  | Número da Nota Fiscal                     |
| serieNf                | String                  | Série da Nota Fiscal                      |
| chaveAcesso            | String                  | Chave de Acesso da Nota Fiscal            |
| documentoDestinatario  | String                  | Documento do destinatário                 |
| documentoRemetente     | String                  | Dcumento do Rementente                    |
| identificacaoCliente   | String                  | Retorna o ID do cliente                   |
| codigoDeRastreio       | String                  | Código do rastreio do pedido              |
| statusUltimaOcorrencia | String                  | Status da ultima ocorrencia               |
| dataEnviada            | String                  | Data enviada                              |
| dataCriacao            | String                  | Data de criação do pedido                 |
| previsaoEntrega        | String                  | Previsão de entrega do pedido             |
| prazoMaximo            | String                  | Prazo máximo de entrega                   |
| tentativasEntrega      | Array<TentativaEntrega> | Objeto com as tentivas de entregas        |
| statusPedido           | String                  | Status do Pedido                          |
| mensagemOcorrencia     | String                  | Mensagem da ultima ocorrencia             |
| nomeDestinatario       | String                  | Nome do Destinatário                      |
| nomeLoja               | String                  | Nome da Loja                              |
| codigoRastreioCorreios | String                  | Código de rastreio correios               |
| fotoComprovante        | String                  | Foto do comprovante                       |
| etapas                 | Array<Etapa>            | Objeto com as etapas de entrega do pedido |

## Tentativas de entrega
Dentro do Array de tentativas de entrega contém um objeto com os seguintes parametros:

| Parâmetro        | Tipo   | Descrição                                     |
|------------------|--------|:----------------------------------------------|
| dataRealizada    | String | Data da tentativa de entrega                  |
| statusOcorrencia | String | Status da ocorrência da entrega               |
| observacao       | String | Anotação escrita sobre a tentativa de entrega |

## Etapas:
Dentro do Array de etapas contém um objeto com os seguintes parametros :

| Parâmetro     | Tipo   | Descrição                                 |
|---------------|--------|:------------------------------------------|
| nomeDaEtapa   | String | Nome da etapa que será realizada          |
| dataPrevista  | String | Data prevista que irá acontecer a etapa   |
| dataRealizada | String | Data efetiva que ocorreu a etapa descrita |
| status        | String | Status da etapa                           |
| statusMessage | String | Anotação sobre o status da etapa          |


Tipos de Etapas:

- COLETA_CLIENTE
- ENTREGA_HUB_TRANSPORTADORA_CIDADE_ORIGEM
- RECEBIMENTO_HUB_ORIGEM
- COLETA_HUB_TRANSFERENCIA_PONTE
- ENTREGA_HUB_TRANSFERENCIA_PONTE
- SAIDA_HUB_DESTINO
- COLETA_HUB_TRANSPORTADORA_CIDADE_DESTINO
- ENTREGA_CONSUMIDOR

Tipos de Status de Pedido:
- REGISTRADA
- BLOQUEADA
- PLANEJADA
- NAO_CONFORMIDADE
- EM_FIRST_MILE
- EM_TRANSFERENCIA
- EM_LAST_MILE
- ENTREGUE
- CANCELADA
- FINALIZADO
- EXTRAVIADO
- FURTADO
- AVARIADO
- DEVOLVIDO


# Rastrear um pedido

## CURL

curl --request POST \
--url http://localhost:8085/webservices/v1/rastrear \
--header 'Content-Type: application/json' \
--cookie SESSION=NjMzNTU1MTAtMmIwMy00NDM4LWE2MzUtYmNiMDM1MDAyNDM2 \
--data '{
"codigoDeRastreio": "FF000000939BR"
}'

## Request

URL: localhost:8085/webservices/v1/rastrear

Método: POST

JSON: {"codigoDeRastreio": "FF000000939BR"}


## Response

Rastreio recebido com sucesso.

200

## Headers

Content-Type:application/json

## Autorization

Basic Auth.

## Body
```
{
	"numeroNfe": "25032",
	"serieNfe": "1",
	"chaveDeAcessoNfe": "42220775491688000159550010000250321415347970",
	"documentoDestinatario": "467*****",
	"documentoRemetente": "274*****",
	"identificacaoCliente": null,
	"codigoDeRastreio": "OF706296395BR",
	"statusUltimaOcorrencia": "",
	"dataEnviada": "",
	"dataCriacao": "05/07/2023",
	"previsaoEntrega": "10/07/2023",
	"prazoMaximo": "07/07/2023",
	"tentativasEntrega": [
		{
			"dataRealizada": "",
			"statusOcorrencia": "",
			"observacao": ""
		}
	],
	"statusPedido": "EM_FIRST_MILE",
	"mensagemOcorrencia": "",
	"nomeDestinatario": "Mar*****",
	"nomeLoja": "",
	"codigoRastreioCorreios": "",
	"fotoComprovante": "",
	"etapas": [
		{
			"nomeDaEtapa": "COLETA_CLIENTE",
			"dataPlanejada": "06/07/2023",
			"dataRealizada": "05/07/2023",
			"status": "true",
			"statusMessage": ""
		},
		{
			"nomeDaEtapa": "ENTREGA_HUB_TRANSPORTADORA_CIDADE_ORIGEM",
			"dataPlanejada": "06/07/2023",
			"dataRealizada": "",
			"status": "false",
			"statusMessage": "Vá até o balcão e informe o código de postagem: OF706296395BR"
		},
		{
			"nomeDaEtapa": "COLETA_HUB_TRANSPORTADORA_CIDADE_DESTINO",
			"dataPlanejada": "10/07/2023",
			"dataRealizada": "",
			"status": "false",
			"statusMessage": ""
		},
		{
			"nomeDaEtapa": "ENTREGA_CONSUMIDOR",
			"dataPlanejada": "10/07/2023",
			"dataRealizada": "",
			"status": "false",
			"statusMessage": ""
		}
	],
	"sucesso": null,
	"erros": null
}
```