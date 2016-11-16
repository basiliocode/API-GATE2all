---
title: GATE2all Guia de Integração API V2

language_tabs:
  - json: JSON
  - shell: cURL

toc_footers:
  - <a href='http://cert.gate2all.com.br'>Painel de Controle do GATE2all</a>
  - <a href='http://cert.gate2all.com.br'>Painel de Controle do SandBox</a>
  - <a href='https://github.com/orgs/NTKSolutions'>GitHub</a>

includes:
  - status
  - status_http
  - errors_api

search: true
---

# Introdução

Olá! Bem vindo a API do **GATE2all.**

Aqui você irá encontrar informações de como integrar seu sistema ao gateway de pagamentos **GATE2all.**

O **GATE2all** é uma plataforma de pagamentos que conecta lojas virtuais, app's mobile, ERP's ou sistema de cobraças com as principais instituições de pagamentos do Brasil.

Ao integrar-se ao gateway de pagamentos **GATE2all** seu negócio poderá receber transações através das principais formas de pagamentos como cartão de crédito e débito, boleto bancário e transferência entre contas.

A vantagem de se utilizar nossa plataforma é que você não precisará se integrar a cada adquirente ou bancos, através do **GATE2all** você se beneficia delas de forma unificada e sem complicações.

O **GATE2all** segue as rigorosas normas do **PCI DSS** que são regras que visam proteger os dados do portador do cartão. Conheça mais no site [https://pt.pcisecuritystandards.org](https://pt.pcisecuritystandards.org)

## Sobre este documento

Este documento constitui a especificação técnica para integração de sistemas que desejam operar com o gateway de pagamento **GATE2all**.

Aqui serão listadas todas as funcionalidades da plataforma **GATE2all** especificando os endereços de requisição, parametros da requisição, formato e exemplos.

Disponibilizamos as coleções no client REST Postman. 

Para instalar o client Postman, basta acessar <a href='https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop' target='_blank'>Install Postman</a> 

Para importar uma coleção contendo os endpoints e mensagens de exemplos, basta clicar no botão abaixo.

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/a6fc46e6eb8e53800b3e)


<aside class="warning">
As informações contidas neste documento estão sujeitas a alteração sem prévio aviso.
</aside>

### PÚBLICO

Este documento é destinado aos desenvolvedores e analistas de sistemas de e-commerce que desejem integrar sua loja virtual com o gateway **GATE2all** para a realização de transações eletrônicas.

### CONTATOS

Suporte ao desenvolvedor é prestado através do e-mail <a href="mailto:suporte@2all.com.br">suporte@2all.com.br.</a>
<aside class="warning">
Nossa equipe de suporte a desenvolvedores não provê suporte para linguagens de programação e tecnologias utilizadas pelo desenvolvedor.
</aside>


## Glossário

**Autenticação**: Processo para assegurar que o comprador é o portador legítimo.

**Autorização**: Processo para verificar se uma compra pode ou não ser realizada num cartão. Verifica-se limite, se o cartão está ativo, se o portador está adimplente, etc.

**Cancelamento**: Processo para cancelar uma compra no cartão.

**Captura**: Processo para confirmar uma autorização. É após, a captura, que o portador recebe um débito na fatura de seu cartão.

**Chave de acesso**: Chave de autenticação da loja usada na chamada aos Web Services da Cielo.

**Comprador**: É aquele que efetua compra na loja virtual.

**Emissor**: Empresa responsável pela emissão do cartão utilizado pelo cliente para a realização de transações eletrônicas no Estabelecimento. Administradoras associadas a bancos são os principais emissores de cartões, assim como administradoras de cartões de benefício (refeição, alimentação, combustível, premiação, etc.).

**Estabelecimento comercial** ou **EC**: Empresa que responde pela loja virtual.

**Número de afiliação**: É um identificador que o lojista recebe após ter-se afiliado a Cielo.

**Portador**: É o mesmo que comprador. É aquele que tem o porte de um cartão.

**TID**: Identificador único da transação.

**Transação**: É o pedido de compra do portador na rede adquirente.

**Gateway de pagamento**: é uma aplicação que realiza transações financeiras através de web sites. Sua função basicamente é comunicar com as redes adquirentes e efetuar com segurança a captura dos dados do comprador.

**Rede Adquirente**: Empresa responsável por prover o serviço de captura de transações eletrônicas (seja de cartão de crédito/débito ou outro meio de pagamento). Cielo, Rede, GetNet e BANRISUL são exemplos de Redes adquirentes brasileiras.

**Bandeira**: Empresa definindo um padrão e provendo serviços de intercâmbio e troca de informações entre a Rede Adquirente e o Emissor. Visa, MasterCard e American Express são exemplos típicos de bandeiras.

**Tokenização**: Método para gravar cartão do comprador no ambiente Cielo para realização de transações sem o número do cartão.

**Soft Descriptor**: Função para incluir um texto que será exibido na fatura do cartão de crédito do comprador.

**Pré-autorização**: Tipo de transação que consulta e reserva um valor estimado para o estabelecimento como garantia até a conclusão da operação, aplica-se normalmente há locadoras de veículos e hotéis.

**Transferência online**: A Transferência entre contas bancárias é uma opção de pagamento on-line. Esse meio de pagamento utiliza-se do Internet Banking do lojista e do consumidor final. No momento do pagamento, basta informar os dados da conta, a senha e a frase secreta, e o banco efetuará a transferência do valor da compra diretamente para a loja, de forma rápida e segura.

## Pré-requisitos

Para que o lojista possa utilizar as funcionalidades do **GATE2all**, este deve possuir afiliação para e-commerce junto às redes adquirentes ou bancos aos quais deseja encaminhar transações ou cobranças.

## Adquirentes integradas

**Cielo** API 1.5 e 3.0

**REDE** (Komerci)

**GetNet**


### Bandeiras suportadas por adquirente


