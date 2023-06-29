# Add S3

- Create, update, read delete set using spacebar

```bash
amplify add storage

? Select from one of the below mentioned services: Content (Images, audio, video, etc.)
? Provide a friendly name for your resource that will be used to label this category in the project: imagestorage
? Provide bucket name: <your-unique-bucket-name>
? Who should have access: Auth users only
? What kind of access do you want for Authenticated users? create/update, read, delete
? Do you want to add a Lambda Trigger for your S3 Bucket? (y/N) no
```

# Add Image to GraphQL Schema

```graphql
type Note @model @auth(rules: [ { allow: public } ] ){
  id: ID!
  name: String!
  description: String
  image: String
}
```

# Push Changes

```bash
amplify push --y
```