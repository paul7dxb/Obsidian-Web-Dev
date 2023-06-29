# Query DynamoDB With Lambda

If your DynamoDB table has a partition key attribute called "customerId" and a sort key attribute called "bookingRef", here's an example of how a query using these keys would look:

```javascript
const queryParams = {
  TableName: tableName,
  IndexName: "exampleIndex",
  KeyConditionExpression: "customerId = :cid",
  ExpressionAttributeValues: {
    ":cid": "exampleCustomerId"
  }
};

body = await dynamo.query(queryParams).promise();
```

In this example, the query is based on the partition key "customerId". The `KeyConditionExpression` specifies the condition for the partition key attribute, and the `ExpressionAttributeValues` maps the placeholder `:cid` to the specific customer ID value you want to query.

You can also include a condition on the sort key attribute "bookingRef" by appending it to the `KeyConditionExpression`. For example, if you want to retrieve items for a specific customer ID and a specific booking reference, you can modify the query as follows:

```javascript
const queryParams = {
  TableName: tableName,
  IndexName: "exampleIndex",
  KeyConditionExpression: "customerId = :cid AND bookingRef = :ref",
  ExpressionAttributeValues: {
    ":cid": "exampleCustomerId",
    ":ref": "exampleBookingRef"
  }
};

body = await dynamo.query(queryParams).promise();
```

Ensure that you replace "exampleCustomerId" and "exampleBookingRef" with the actual values you want to query.