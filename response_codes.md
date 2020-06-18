# Response Codes   

The following Response codes can be returned from the Solvexia API'Solvexia

| Code | Type | Description |
| ------------- |------------- | ------------- |
| 200 | Ok | Successful Request |
| 400 | Bad Request | Requests input were invalid or malformed |
| 403 | Forbidden | The user does not have access to the resource or action |
| 404 | Not Found | The resource doesn't exist or has been deleted |
| 500 | Internal Server Error | An exception has occurred during processing the request |

## Error Response Body
All non-200 responses will return a general error json object

```javascript
{
    "message": "Supplied step id is not of type Data Step",
    "supportId": "cb4712e5-4eb9-40eb-acbb-091aaf740dca"
}

```

| Name | Type |Description |
| ------------- |------------- | -------------|
|message|`string`| Friendly error information.|
|supportId|`string`| Error Support id that can be given to Solvexia support for investigation.  |