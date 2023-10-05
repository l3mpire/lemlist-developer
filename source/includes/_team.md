# Team

## Get Team Information

```shell
curl https://api.lemlist.com/api/team \
  --user ":YourApiKey"
```

> The above command returns JSON structured like this:

```json
{
  "_id": "tea_ZSC4DkNwPGMe7rMJi",
  "name": "My team",
  "userIds": [
    "usr_WhvZ6kTGMcDkg7iH9",
    "usr_5AJZjmsDGTwvjvbt7"
  ],
  "createdBy": "usr_WhvZ6kTGMcDkg7iH9",
  "createdAt": "2023-02-07T15:13:40.668Z",
  "beta": [],
  "invitedUsers": [
    {
      "email": "new.user@my-domain.com",
      "role": "member",
      "invitedBy": "usr_WhvZ6kTGMcDkg7iH9",
      "invitedAt": "2023-02-17T10:36:42.279Z"
    }
  ],
  "customDomain": "my-domain.com"
}
```

This endpoint retrieves information of your team.

### HTTP Request

`GET https://api.lemlist.com/api/team`

### Query Parameters

No parameters.
