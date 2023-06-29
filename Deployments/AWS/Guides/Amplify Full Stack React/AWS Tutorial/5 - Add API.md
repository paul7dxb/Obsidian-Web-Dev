- GraphQL API that uses AWS AppSync (managed GraphQL service backed by Amazon DynamoDB NoSQL)

# Add API to project

```
amplify add api

? Select from one of the below mentioned services: GraphQL
? Here is the GraphQL API that we will create. Select a setting to edit or continue: Continue
? Choose a schema template: Single object with fields (e.g., "Todo" with ID, name, description)
? Do you want to edit the schema now? (Y/n) yes
```

# Edit Schema

- Found in **/amplify/backend/api/<api_name>/schema.graphql.**

Example:
```graphQL
type Note @model @auth(rules: [ { allow: public } ] ){
  id: ID!
  name: String!
  description: String
}
```

# Deploy Changes

```bash
amplify push --y
```

This will do three things:

- Create the AWS AppSync API
- Create a DynamoDB table
- Create the local GraphQL operations in a folder located at src/graphql that you can use to query the API

- How to View GraphQL API
```bash
amplify console api

> Choose GraphQL
```

- How to view Amplify App
```bash
amplify console
? Which site do you want to open? AWS console
```