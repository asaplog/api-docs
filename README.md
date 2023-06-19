# ASAP Log API

## Introdução

Seja bem-vindo à documentação das APIs disponiblizadas pela ASAP Log.
Os tópicos abaixo descrevem sobre cada uma delas e exemplos de como usá-las.

## Autenticação

### Como autenticar

Nossa autenticação é feita com Basic Auth, utilizando um usuário e senha, passado para o cliente mediante solicitação e aprovação.

A autenticação com Basic Auth consiste em transformar o usuário e senha, no formato usuario:senha em uma hash base64 e enviar como header nas requisições HTTP. A maioria dos clientes HTTP já fazem isso para você, então você provavelmente irá somente informar o usuário e senha para continuar.

**Usuário**: d41d8cd98f00b204

**Senha**: e9800998ecf8427e

**Base64**: d41d8cd98f00b204:e9800998ecf8427e

**Logo, o header enviado é Authorization:** Basic
ZDQxZDhjZDk4ZjAwYjIwNDplOTgwMDk5OGVjZjg0Mjdl