Adquirente | Cielo | REDE | GetNet |
-------------- | -------------- | -------------- | --------------
Visa |  <input type="checkbox" checked disabled readonly> |  <input type="checkbox" checked disabled readonly> | <input type="checkbox" checked disabled readonly>
Mastercard |  <input type="checkbox" checked disabled readonly> |  <input type="checkbox" checked disabled readonly> |  <input type="checkbox" checked disabled readonly> 
Diners Club |  <input type="checkbox" checked disabled readonly> |  <input type="checkbox" checked disabled readonly> | <input type="checkbox" disabled readonly> 
American Express |  <input type="checkbox" checked disabled readonly> | <input type="checkbox" disabled readonly> | <input type="checkbox" disabled readonly> 
Elo |  <input type="checkbox" checked disabled readonly> | <input type="checkbox" disabled readonly> | <input type="checkbox" disabled readonly> 
Hipercard | <input type="checkbox" disabled readonly> |  <input type="checkbox" checked disabled readonly> | <input type="checkbox" disabled readonly> 
Hiper | <input type="checkbox" disabled readonly> |  <input type="checkbox" checked disabled readonly> | <input type="checkbox" disabled readonly>
Aura |  <input type="checkbox" checked disabled readonly> | <input type="checkbox" disabled readonly> | <input type="checkbox" disabled readonly> 
Discover |  <input type="checkbox" checked disabled readonly> | <input type="checkbox" disabled readonly> | <input type="checkbox" disabled readonly> 
JCB |  <input type="checkbox" checked disabled readonly> | <input type="checkbox" disabled readonly> | <input type="checkbox" disabled readonly> 
Visa Electron |  <input type="checkbox" checked disabled readonly> | <input type="checkbox" disabled readonly> | <input type="checkbox" disabled readonly> 
Mastercard Maestro |  <input type="checkbox" checked disabled readonly> | <input type="checkbox" disabled readonly> | <input type="checkbox" disabled readonly> 

<aside class="warning">
As transações de cartão de débito (Visa Electron e Mastercard Maestro) só são processadas se houver autenticação pelo mecanismo Verified by Visa ou Mastercard Secure Code.

Não são todos os bancos emissores destas bandeiras que suportam transações autenticadas no e-commerce.

</aside>

## Bancos integrados

<img src="images/logo-bradesco.jpg" />

* Emissão de boleto
* Transferência entre contas

<img src="images/itau-logo.jpg" />

* Emissão de boleto
* Transferência entre contas

## Tipos de Transações

### Crédito

As opções de pagamento com cartão de crédito são: 

* À vista. 
* Parcelado emissor. 
* Parcelado loja.

<aside class="warning">
O valor do resultante da divisão do valor do pedido pelo número de parcelas não deve ser inferior a R$5,00. Caso contrário a transação será negada.
</aside>
 
### Débito

Bandeiras Visa Electron e Maestro através da rede adquirente Cielo, para esta modalidade é necessário a autenticação do portador através dos mecanismos “Verify By Visa” ou “Mastercard Secure Code”.

O cartão do portador deve estar habilitado para transações autenticadas.

### Transferência on-line entre contas

Transferência online entre contas bancárias. Para utilizar este serviço o cliente deverá ter contratado junto ao banco o serviço de comercio eletrônico Bradesco ou Itaú Shopline.

### Boletos

Emissão de boleto bancário com os bancos, Bradesco e Itaú, com conciliação automática. A compensação do boleto poderá ser verificada através do relatório de transações.

Para utilizar este serviço o cliente deverá ter contratado junto ao banco o serviço de comercio eletrônico.

## Tipos de Integração

O gateway de pagamento **GATE2all** permite dois tipos de integração:
 
1. **Loja**, que redireciona o comprador para um ambiente seguro do **GATE2all** onde os dados do cartão serão capturados. 
2. **Integrado**, onde o lojista poderá capturar os dados do cartão em seu próprio sistema.


## Ambientes

Para utilizar nosso ambiente de testes envie um e-mail informando os dados abaixo para <a href="mailto:suporte@2all.com.br">suporte@2all.com.br</a> onde realizaremos o cadastro do desenvolvedor ou empresa responsável pelo desenvolvimento. 

* `RAZAO SOLCIAL`
* `NOME FANTASIA`
* `CNPJ`
* `Nome do desenvolvedor`
* `Telefone`
* `E-mail`

### Ambiente Produção

**Requisição de transação**: https://api.gate.2all.com.br/

### Ambiente de testes (Sandbox)

**Requisição de transação**: https://api.cert.gate.2all.com.br/

# Autenticação

As requisições são autenticadas, pelas credenciais obtidas, passados pelo headers. **Exemplo:**

<img src='images/authenticationApi.png' />

# GATE2all Loja

No **GATE2all** Loja é possível realizar vendas sem a necessidade de desenvolver-se uma página segura de pagamentos, por meio do recurso chamado **Intenção de Venda**. 

Através deste tipo de integração o comprador digita os dados do cartão no ambiente seguro do gateway de pagamentos **GATE2all**, isentando a loja, da manipulação dos dados sensíveis do cartão do comprador.

## Intenção de Venda

Para realizar uma intenção de venda é necessário enviar um POST para o seguinte recurso: 

### Requisição

<aside class="request"><span class="method post">POST</span> <span class="endpoint">/v1/intention/sale/</span></aside>


```json
{
    "orderId": "19893211234",
    "amount": "100",
    "description": "Mouse sem fio",
    "postBackUrl": "http://url-notificacao",
    "dhExpiration": "2017-08-25T18:10:53",
    "customer": {
        "name": "Comprador Teste",
        "document": "12345678909",
        "email": "compradorteste@gmail.com",
        "address": {
            "address": "Rua Fidencio Ramos 100",
            "district": "Vila Olimpia",
            "zipcode": "09878-675",
            "city": "Sao Paulo",
            "state": "SP"
        }
    },
    "payment": {
        "card": {
            "type": 0,
            "capture": false,
            "installments": "2",
            "fixedInstallments": false,
            "operationType": "4",
            "authenticate": "3",
            "softDescriptor": "Gate2@all",
            "saveCard": true
        },
        "eletronicTransfer": {
            "provider": "Bradesco"
        },
        "bankSlip": {
            "expirationDate": "2016-06-30",
            "instructions": "Aceitar somente até a data de vencimento, após essa data juros de 1% dia",
            "guarantor": "Comprador Teste",
            "provider": "Bradesco"
        }
    }
}
```

