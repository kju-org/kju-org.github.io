# kju API

kju is an open communication platform that works on a simple `request <-> response` pattern. 

* Any participator can create a request with a number of predefined responses.
* Any participator can redeem a response for a given request

# Basics

...

# Tokens

Being an open and simple platform, kju doesn't require a registration or login. You will, however need tokens for working with the API.

There are different types of tokens:

* ***create token***  for creating messages
* ***read token*** for reading particular messages (each token is valid for a specific message)
* ***redeem token*** for redeeming responses for a given message
* ***seeResponses token*** for viewing the responses for a given message



>  When creating a message, the tokens will be generated and returned!

# API

kju is consumed via a REST API and offers the following endpoints:

* `POST /creationToken`
* `POST /message`
* `GET /message/:messageId`
* `GET /message/:messageId/response/:responseId`
* `GET /message/:messageId/responses`

## (Browser API)

The following two API Endpoints can also be opened int he browser. kju will then render them with a tiny UI.

* `/message/:messageId` 

* `/message/:messageId/responses` 




## GET a token

Generates a token for creating a message

```
Endpoint: /api/token
Method: POST
Data:
{
	createToken: "XXX"
}
```

## CREATE a message

Creates a message in the kju platform.

```
Endpoint: /api/message?token=XXX
Method: POST
Query Params: token
Data:
{
	content: "",
	responses: [{

	}]
}
```

## SEE a message

Returns a raw message

```
Endpoint: /api/message/:messageId?token=XXX
Method: GET
Query Params: token
Returns:
{
	...
}
```

## REDEEM a response

Webhook for redeeming a predefined response for a given message

```
Endpoint: /api/message/:messageId/response/:responseId?token=XXX
Method: GET
Query Params: token
Returns:
{
	...
}
```

## SEE responses

Returns the redeemed responses for a given message

```
Endpoint: /api/message/:messageId/responses?token=XXX
Method: GET
Query Params: token
Returns:
{
	responseId: {
		content: "",
		responses: [{}]
	}
}
```