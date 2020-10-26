# API

> 👍 For easy adoption and embedding into any system, kju works on some simple but versatile concepts. There are only a small number of API endpoints that do the job.

> 🔑 For <u>Authentication</u>, kju doesn't rely on annoying registration and login procedures. Instead, a token-based authentification methodology is used. In order to create messages, one must create a token (one-time) first. This token can then be used to create messages. Tokens for viewing and redeeming responses are bound to specific messages and will be generated and returned when a message is created.


The API (alpha version!) is available under:

`http://europe-west3-spoocloud-202009.cloudfunctions.net/kju-dummy/api`

## GET a token

Generates a token for creating a message. The token will be sent to the contact email address.

```
Endpoint: /api/personalToken
Method: POST
Data:
{
	contact: "email"
}
Returns:
{
	data: "TOKEN"
}
```

## CREATE a message

Creates a message in the kju platform and returns the neccessary tokens for viewing and redeeming responses.

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
Returns:
{
	_id: "auto generated id",
	content: "",
	responses: [{

	}]
}
```

## ALLOW correspondence

When a sender adresses a reciever within a message for the first time, the reciever hast to allow further correspondence with that sender. Otherwise, further messages to that reciever will not be delivered.

```
Endpoint: /api/permitCorrespondence?token=XXX
Method: POST
Query Params: token
Data:
{
	contact: "email of sender",
}
Returns:
{
	msg: "ok"
}
```

## SEE a message

Returns a raw message.

> When opened in the browser, a UI will be rendered.

```
Endpoint: /api/message/:messageId?token=XXX
Method: GET
Query Params: token
Returns:
{
	_id: "auto generated id",
	content: "",
	responses: [{

	}]
}
```

## DELETE a message

Deletes a message.

> Can only be performend with the same token, that the message was created with!

```
Endpoint: /api/message/:messageId?token=XXX
Method: DELETE
Query Params: token
Returns:
{
	msg: "ok"
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
	msg: "ok"
}
```

## SEE responses

Returns the redeemed responses for a given message

> When opened in the browser, a UI will be rendered.

```
Endpoint: /api/message/:messageId/responses?token=XXX
Method: GET
Query Params: token
Returns:
[
	{
		_id: "auto generated id",
		response: "responseId",
		timestamp: "ISO-8601"
	}
]
```

## SEE messages

Returns the messages matching a messageTag

> The messageTag is encoded inside the token. 

> When opened in the browser, a UI will be rendered.

```
Endpoint: /api/messages?token=XXX
Method: GET
Query Params: token
Returns:
[
	{
		_id: "auto generated id",
		content: "content",
		responses: [...]
	}
]
```
