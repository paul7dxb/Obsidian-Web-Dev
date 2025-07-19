# Routing through Gateway

- Determined by payload sent from client
- API Gateway has an attribute that it will use to determine the path
![[AWS_API_GW_WebSocket_Route.png]]
- Example event
	- Action to be sent to route "echoMessage"

```JSON
{
   "requestContext":{
      "routeKey":"echoMessage",
      "messageId":"Ga4JueZBLPECIsg=",
      "eventType":"MESSAGE",
      "extendedRequestId":"Ga4JuGBQrPEF25g=",
      "requestTime":"12/Jun/2023:19:09:37 +0000",
      "messageDirection":"IN",
      "stage":"dev",
      "connectedAt":1686596601950,
      "requestTimeEpoch":1686596977132,
      "identity":{
         "userAgent":"Mozilla/5.0",
         "sourceIp":"x.x.x.x"
      },
      "requestId":"Ga4JlUeQrPEF25g=",
      "domainName":"6behyoa40f.execute-api.eu-west-2.amazonaws.com",
      "connectionId":"Ga3PGd2wLPECIsg=",
      "apiId":"6behyoa40f"
   },
   "body":"{\"action\":\"echoMessage\", \"message\":\"hello there...\"}",
   "isBase64Encoded': False
}
```
# Permission to Send to Invoke WebSocket API

`AmazonAPIGatewayInvokeFullAccess`

# Connecting

```JS
exports.handler = async (event, context) => {

     //Starting Connection with webSocket
     console.log(event)
     console.log("******************")
     console.log(context)
     
    const response = {
        statusCode: '200',
        body: JSON.stringify({ msg: 'Connected To Websocket'}),
    };

    return response;
};

```

```python 
# Version 3.8
import json

def lambda_handler(event, context):
    print(event)
    print("****")
    print(context)

```

# Send Message to Client
```python 
# Version 3.8
#SendMessage - Needs AmazonAPIGatewayInvokeFullAccess IAM Policy


import json
import urllib3
import boto3

client = boto3.client('apigatewaymanagementapi', endpoint_url="xxxxxxxxxx.com/production")

def lambda_handler(event, context):
    print(event)
    
    #Extract connectionId from incoming event
    connectionId = event["requestContext"]["connectionId"]
    
    #Do something interesting... 
    responseMessage = "responding..."
    
    #Form response and post back to connectionId
    response = client.post_to_connection(ConnectionId=connectionId, Data=json.dumps(responseMessage).encode('utf-8'))
    return { "statusCode": 200  }
```

# Process Received Message & Reply

- Message body sent by client:
	- `{"action":"echoMessage", "message":"hello there..."}`
- Lambda retrieves the message from the event
- Lambda responds to client with processed message

```python 
# Version 3.8
# Broadcast - Needs AmazonAPIGatewayInvokeFullAccess IAM Policy

import json
import urllib3
import boto3

client = boto3.client('apigatewaymanagementapi', endpoint_url="https://6behyoa40f.execute-api.eu-west-2.amazonaws.com/dev/")

def lambda_handler(event, context):
    print("***EVENT***")
    print(event)
    
    #Extract connectionId from incoming event
    connectionId = event["requestContext"]["connectionId"]
    messageBody = event["body"]
    print (messageBody)
    json_data = json.loads(messageBody)
    
    userMessage = json_data["message"]
    print("userMessage: ")
    print(userMessage)
    
    print("***connectionId***")
    print(connectionId)
    
    #Do something interesting... 
    responseMessage = "Your message was: " + userMessage
    
    
    #Form response and post back to connectionId
    response = client.post_to_connection(ConnectionId=connectionId, Data=json.dumps(responseMessage).encode('utf-8'))
    return { "statusCode": 200  }

```


# Websocket Info

- [Link]([https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-websocket-api-route-keys-connect-disconnect.html](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-websocket-api-route-keys-connect-disconnect.html))
```
{
    "connectionId": "$context.connectionId",
    "domain": "$context.domainName",
    "stage": "$context.stage",
    "params": "$input.params()"
}
```