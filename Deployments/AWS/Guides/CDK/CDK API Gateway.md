```TS
// REST api
	const wildRydesApi = new apigateway.RestApi(this, "WildRydesApi", {
		defaultCorsPreflightOptions: {
			allowOrigins: apigateway.Cors.ALL_ORIGINS,
			allowMethods: apigateway.Cors.ALL_METHODS,
		},
	});
```

## With Cognito Authorizer
```TS
// REST api
const wildRydesApi = new apigateway.RestApi(this, "WildRydesApi", {
	defaultCorsPreflightOptions: {
		allowOrigins: apigateway.Cors.ALL_ORIGINS,
		allowMethods: apigateway.Cors.ALL_METHODS,
	},
});

// API Authorizer
const userPoolAuthorizer = new apigateway.CfnAuthorizer(
	this,
	"WildRydesAuthorizer",
	{
		restApiId: wildRydesApi.restApiId,
		name: "WildRydesAuthorizer",
		type: "COGNITO_USER_POOLS",
		identitySource: "method.request.header.Authorization",
		providerArns: [userPool.userPoolArn],
	}
);

//API resource
const wildRydesResourceRide = wildRydesApi.root.addResource("ride");

// Connect lambda to API
const wildRydeslambdaIntegration = new apigateway.LambdaIntegration(
	wildRydesLambda
);

wildRydesResourceRide.addMethod("POST", wildRydeslambdaIntegration, {
	authorizationType: apigateway.AuthorizationType.COGNITO,
	authorizer: { authorizerId: userPoolAuthorizer.ref },
});
```