# DynamoDB CLI

```bash
# Demo Projection Expression (choose items to get back)
aws dynamodb scan --table-name UserPosts --projection-expression "user_id, content"

# Demo Filter Expression
aws dynamodb scan --table-name UserPosts --filter-expression "user_id = :u" --expression-attribute-values '{ ":u": {"S":"john123"}}'

# Page Size demo: will do 1 API call if you have 3 Items
aws dynamodb scan --table-name UserPosts 

# Will do 3 API calls if you have 3 Items. Still get all items returned work is done behind the scenes
aws dynamodb scan --table-name UserPosts --page-size 1

# Max Item demo:
aws dynamodb scan --table-name UserPosts --max-items 1

# Fetch the next item
aws dynamodb scan --table-name UserPosts --max-items 1 --starting-token eyJFeGNsdXNpdmVTdGFydEtleSI6IG51bGwsICJib3RvX3RydW5jYXRlX2Ftb3VudCI6IDF9

# Fetch the next item
aws dynamodb scan --table-name UserPosts --max-items 1 --starting-token eyJFeGNsdXNpdmVTdGFydEtleSI6IG51bGwsICJib3RvX3RydW5jYXRlX2Ftb3VudCI6IDJ9
```