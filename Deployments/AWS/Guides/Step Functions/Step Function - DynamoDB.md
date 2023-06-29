# DeleteItem

- Delete an item that has a specific primary key and sort key when the value of "bookingStatus" is set to reserved
- "Status" cannot be used as it is a reserved word

```JSON
{
  "TableName": "tutReactTable",
  "Key": {
    "customerId": {
      "S.$": "$.Payload.customerID"
    },
    "bookingRef": {
      "S.$": "$.bookingRef.bookingRef"
    }
  },
  "ConditionExpression": "attribute_exists(bookingStatus) AND bookingStatus = :bookingStatusValue",
  "ExpressionAttributeValues": {
    ":bookingStatusValue": {
      "S": "Reserved"
    }
  }
}
```