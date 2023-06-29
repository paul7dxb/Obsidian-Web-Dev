```Python
# Lambda permissions
table.grant_read_write_data(self.handler) # Read and write to Dynamo DB

downstream.grant_invoke(self.handler) # Invoke another lambda function downstream
```

# Lambda Role

```ts
lambdaFn.addToRolePolicy(new iam.PolicyStatement({
  effect: iam.Effect.ALLOW,
  actions: ["ses:SendEmail", "ses:SendRawEmail"],
  resources: ["*"],
  conditions: {
	StringEquals: {
	  "ses:FromAddress": verifiedEmail,
	},
  },
}))
```
