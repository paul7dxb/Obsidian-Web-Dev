```ts
import * as lambda from "aws-cdk-lib/aws-lambda";
import * as apigateway from "aws-cdk-lib/aws-apigateway";

//REST API
const api = new apigateway.RestApi(this, "CdkSandboxApi", {
	defaultCorsPreflightOptions: {
		allowOrigins: apigateway.Cors.ALL_ORIGINS,
		allowMethods: apigateway.Cors.ALL_METHODS,
	},
});

//lambda
const lambdaFunction = new lambda.Function(this, "CdkSandboxLambda", {
	runtime: lambda.Runtime.NODEJS_18_X,
	handler: "index.handler",
	code: lambda.Code.fromAsset("./lambda/CdkSandboxLambda"),
	memorySize: 128,
	timeout: cdk.Duration.seconds(10),
});

//lambda
const lambdaTwoFunction = new lambda.Function(
	this,
	"CdkSandboxLambdaTwo",
	{
		runtime: lambda.Runtime.NODEJS_18_X,
		handler: "index.handler",
		code: lambda.Code.fromAsset("./lambda/CdkSandboxLambdaTwo"),
		memorySize: 128,
		timeout: cdk.Duration.seconds(10),
	}
);

// Connect lambda to API
const lambdaIntegration = new apigateway.LambdaIntegration(
	lambdaFunction
);
api.root.addMethod("GET", lambdaIntegration);

// Connect lambda to API
const apiResource = api.root.addResource("lambdaTwo");

const lambdaTwoIntegration = new apigateway.LambdaIntegration(
	lambdaTwoFunction
);
	apiResource.addMethod("GET", lambdaTwoIntegration);
```