```shell
curl --request POST
  --url /v1/intention/sale
  --header 'authorization: Basic bnRrOjEyMzQ='
  --header 'content-type: application/json'
  --data-binary
  {
      "orderId": "19893211234",
      "amount": "100",
      "description": "Mouse sem fio",
      "postBackUrl": "http://url-notificacao",
      "dhExpiration": "2017-08-25T18:10:53",
      "customer": {
          "name": "Comprador Teste",
          "document": "12345678909",
          "email": "compradorteste@gmail.com",
          "address": {
              "address": "Rua Fidencio Ramos 100",
              "district": "Vila Olimpia",
              "zipcode": "09878-675",
              "city": "Sao Paulo",
              "state": "SP"
          }
      },
      "payment": {
          "card": {
              "type": 0,
              "capture": false,
              "installments": "1",
              "fixedInstallments": false,
              "operationType": "4",
              "authenticate": "3",
              "softDescriptor": "Gate2@all",
              "saveCard": true
          },
          "eletronicTransfer": {
              "provider": "Bradesco"
          },
          "bankSlip": {
              "expirationDate": "2016-06-30",
              "instructions": "Aceitar somente até a data de vencimento, após essa data juros de 1% dia",
              "guarantor": "Comprador Teste",
              "provider": "Bradesco"
          }
      }
  }
```

|Propriedade|Tipo|Tamanho|Obrigatório|Descrição|
|-----------|----|-------|-----------|---------|
|`orderId`|Texto|100|Sim|Numero de identificação da loja.|
|`amount`|Número|16|Sim|Valor da transação.|
|`description`|Texto|300|Não|Descrição da venda.|
|`postBackUrl`|Texto|—|Não|URL a qual o gate2all notificará eventuais status da trancação a loja.|
|`dhExpiration`|Texto|20|Não|Data da expiração da intenção. Formato **2016-10-16T18:10:53** |
|`customer.name`|Texto|100|Sim|Nome do portador do cartão.|
|`customer.document`|Texto|18|Sim|Número do CPF/CNPJ do portador do cartão.|
|`customer.email`|Texto|100|Sim|Email do portador do cartão.|
|`address.address`|Texto|60|Sim|Endereço do comprador.|
|`address.district`|Texto|80|Sim|Bairro do comprador.|
|`address.zipcode`|Texto|10|Sim|CEP do comprador.|
|`address.city`|Texto|30|Sim|Cidade do comprador.|
|`address.state`|Texto|2|Sim|Sigla do estado do comprador.|
|`card.type`|Inteiro|—|Não|0 Default, configura as opcões disponíveis. 1 Configura cartão de crédito. 2 Configura cartão de débito.|
|`card.capture`|Booleano|—|Sim|Identifica que a autorização deve ser efetuada com captura automática.|
|`card.installments`|Número|20|Sim|Número de parcelas.|
|`card.fixedInstallments`|Booleano|—|Não|Configura parcela fixa.|
|`card.operationType`|Número|20|Sim|Operações disponíveis: 1. Cartão de Crédito 2. Cartão de Débito 3. Parcelado Loja 4. Parcelado Administrador.|
|`card.authenticate`|Texto|20|Sim|(1. para transaação autenticada OBS: rever...)|
|`card.softDescriptor`|Texto|22|Não|Texto a ser exibido na fatura do portador do cartão.|
|`card.saveCard`|Booleano|—|Sim|Configura salvar o cartão (tokenização). |
|`eletronicTransfer.provider`|Texto|20|Sim|Nome da instituição responsável pela transferência.|
|`boleto.expirationDate`|Texto|20|Sim|Data de vencimento do boleto. formato **YYYY/MM/DD**|
|`boleto.instructions`|Texto|300|Sim|Instruções do boleto.|
|`boleto.guarantor`|Texto|45|Sim|Nome do avalista.|
|`boleto.provider`|Texto|20|Sim|Nome da instituição responsável pela emissão.|

### RESPOSTA

```json
{
  "transactionId": "b9bb32a8-401e-41a0-a9ee-af9e8ab0de92",
  "url": "https://gate.2all.com.br/v1/url-payment/b9bb32a8-401e-41a0-a9ee-af9e8ab0de92"
}
```


```shell
  {
    "transactionId": "b9bb32a8-401e-41a0-a9ee-af9e8ab0de92",
    "url": "https://gate.2all.com.br/v1/url-payment/b9bb32a8-401e-41a0-a9ee-af9e8ab0de92"
  }
```


|Propriedade|Tipo|Tamanho|Descrição|
|-----------|----|-------|---------|
|`transactionId`|Texto|36|Identificador da transação retornado pelo gateway.|
|`url`|Texto|150|URL da intenção.|


## Submissão do token

