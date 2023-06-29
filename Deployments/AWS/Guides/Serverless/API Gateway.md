# Lambda Function Stage Variables

- Create lambda unction with versions
	- PROD
	- DEV
	- TEST
- Create Get request that uses stage variable
- `demoLambdaAPIGWProxyRouteGet:${stageVariables.lambdaAlias}`
- Add permission to lambda function
	- Resource based policy to allow API gateway to invoke function
	- `aws lambda add-permission --function-name "arn:aws:lambda:eu-west-2:495020837192:function:demoLambdaAPIGWProxyRouteGet:DEV" --source-arn "arn:aws:execute-api:eu-west-2:495020837192:yer04mxfa6/*/GET/stagevariables" --principal apigateway.amazonaws.com --statement-id 0a076a7c-8a1c-4cdb-a216-19d7ee752bbe --action lambda:InvokeFunction`
	- Do this for each alias
- Deploy API Stage
	- Configure stageVariables in stage

# Mapping Templates

- API gateway
- Go to API call
- Integration Response
	- Expand
	- Mapping Templates

# Enable CORS

- API
- Resource
- Action
	- Enable CORS
		- Access-Control-Allow-Origin
		- Input domain of resource

If using  lambda proxy

- Go to lambda function to allow CORS
- Allow `'Access-Control-Allow-Origin' : '*'` in lambda function request