# Unsubscribes

## List All Unsubscribes

```shell
curl https://api.lemlist.com/api/unsubscribes \
  --user ":YourApiKey"
```

> The above command returns JSON structured like this:

```json
[{
  "_id": "lead_123456",
  "email": "a@a.com"
}, {
  "_id": "lead_123457",
  "email": "b@b.com"
}]
```

This endpoint retrieves the list of all people who are unsubscribed.

### HTTP Request

`GET https://api.lemlist.com/api/unsubscribes`

### Query Parameters

Parameter | Description
--------- | -----------
offset | (Optional) Offset from the start. For pagination.
limit | (Optional) Number of email to retrieve. 100 per default.


## Export the List of Unsubscribes

```shell
curl https://api.lemlist.com/api/unsubs/export \
  --user ":YourApiKey"
```

> The above command returns the CSV file with all unsubscribed email addresses

This endpoint downloads a CSV file that contains all the unsubscribed email addresses.

Result is not sorted.

### HTTP Request

`GET https://api.lemlist.com/api/unsubs/export`

### URL Parameters

No parameters.


## Add an Email Address or a Domain in the Unsubscribes

```shell
curl -X POST https://api.lemlist.com/api/unsubscribes/a@a.com \
  --user ":YourApiKey"
```

> The above command returns JSON structured like this:

```json
{
  "_id": "lea_aaJgm566c9tyzTBeu",
  "email": "a@a.com"
}
```

> If lead is already unsubscribed, returns JSON structured like this:

```json
{
  "_id": "lea_aaJgm566c9tyzTBeu",
  "email": "a@a.com",
  "alreadyUnsubscribed": true
}
```

> To unsubscribe the entire domain 'a.com'

```shell
curl -X POST https://api.lemlist.com/api/unsubscribes/@a.com \
  --user ":YourApiKey"
```

This endpoint adds a lead in the unsubscribed list.
Domain to unsubscribe must start with @, e.g. @a.com

### HTTP Request

`POST https://api.lemlist.com/api/unsubscribes/:email`

### URL Parameters

Parameter | Description
--------- | -----------
email or domain | email address to unsubscribe. If this is a domain, it must start with @


## Delete an Email Address from the Unsubscribes

```shell
curl -X DELETE https://api.lemlist.com/api/unsubscribes/a@a.com \
  --user ":YourApiKey"
```

> The above command returns JSON structured like this:

```json
{
  "_id": "lea_aaJgm566c9tyzTBeu",
  "email": "a@a.com"
}
```

This endpoint deletes a lead in the unsubscribed list.

### HTTP Request

`DELETE https://api.lemlist.com/api/unsubscribes/:email`

### URL Parameters

Parameter | Description
--------- | -----------
email | email address of the lead