URL para pagamento: [https://gate.2all.com.br/gateway/intencao/pagamento?token={{token}}] (https://gate.2all.com.br/gateway/intencao/pagamento?token={{token}})

**Obs.:** {{token}}: Código do token recebido do retorno positivo da aprovação da intenção de venda.

Após o usuario acessar a URL gerada, aparecerá a seguinte tela de pagamento:

<img src="images/intencao01.png" />

Caso a forma de pagamento escolhida pelo usuário for cartão de crédito, aparecerá a seguinte tela:

<img src="images/intencao02.png" />

Caso a forma de pagamento escolhida pelo usuário for boleto, aparecerá a seguinte tela:

<img src="images/intencao03.png" />

Caso a forma de pagamento escolhida pelo usuário for transferência, aparecerá a seguinte tela:

<img src="images/intencao04.png" />

Em caso de erro ou token incorreto aparecerá a seguinte tela:

<img src="images/intencao05.png" />


# GATE2all Integrado 

`(CHECKOUT TRANSPARENTE)`

Neste modelo todo o relacionamento com o usuário é realizado pela loja virtual, inclusive eventual
captura de dados de cartões de crédito. Portanto sua loja virtual deverá ser homologada PCI, para
maiores informações consulte o site https://www.pcisecuritystandards.org

A loja virtual deve fazer a captura de todos os dados necessários e submetê-los ao **GATE2all**.

## Autorização

Para criar uma autorização é necessário enviar um POST para o seguinte recurso:

### REQUISIÇÃO

<aside class="request"><span class="method post">POST</span> <span class="endpoint">/v1/transactions/authorization/</span></aside>

```json
{
   "orderId": "19893211234",
   "amount": "100",
   "softDescriptor": "Pagamento Gate2all",
   "description": "Mouse sem fio",
   "capture": false,
   "installments": 01,
   "operationType": 1,
   "authenticate": 3,
   "customer": {
      "name": "Comprador Teste",
      "document": "12345678909"
   },
   "payment": {
       "card": {
          "number": "4539708473330561",
          "expirationMonth": "04",
          "expirationYear": "2017",
          "cvv": "234",
          "brand": "VISA",
          "holderName": "LUIS A R ROMERO",
          "saveCard": false
        }
   }
}
```

```shell
curl --request POST
  --url /v1/transactions/authorization
  --header 'authorization: Basic bnRrOjEyMzQ='
  --header 'content-type: application/json'
  --data-binary
  {
     "orderId": "19893211234",
     "amount": "100",
     "softDescriptor": "Pagamento Gate2all",
     "description": "Mouse sem fio",
     "capture": false,
     "installments": 01,
     "operationType": 1,
     "authenticate": 3,
     "customer": {
        "name": "Comprador Teste",
        "document": "12345678909",
        "birthDate": "16/08/1986"
     },
     "payment": {
         "card": {
            "number": "4539708473330561",
            "expirationMonth": "04",
            "expirationYear": "2017",
            "cvv": "234",
            "brand": "VISA",
            "holderName": "LUIS A R ROMERO",
            "saveCard": false
        }
     }
  }
--verbose
```

|Propriedade|Tipo|Tamanho|Obrigatório|Descrição|
|-----------|----|-------|-----------|---------|
|`orderId`|Texto|100|Sim|Numero de identificação da loja.|
|`amount`|Número|16|Sim|Valor da transação.|
|`softDescriptor`|Texto|22|Não|Texto a ser exibido na fatura do portador do cartão.|
|`description`|Texto|300|Não|Descrição da venda.|
|`postBackUrl`|Texto|—|Não|URL a qual o gate2all notificará eventuais status da trancação a loja.|
|`capture`|Booleano|—|Sim|Identifica que a autorização deve ser efetuada com captura automática.|
|`installments`|Número|2|Sim|Número de parcelas.|
|`operationType`|Número|1|Sim|Operações disponíveis: <BR /> 1. Cartão de Crédito<BR /> 2. Cartão de Débito <BR /> 3. Parcelado Loja <BR /> 4. Parcelado Administrador|
|`authenticate`|Número|1|Não|Opções disponíveis: <BR /> 1. Autorizar só transações autenticadas <BR /> 2. Autorizar transações autenticadas ou não autenticadas <BR /> 3. Autorizar sem autenticação <BR /> 4. Parcelado Administrador|
|`customer.name`|Texto|100|Sim|Nome do portador do cartão.|
|`customer.document`|Texto|18|Não|Número do CPF/CNPJ do portador do cartão.|
|`card.number`|Texto|19|Sim|Número do cartão.|
|`card.expirationMonth`|Número|2|Sim|Mês da validade do cartão.|
|`card.expirationYear`|Número|2|Sim|Ano da validade do cartão.|
|`card.cvv`|Número|4|Não|Código de segurança do cartão.|
|`card.holderName`|Texto|20|Não|Nome do portador do cartão.|
|`card.brand`|Texto|20|Sim|Bandeira do cartão.|
|`card.saveCard`|Booleano|—|Sim|Configura salvar o cartão (tokenização). |

### RESPOSTA

> Transação autorizada e não capturada

```json
{
  "transactionId": "92d50ba4-5d93-4ee5-90e8-9884b250310a",
  "orderId": "1463697571584",
  "description": "TV LG 42",
  "softDescriptor": "EC02",
  "operationType": 1,
  "integrationType": 1,
  "amount": "100",
  "installments": 1,
  "capture": false,
  "authenticate": 3,
  "status": 5,
  "dtTransaction": "2016-10-19T12:04:20",
  "payment": {
    "authenticationECI": 7,
    "codAuthorization": "123456",
    "providerReference": "1006993069000834928A",
    "card": {
      "number": "453970******0561",
      "expirationMonth": "04",
      "expirationYear": "2017",
      "cvv": "***",
      "brand": "VISA",
      "holderName": "LUIS A R ROMERO",
      "saveCard": false
    }
  },
  "customer": {
    "name": "LUIS A R ROMERO",
    "document": "12345678909"
  }
}
```


```shell
 {
   "transactionId": "92d50ba4-5d93-4ee5-90e8-9884b250310a",
   "orderId": "1463697571584",
   "description": "TV LG 42",
   "softDescriptor": "EC02",
   "operationType": 1,
   "integrationType": 1,
   "amount": "100",
   "installments": 1,
   "capture": false,
   "authenticate": 3,
   "status": 5,
   "dtTransaction": "2016-10-19T12:04:20",
   "payment": {
     "authenticationECI": 7,
     "codAuthorization": "123456",
     "providerReference": "1006993069000834928A",
     "card": {
       "number": "453970******0561",
       "expirationMonth": "04",
       "expirationYear": "2017",
       "cvv": "***",
       "brand": "VISA",
       "holderName": "LUIS A R ROMERO",
       "saveCard": false
     }
   },
   "customer": {
     "name": "LUIS A R ROMERO",
     "document": "12345678909"
   }
 }
```


> Falha

```json
{
  "error": {
    "message": "O campo amount e obrigatorio."
  }
}
```

```shell
  {
    "error": {
      "message": "O campo amount e obrigatorio."
    }
  }
```

|Propriedade|Tipo|Tamanho|Descrição|
|-----------|----|-------|-----------|---------|
|`transactionId`|Texto|150|Identificador da transação retornado pelo gateway.|
|`message`|Texto|100|Mensagem de retorno da transação.|
|`orderId`|Texto|100|Número de identificação da loja.|
|`amount`|Número|16|alor da transação.|
|`tid`|Texto|100|Identificador da transação retornado pela rede adquirente.|
|`authorizationCode`|Texto|20|Código da autorização retornado pela rede adquirente.|
|`status`|Número|2|Status da transação retornado pelo gateway.|

## Boleto

O boleto bancário ou bloqueto é um instrumento de pagamento de produtos ou serviços. É amplamente utilizado por empresas no Brasil.

Entidades envolvidas: “Banco” que são as instituições financeiras responsáveis pela emissão, recebimento e pagamento do boleto, “Cedente” é quem solicita a emissão do documento de cobrança e o que receberá o valor do pagamento e o “Sacado” que é consumidor do produto ou serviço, ou seja, quem paga o boleto.

Como é o processo de pagamento com boleto bancário:

1. Cedente encaminha para o Sacado o Boleto
2. Sacado efetua o pagamento até a data de vencimento estipulada.
3. Banco recebe o valor e repassa para conta do Cedente.
4. Banco aplica a taxa acordada entre as partes.

### Requisição

<aside class="request"><span class="method post">POST</span> <span class="endpoint">/v1/transactions/bankslip/</span></aside>

```json
{
   "orderId": "19893211234",
   "amount": "100",
   "description": "Produto ou serviço",
   "customer": {
      "name": "Comprador",
      "document": "12345678909",
      "email" : "comprador@email.com",
      "address" : {
          "address" : "Rua Fidencio Ramos 100",
          "district" : "Vila Olimpia",
          "zipcode" : "09878-675",
          "city" : "Sao Paulo",
          "state" : "SP"
      }
   },
   "payment": {
       "bankSlip" : {
            "expirationDate" :"1970-01-01",
            "instructions" : "Aceitar somente até a data de vencimento, após essa data juros de 1% dia",
            "guarantor" : "Comprador",
            "provider":"Itau"
       }
    }
}
```

```shell
```


|Propriedade|Tipo|Tamanho|Obrigatório|Descrição|
|-----------|:----:|:-------:|:-----------:|---------|
|`transactionId`|Texto|150|Não|Utilize somente para intenções de venda previamente configuradas|
|`orderId`|Texto|100|Sim|Numero de identificação da loja.|
|`amount`|Número|16|Sim|Valor da transação.|
|`description`|Texto|300|Não|Descrição da venda.|
|`customer.name`|Texto|100|Sim|Nome do portador do cartão.|
|`customer.document`|Texto|18|Sim|Número do CPF/CNPJ do portador do cartão.|
|`customer.email`|Texto|100|Sim|Email do portador do cartão.|
|`address.address`|Texto|60|Sim|Endereço do comprador.|
|`address.district`|Texto|80|Sim|Bairro do comprador.|
|`address.zipcode`|Texto|10|Sim|CEP do comprador.|
|`address.city`|Texto|30|Sim|Cidade do comprador.|
|`address.state`|Texto|2|Sim|Sigla do estado do comprador.|
|`payment.bankSlip.expirationDate`|Texto|20|Sim|Data de vencimento do boleto. formato **YYYY-MM-DD**|
|`payment.bankSlip.instructions`|Texto|300|Sim|Instruções do boleto.|
|`payment.bankSlip.guarantor`|Texto|45|Sim|Nome do avalista.|
|`payment.bankSlip.provider`|Texto|20|Sim|Nome da instituição financeira :<ul><li>**BRADESCO**</li><li>**ITAU**</li></ul>|

### RESPOSTA

```json
{
  "transactionId": "62d02f48-ef2c-4518-9e6f-68ca5cbc4231",
  "orderId": "19893211234",
  "amount": "100",
  "description": "Produto ou serviço",
  "dtTransaction": "1970-01-01T00:00:00",
  "customer": {
    "name": "Comprador",
    "document": "12345678909",
    "email": "comprador@email.com",
    "address": {
      "address": "Rua Fidencio Ramos 100",
      "district": "Vila Olimpia",
      "zipcode": "05890090",
      "city": "Sao Paulo",
      "state": "SP"
    }
  },
  "payment": {
    "providerReference": "0987654321",
    "bankSlip": {
      "emissionDate": "1970-01-01",
      "expirationDate": "1970-01-01",
      "instructions": "Aceitar somente até a data de vencimento, após essa data juros de 1% dia",
      "guarantor": "Comprador",
      "provider": "Itau",
      "paymentDate": null,
      "paymentAmount": null,
      "url": "<%= url_gateway %>/v1/url-payment/62d02f48-ef2c-4518-9e6f-68ca5cbc4231"
    }
  },
  "status": 0
}
```


```shell  
```


|Propriedade|Tipo|Tamanho|Descrição|
|-----------|:----:|:-------:|---------|
|`transactionId`|Texto|150|Identificador da transação retornado pelo gateway.|
|`orderId`|Texto|100|Numero de identificação da loja.|
|`amount`|Número|16|Valor da transação.|
|`description`|Texto|300|Descrição da transação.|
|`dtTransaction`|DataHora|19|Data e hora da transação.|
|`customer.name`|Texto|100|Nome do portador do cartão.|
|`customer.document`|Texto|18|Número do CPF/CNPJ do portador do cartão.|
|`customer.email`|Texto|100|Email do portador do cartão.|
|`address.address`|Texto|60|Endereço do comprador.|
|`address.district`|Texto|80|Bairro do comprador.|
|`address.zipcode`|Texto|10|CEP do comprador.|
|`address.city`|Texto|30|Cidade do comprador.|
|`address.state`|Texto|2|Sigla do estado do comprador.|
|`payment.providerReference`|Texto|100|Referencia da instituição.|
|`payment.bankSlip.emissionDate`|Texto|20|Data de emissão do boleto. formato **YYYY-MM-DD**|
|`payment.bankSlip.expirationDate`|Texto|20|Data de vencimento do boleto. formato **YYYY-MM-DD**|
|`payment.bankSlip..instructions`|Texto|300|Instruções do boleto.|
|`payment.bankSlip..guarantor`|Texto|45|Nome do avalista.|
|`payment.bankSlip..provider`|Texto|20|Nome da instituição financeira :<ul><li>**BRADESCO**</li><li>**ITAU**</li></ul>|
|`payment.bankSlip.paymentDate`|Texto|20|Data de pagamento do boleto. formato **YYYY-MM-DD**|
|`payment.bankSlip.paymentAmount`|Número|16|Valor de pagamento do boleto.|
|`payment.bankSlip.url`|Texto|300|Endereço de acesso da transação.|
|`status`|Numero|2|[tabela de Status](#status)|


## Transferência entre contas bancárias

Este tipo de transação permite a transferência de valores entre contas do banco Bradesco, a compensação é realizada no mesmo dia. Esse meio de pagamento é integrado ao Internet Banking.

No momento do pagamento, o cliente comprador informa os dados da agência, informa os dados da conta, como senha de 4 dígitos e do dispositivo de segurança (Cartão Chave de Segurança Bradesco ou Chave de Segurança Bradesco - versão Eletrônica ou no Celular.

### Requisição

<aside class="request"><span class="method post">POST</span> <span class="endpoint">/v1/transactions/eletronictransfer/</span></aside>

```json
{
    "orderId": "19893211234",
    "amount": "100",
    "description": "Produto ou serviço",
    "customer": {
      "name": "Comprador",
      "document": "12345678909",
      "email": "comprador@email.com",
      "address": {
        "address": "Rua Fidencio Ramos 100",
        "district": "Vila Olimpia",
        "zipcode": "05890090",
        "city": "Sao Paulo",
        "state": "SP"
      }
    },
   "payment": {
       "electronicTransfer" : {
           "provider" : "Itau"
       }
    }
}
```

```shell
```

|Propriedade|Tipo|Tamanho|Obrigatório|Descrição|
|-----------|:----:|:-------:|:-----------:|---------|
|`transactionId`|Texto|150|Não|Utilize somente para intenções de venda previamente configuradas|
|`orderId`|Texto|100|Sim|Numero de identificação da loja.|
|`amount`|Número|16|Sim|Valor da transação.|
|`description`|Texto|300|Não|Descrição da venda.|
|`customer.name`|Texto|100|Sim|Nome do portador do cartão.|
|`customer.document`|Texto|18|Sim|Número do CPF/CNPJ do portador do cartão.|
|`customer.email`|Texto|100|Sim|Email do portador do cartão.|
|`address.address`|Texto|60|Sim|Endereço do comprador.|
|`address.district`|Texto|80|Sim|Bairro do comprador.|
|`address.zipcode`|Texto|10|Sim|CEP do comprador.|
|`address.city`|Texto|30|Sim|Cidade do comprador.|
|`address.state`|Texto|2|Sim|Sigla do estado do comprador.|
|`payment.electronicTransfer.provider`|Texto|20|Sim|Nome da instituição financeira :<ul><li>**BRADESCO**</li><li>**ITAU**</li></ul>|

### RESPOSTA

```json
{
    "transactionId": "6400d988-cc4b-4084-80ee-d5575dbbed4d",
    "orderId": "19893211234",
    "amount": "100",
    "description": "Produto ou serviço",
    "dtTransaction": "2016-10-30T16:16:14-0200",
    "customer": {
      "name": "Comprador",
      "document": "12345678909",
      "email": "comprador@email.com",
      "address": {
        "address": "Rua Fidencio Ramos 100",
        "district": "Vila Olimpia",
        "zipcode": "05890090",
        "city": "Sao Paulo",
        "state": "SP"
      }
    },
    "payment": {
        "providerReference": "20518839",
        "electronicTransfer": {
            "provider": "Itau",
            "url": "<%= url_gateway %>/v1/url-payment/6400d988-cc4b-4084-80ee-d5575dbbed4d"
        }
    },
    "status": 0
}
```


```shell
```


|Propriedade|Tipo|Tamanho|Descrição|
|-----------|:----:|:-------:|---------|
|`transactionId`|Texto|150|Identificador da transação retornado pelo gateway.|
|`orderId`|Texto|100|Numero de identificação da loja.|
|`amount`|Número|16|Valor da transação.|
|`description`|Texto|300|Descrição da transação.|
|`dtTransaction`|DataHora|19|Data e hora da transação.|
|`customer.name`|Texto|100|Nome do portador do cartão.|
|`customer.document`|Texto|18|Número do CPF/CNPJ do portador do cartão.|
|`customer.email`|Texto|100|Email do portador do cartão.|
|`address.address`|Texto|60|Endereço do comprador.|
|`address.district`|Texto|80|Bairro do comprador.|
|`address.zipcode`|Texto|10|CEP do comprador.|
|`address.city`|Texto|30|Cidade do comprador.|
|`address.state`|Texto|2|Sigla do estado do comprador.|
|`payment.providerReference`|Texto|100|Referencia da instituição.|
|`payment.electronicTransfer.provider`|Texto|20|Nome da instituição financeira :<ul><li>**BRADESCO**</li><li>**ITAU**</li></ul>|
|`payment.electronicTransfer.url`|Texto|300|Endereço de acesso da transação.|
|`status`|Numero|2|[tabela de Status](#status)|


## Captura

Captura é a confirmação de uma transação autorizada, após a captura que é confirmada a transação entre lojista e comprador, gerando o crédito para o lojista e o lançamento do débito na fatura do portador do cartão.

### Regras da captura

|Rede adquirente|Prazo|Captura Parcial|
|---------------|-----|---------------|
|`Cielo`|5 dias|Sim|
|`Rede(Komerci)`|2 minutos|Não|
|`GetNet`|20 dias|Sim|

* O prazo pode ser alterado para até 28 dias.

* Transações de pré-autorização podem ser capturadas em até 30 dias.

### Requisição

<aside class="request"><span class="method put">PUT</span> <span class="endpoint">/v1/transactions/{{transactionId}}/capture/</span></aside>

|Propriedade|Tipo|Tamanho|Obrigatório|Descrição|
|-----------|----|-------|-----------|---------|
|`transactionId`|Texto|150|Sim|Identificador da transação retornado pelo gateway.|

### RESPOSTA

> Transação autorizada e capturada

```json
{
  "retorno": {
    "transactionId": "e8e7c437-3cbf-4108-a482-2b870e0d8ead",
    "message": "Transacao capturada com sucesso",
    "amount": "100",
    "tid": "10069930690006A8C0CA",
    "status": "AUTORIZADA_E_CAPTURADA",
    "responseCode": "00"
  }
}
```


```shell
  {
    "retorno": {
      "transactionId": "e8e7c437-3cbf-4108-a482-2b870e0d8ead",
      "message": "Transacao capturada com sucesso",
      "amount": "100",
      "tid": "10069930690006A8C0CA",
      "status": "AUTORIZADA_E_CAPTURADA",
      "responseCode": "00"
    }
  }
   
```


|Propriedade|Tipo|Tamanho|Descrição|
|-----------|----|-------|-----------|---------|
|`transactionId`|Texto|150|Identificador da transação retornado pelo gateway.|
|`message`|Texto|100|Mensagem de retorno da transação.|
|`amount`|Número|16|alor da transação.|
|`tid`|Texto|100|Identificador da transação retornado pela rede adquirente.|
|`status`|Número|2|Status da transação retornado pelo gateway.|
|`responseCode`|Texto|2|Código de resposta retornado pela rede adquirente.|


## Captura Parcial

Para efetuar uma captura parcial, é necessário enviar um POST passando como parametro o valor a ser capturado.

### Requisição

<aside class="request"><span class="method put">PUT</span> <span class="endpoint">/v1/transaction/{{transactionId}}/capture?amount=100</span></aside>

|Propriedade|Tipo|Tamanho|Obrigatório|Descrição|
|-----------|----|-------|-----------|---------|
|`transactionId`|Texto|150|Sim|Identificador da transação retornado pelo gateway.|
|`amount`|Número|16|Sim|Valor da transação a ser capturado.|

### RESPOSTA

> Transação autorizada e capturada

```json
{
  "retorno": {
    "transactionId": "e8e7c437-3cbf-4108-a482-2b870e0d8ead",
    "message": "Transacao capturada com sucesso",
    "amount": "100",
    "tid": "10069930690006A8C0CA",
    "status": "AUTORIZADA_E_CAPTURADA",
    "responseCode": "00"
  }
}
```


```shell
    {
      "retorno": {
        "transactionId": "e8e7c437-3cbf-4108-a482-2b870e0d8ead",
        "message": "Transacao capturada com sucesso",
        "amount": "100",
        "tid": "10069930690006A8C0CA",
        "status": "AUTORIZADA_E_CAPTURADA",
        "responseCode": "00"
      }
    }
```


|Propriedade|Tipo|Tamanho|Descrição|
|-----------|----|-------|-----------|---------|
|`transactionId`|Texto|150|Identificador da transação retornado pelo gateway.|
|`message`|Texto|100|Mensagem de retorno da transação.|
|`amount`|Número|16|Valor da transação.|
|`tid`|Texto|100|Identificador da transação retornado pela rede adquirente.|
|`status`|Número|2|Status da transação retornado pelo gateway.|
|`responseCode`|Texto|2|Código de resposta retornado pela rede adquirente.|


## Cancelamento

Para realizar um cancelamento "estorno", deve-se observar as seguintes condições:

### Prazos para cancelamento

|Rede adquirente|Prazo para cancelamento|
|---------------|-----|
|`Cielo`|300 dias|
|`Rede(Komerci)`|* Até às 23:59 a partir da data da transação. <BR /> * Pré-autorização prazo 15 dias.|
|`GetNet`|Até 2 dias.|

### Requisição

<aside class="request"><span class="method put">PUT</span> <span class="endpoint">/v1/transaction/{{transactionId}}/void</span></aside>

|Propriedade|Tipo|Tamanho|Obrigatório|Descrição|
|-----------|----|-------|-----------|---------|
|`transactionId`|Texto|150|Sim|Identificador da transação retornado pelo gateway.|

### RESPOSTA

> Transação cancelada

```json
{
  "retorno": {
    "transactionId": "e8e7c437-3cbf-4108-a482-2b870e0d8ead",
    "message": "Transacao cancelada com sucesso",
    "amount": "100",
    "tid": "10069930690006A8C0CA",
    "status": "CANCELADA",
    "responseCode": "00"
  }
}
```


```shell
   {
     "retorno": {
       "transactionId": "e8e7c437-3cbf-4108-a482-2b870e0d8ead",
       "message": "Transacao cancelada com sucesso",
       "amount": "100",
       "tid": "10069930690006A8C0CA",
       "status": "CANCELADA",
       "responseCode": "00"
     }
   }
```


|Propriedade|Tipo|Tamanho|Descrição|
|-----------|----|-------|-----------|---------|
|`transactionId`|Texto|150|Identificador da transação retornado pelo gateway.|
|`message`|Texto|100|Mensagem de retorno da transação.|
|`amount`|Número|16|Valor da transação.|
|`tid`|Texto|100|Identificador da transação retornado pela rede adquirente.|
|`status`|Número|2|Status da transação retornado pelo gateway.|
|`responseCode`|Texto|2|Código de resposta retornado pela rede adquirente.|

## Cancelamento Parcial

Para efetuar um cancelamento parcial é necessário enviar um POST passando como parametro o valor a ser cancelado.

### Requisição

<aside class="request"><span class="method put">PUT</span> <span class="endpoint">/v1/transaction/{{transactionId}}/void?amount=100</span></aside>

|Propriedade|Tipo|Tamanho|Obrigatório|Descrição|
|-----------|----|-------|-----------|---------|
|`transactionId`|Texto|150|Sim|Identificador da transação retornado pelo gateway.|
|`amount`|Número|16|Sim|Valor da transação.|

### RESPOSTA

> Transação cancelada

```json
{
  "retorno": {
    "transactionId": "e8e7c437-3cbf-4108-a482-2b870e0d8ead",
    "message": "Transacao cancelada com sucesso",
    "amount": "100",
    "tid": "10069930690006A8C0CA",
    "status": "CANCELADA",
    "responseCode": "00"
  }
}
```


```shell
    {
       "retorno": {
         "transactionId": "e8e7c437-3cbf-4108-a482-2b870e0d8ead",
         "message": "Transacao cancelada com sucesso",
         "amount": "100",
         "tid": "10069930690006A8C0CA",
         "status": "CANCELADA",
         "responseCode": "00"
       }
     }
```


|Propriedade|Tipo|Tamanho|Descrição|
|-----------|----|-------|-----------|---------|
|`transactionId`|Texto|150|Identificador da transação retornado pelo gateway.|
|`message`|Texto|100|Mensagem de retorno da transação.|
|`amount`|Número|16|Valor da transação.|
|`tid`|Texto|100|Identificador da transação retornado pela rede adquirente.|
|`status`|Número|2|Status da transação retornado pelo gateway.|
|`responseCode`|Texto|2|Código de resposta retornado pela rede adquirente.|


## Consulta

Para realizar uma consulta é necessário enviar um GET para o seguinte recurso:

### Requisição

<aside class="request"><span class="method get">GET</span> <span class="endpoint">/v1/transaction/{{transactionId}}/</span></aside>

|Propriedade|Tipo|Tamanho|Obrigatório|Descrição|
|-----------|----|-------|-----------|---------|
|`transactionId`|Texto|150|Sim|Identificador da transação retornado pelo gateway.|


### RESPOSTA

```json
{
  "retorno": {
    "transactionId": "e8e7c437-3cbf-4108-a482-2b870e0d8ead",
    "orderId": "1463697571584",
    "amount": "100",
    "tid": "10069930690006A8C0CA",
    "authorizationCode": "123456",
    "status": "CANCELADA"
  }
}
```


```shell
  {
    "retorno": {
      "transactionId": "e8e7c437-3cbf-4108-a482-2b870e0d8ead",
      "orderId": "1463697571584",
      "amount": "100",
      "tid": "10069930690006A8C0CA",
      "authorizationCode": "123456",
      "status": "CANCELADA"
    }
  }
  
```


|Propriedade|Tipo|Tamanho|Descrição|
|-----------|----|-------|-----------|---------|
|`transactionId`|Texto|150|Identificador da transação retornado pelo gateway.|
|`orderId`|Texto|100|Sim|Numero de identificação da loja.|
|`amount`|Número|16|Valor da transação.|
|`tid`|Texto|100|Identificador da transação retornado pela rede adquirente.|
|`status`|Número|2|Status da transação retornado pelo gateway.|
|`authorizationCode`|Texto|2|Código de autorização retornado pela rede adquirente.|


# LightBox

O gate2All disponibiliza uma biblioteca javascript para facilitar a integração com o seu site.

<img src="images/lightBox.png" />

* Primeiro o usuário deve acessar o seguinte endereço: <a href='http://192.168.20.79:9191' target='_blank'>clicar aqui</a>

* Depois que logar com suas credenciais, ele deve acessar o menu clientes, depois ir em configuração.
  
<img src="images/lightBoxp1.png" />

* Clicar no botão "Visualizar". Copiar o usuario e o token.

<img src="images/lightBoxp2.png" />

     
> Em sua página web você deve importar os seguintes scripts.

```js
<script src="path/jquery.min.js" />
<script>
 id="gate2all-payment"
 src="js/lightBoxGate2all.js"
 data-company="Setis"
 data-button="Enviar doação"
 data-user="sdfsfsdfdf345453"
 data-password="klkljkljkl45jk45"
 data-fixedinstallments="true"
 data-operationtype="3"
 data-installments="6"
 data-capture="false"
</script>
```
            
|Propriedade|Tipo|Tamanho|Descrição|
|-----------|----|-------|-----------|---------|
|`data-company`|Texto|150|Nome da sua empresa| 
|`data-button`|Texto|150|Texto do botão de enviar transação| 
|`data-user`|Texto|150|Usuário copiado do site| 
|`data-password`|Texto|150|Token copiado do site| 
|`data-fixedinstallments`|Booleano|-|Flag utilizada para indicar se a parcela é fixa| 
|`data-operationtype`|Número|2|Tipo de parcelamento. ADM: 2 ou Loja: 3| 
|`data-installments`|Número|16|Valor do numero de parcelas fixa| 
|`data-capture`|Booleano|-|Flag para capturar suas transações depois de completas| 

> Nos campos de valor da compra e número do documento devem ter os seguintes id's:
     *id="valor"; id="pedido";*

<br />
     
> Segue a chamada do botão para chamar a tela lightBox de pagamento:

```js    
<button type="button" name="chamaPag" data-toggle="modal" data-target="#modalPag">Dados de Pagamento</button>
``` 
 
> Deve colocar essa div dentro do body onde está o "button":

```js    
<div id="payment-form"></div>
```
