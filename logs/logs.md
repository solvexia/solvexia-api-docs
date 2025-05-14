# Log APIs

[Get list of logs](#get-list-of-logs)  

---

## Get list of logs

Retrieves all logs accessible to the authenticated user. The caller may provide optional filters to refine the results. If no filters are provided, the latest 50 logs will be returned.

```apacheconfig
GET /api/v1/logs
```

#### Path parameters

This request does not have any path parameters.

#### Query parameters

| Name | Type |Description |
| ------------- |------------- | -------------|
|startDate|`string`|Filters logs to return only those with a `timeStamp` later than this value.  |
|endDate|`string`|Filters logs to return only those with a `timeStamp` earlier than this value. |

#### Request body
The request body must be empty.

#### Response

The successful response contains an array of instances of [Log List Item](./logs_schemas.md/#log-list-item).

The error response contains an [Error](../response_codes.md).

### Example

Request

```shell
curl https://app.solvexia.com/api/v1/logs -X GET -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

With query parameters

```shell
curl https://app.solvexia.com/api/v1/logs?startDate=2025-02-20T00:28:10.677Z -X GET -H "Authorization: Bearer syPHeMY5H--kdRtfpoXTgYFF7LHgVOhIjOQ5QkIvSD68VZvc2_uAew.P07tEVThD5SqNCV_tFwbAg"
```

Response

```json
[
    {
        "id": "n_sbzZYBi9W5689HT5uJ",
        "message": "Scheduled process run \"Test analytics 2 : run #5886\" has completed in 1 s with status \"Finished\" at 02/21/2025 04:44:00 for User \"template.mona.benson\"",
        "userName": "template.mona.benson",
        "timeStamp": "2025-05-21T14:44:00.7283212+10:00"
    },
    {
        "id": "nPsbzZYBi9W5689HT5uJ",
        "message": "Process run \"Test analytics : run #5888\" has completed in 2 s with status \"Finished\" at 02/20/2025 04:44:00 for User \"template.mona.benson\"",
        "userName": "template.mona.benson",
        "timeStamp": "2025-02-20T14:44:00.6578787+10:00"
    }
]
```
---

