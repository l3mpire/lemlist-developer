# Leads

## Get a Specific Lead by Email

```shell
curl https://api.lemlist.com/api/leads/:email \
  --user ":YourApiKey"
```

> The above command returns JSON structured like this:

```json
{
  "_id":"lea_aaNfSAHJoa4gj86Px",
  "email":"richard@piedpiper.com",
  "firstName":"Richard",
  "lastName":"Hendricks"
}
```

This endpoint retrieves all the information of a specific lead using its email.

### HTTP Request

`GET https://api.lemlist.com/api/leads/:email`

### Query Parameters

Parameter | Description
--------- | -----------
email | email address of the lead.
