- Give Lambda permission to start Step Function
```JSON
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "StepFunctionsStartExecution",
      "Effect": "Allow",
      "Action": "states:StartExecution",
      "Resource": "arn:aws:states:eu-west-2:12345678:stateMachine:StatMachineName"
    }
  ]
}

```

```python
# Version 3.8

import json
import urllib3
import boto3

from datetime import datetime

apigw_client = boto3.client('apigatewaymanagementapi', endpoint_url="https://6behyoa40f.execute-api.eu-west-2.amazonaws.com/dev/")
# Step Functions ARN
state_machine_arn = "arn:aws:states:eu-west-2:12345678:stateMachine:MyStateMachine"

def lambda_handler(event, context):
    
    #Extract connectionId from incoming event
    connectionId = event["requestContext"]["connectionId"]

    # Generate the execution name using current date and time
    execution_name = datetime.now().strftime("%Y-%m-%d-%H-%M-%S")

    # Create the Step Functions client
    stepfunctions_client = boto3.client('stepfunctions')

    # Start the Step Functions execution
    response = stepfunctions_client.start_execution(
        stateMachineArn=state_machine_arn,
        name=execution_name,  # Optional: Provide a unique name for the execution
        input='{}'  # Optional: Provide input data as a JSON string
    )

    # Print the response
    print("***RESPONSE***")
    print(response)
    print("***connectionId***")
    print(connectionId)
    
    #Do something interesting... 
    responseMessage = "All good in the step func"
    
    #Form response and post back to connectionId
    response = apigw_client.post_to_connection(ConnectionId=connectionId, Data=json.dumps(responseMessage).encode('utf-8'))
    return { "statusCode": 200  }

```