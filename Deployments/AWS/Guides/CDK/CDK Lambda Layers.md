# Create Lambda Layer

- [Docs](https://docs.aws.amazon.com/cdk/api/v1/docs/@aws-cdk_aws-lambda.LayerVersion.html#static-from-layer-version-arnscope-id-layerversionarn)
- Create `lambda.LayerVersion`
- Make publicly available for other stacks

```ts
import { RemovalPolicy, Stack, StackProps } from "aws-cdk-lib";
import * as ddb from "aws-cdk-lib/aws-dynamodb";
import * as lambda from "aws-cdk-lib/aws-lambda";
import { Construct } from "constructs";

export class DatabaseStack extends Stack {
	// Public variables
	public readonly database: ddb.Table;
	public readonly dbLayer: lambda.LayerVersion;
	// public readonly layer: lambda.LayerVersion;

	constructor(scope: Construct, id: string, props?: StackProps) {
		super(scope, id, props);

		this.database = new ddb.Table(this, "entry-table", {
			partitionKey: {
				name: "id",
				type: ddb.AttributeType.STRING,
			},
			billingMode: ddb.BillingMode.PAY_PER_REQUEST,
			removalPolicy: RemovalPolicy.DESTROY,
		});

		// Setup a Lambda layer for sharing database functions ------------------------
		this.dbLayer = new lambda.LayerVersion(
			this,
			"shared-db-functions-layer",
			{
				code: lambda.Code.fromAsset(`${__dirname}/lambda/database-read-layer`),
				compatibleRuntimes: [lambda.Runtime.NODEJS_18_X],
				license: "Apache-2.0",
				description: "Layer for common database access functions",
			}
		);
	}
}

```

- Read into other stack

```ts
import { Duration, RemovalPolicy, Stack, StackProps } from "aws-cdk-lib";
import * as ddb from "aws-cdk-lib/aws-dynamodb";
import * as lambda from "aws-cdk-lib/aws-lambda";
import { Construct } from "constructs";
import { LambdaToDynamoDB } from "@aws-solutions-constructs/aws-lambda-dynamodb";

// Properties for the service-staff-stack
export interface AdminStackProps {
	// The main database created in the database-stack
	readonly db: ddb.Table;
    readonly dbLayer: lambda.LayerVersion;
}

export class AdminStack extends Stack {
	// Constructor
	constructor(scope: Construct, id: string, props: AdminStackProps) {
		super(scope, id);

		const addEntry = new LambdaToDynamoDB(this, "add-entry", {
			lambdaFunctionProps: {
				runtime: lambda.Runtime.NODEJS_18_X,
				code: lambda.Code.fromAsset(`${__dirname}/lambda/get-entry`),
				handler: "index.handler",
                layers: [props.dbLayer],
				timeout: Duration.seconds(30),
			},
			existingTableObj: props.db,
		});
	}
}

```

