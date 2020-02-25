# Team

## Get Team Information

```shell
curl https://api.lemlist.com/api/team \
  --user ":YourApiKey"
```

> The above command returns JSON structured like this:

```json
{
  "_id": "tea_aaqam5a3BkY8aje24",
  "name": "PiedPiper",
  "userIds": ["usr_aawMB5Gd5JJCFYvjp"],
  "createdBy": "usr_aawMB5Gd5JJCFYvjp",
  "createdAt": "2018-04-30T12:19:42.829Z",
  "apiKey": "aa13722b45b9c475cc686231b1af6583",
  "billing": {
    "quantity": 1,
    "ok": true,
    "plan": "freetrial"
  },
}
```

This endpoint retrieves information of your team.

### HTTP Request

`GET https://api.lemlist.com/api/team`

### Query Parameters

No parameters.
