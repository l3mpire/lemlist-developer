# Campaigns

## List All Campaigns

```shell
curl https://api.lemlist.com/api/campaigns \
  --user ":YourApiKey"
```

> The above command returns JSON structured like this:

```json
[{
  "_id": "cam_aaWL92T22Sei3Bz6v",
  "name": "Campaign1"
}, {
  "_id": "cam_aaXwBiebA8pWPKqpK",
  "name": "Campaign2"
}]
```

This endpoint retrieves the list of all campaigns.

### HTTP Request

`GET https://api.lemlist.com/api/campaigns`

### Query Parameters

No parameters.


## Export Statistics of a Campaign

```shell
curl https://api.lemlist.com/api/campaigns/cam_123456/export \
  --user ":YourApiKey"
```

> The above command returns the CSV file for the campaign `cam_123456`

This endpoint downloads a CSV file that contains all the statistics of a campaign.

### HTTP Request

`GET https://api.lemlist.com/api/campaigns/:campaignId/export`

### URL Parameters

Parameter | Description
--------- | -----------
campaignId | The ID of the campaign to retrieve.


## Export Leads of a Campaign

```shell
curl https://api.lemlist.com/api/campaigns/cam_123456/export/list \
  --user ":YourApiKey"
```

> The above command returns the CSV file for the campaign `cam_123456`

This endpoint downloads a CSV file that contains all the leads of a campaign.

### HTTP Request

`GET https://api.lemlist.com/api/campaigns/:campaignId/export`

### URL Parameters

Parameter | Description
--------- | -----------
campaignId | The ID of the campaign to retrieve.


## Add a Lead in a Campaign

```shell
curl -X POST https://api.lemlist.com/api/campaigns/cam_aa7uvyxECcni5KXBM/leads/richard@piedpiper.com \
  -H "Content-Type: application/json" \
  --data '{"firstName":"Richard","lastName":"Hendricks"}' \
  --user ":YourApiKey"
```

> The above command returns JSON structured like this:

```json
{
  "campaignId": "cam_aa7uvyxECcni5KXBM",
  "campaignName": "Campaign1",
  "leadUrl":"https://api.lemlist.com/api/leads/richard%40piedpiper.com",
  "_id":"lea_aaNfSAHJoa4gj86Px",
  "email":"richard@piedpiper.com",
  "firstName":"Richard",
  "lastName":"Hendricks"
}
```

This endpoint adds a lead in a specific campaign. If the lead doesn't exist, it'll be created, then inserted to the campaign.

You can just add the email without any body.

### HTTP Request

`POST https://api.lemlist.com/api/campaigns/:campaignId/leads/:email`

### URL Parameters

Parameter | Description
--------- | -----------
campaignId | The ID of the campaign to add the lead.
email | email address of the lead


### Query Parameters

```shell
curl POST "https://api.lemlist.com/api/campaigns/cam_aa7uvyxECcni5KXBM/leads/richard@piedpiper.com?deduplicate=true" \
  -H "Content-Type: application/json" \
  --data '{"firstName":"Richard","lastName":"Hendricks"}' \
  --user ":YourApiKey"
```

> The above command returns JSON structured like this:

```json
{
  "campaignId": "cam_aa7uvyxECcni5KXBM",
  "campaignName": "Campaign1",
  "leadUrl":"https://api.lemlist.com/api/leads/richard%40piedpiper.com",
  "_id":"lea_aaNfSAHJoa4gj86Px",
  "email":"richard@piedpiper.com",
  "firstName":"Richard",
  "lastName":"Hendricks"
}
```

Parameter | Description
--------- | -----------
deduplicate=true | search email address in another campaign, will not insert the lead if email address already inserted  


### Body Parameters

Body is optional. If set, it must be a JSON object with any information you want to add to the lead.

There's some optional predefined key:

Parameter | Description
--------- | -----------
firstName | First name of the lead.
lastName | Last name of the lead.
companyName | Company name of the lead.

## Update a Lead in a Campaign
```shell
curl -X PATCH https://api.lemlist.com/api/campaigns/cam_aa7uvyxECcni5KXBM/leads/richard@piedpiper.com \
  -H "Content-Type: application/json" \
  --data '{"companyName":"Pied Piper"}' \
  --user ":YourApiKey"
```

> The above command returns JSON structured like this:

```json
{
  "campaignId": "cam_aa7uvyxECcni5KXBM",
  "campaignName": "Campaign1",
  "leadUrl":"https://api.lemlist.com/api/leads/richard%40piedpiper.com",
  "_id":"lea_aaNfSAHJoa4gj86Px",
  "email":"richard@piedpiper.com",
  "firstName":"Richard",
  "lastName":"Hendricks",
  "companyName": "Pied Piper"
}
```

This endpoint updates a lead in a specific campaign.

If the lead doesn't exist a 404 error will be returned.

### HTTP Request

`PATCH https://api.lemlist.com/api/campaigns/:campaignId/leads/:email`

### URL Parameters

Parameter | Description
--------- | -----------
campaignId | The ID of the campaign to add the lead.
email | email address of the lead

### Body Parameters

Body is mandatory. It must be a JSON object with any information you want to update on the lead.

If no body is specified a 401 error will be returned.

## Unsubscribe a Lead from a Campaign

```shell
curl -X DELETE https://api.lemlist.com/api/campaigns/cam_aa7uvyxECcni5KXBM/leads/richard@piedpiper.com \
  --user ":YourApiKey"
```

> The above command returns JSON structured like this:

```json
{
  "_id": "lea_aaNfSAHJoa4gj86Px",
  "email": "richard@piedpiper.com"
}
```

This endpoint will unsuscribe a lead from a specific campaign.


### HTTP Request

`DELETE https://api.lemlist.com/api/campaigns/:campaignId/leads/:email`

### URL Parameters

Parameter | Description
--------- | -----------
campaignId | The ID of the campaign to add the lead.
email | email address of the lead
## Delete a Lead from a Campaign

```shell
curl -X DELETE https://api.lemlist.com/api/campaigns/cam_aa7uvyxECcni5KXBM/leads/richard@piedpiper.com?action=remove \
  --user ":YourApiKey"
```

> The above command returns JSON structured like this:

```json
{
  "_id": "lea_aaNfSAHJoa4gj86Px",
  "email": "richard@piedpiper.com"
}
```

This endpoint delete a lead from a specific campaign.  
All information, including statistics, will be deleted.

### HTTP Request

`DELETE https://api.lemlist.com/api/campaigns/:campaignId/leads/:email?action=remove`

### URL Parameters

Parameter | Description
--------- | -----------
campaignId | The ID of the campaign to add the lead.
email | email address of the lead
### Query Parameters

Parameter | Value | Description
--------- | ----- | -----------
action | remove | Force the deletion of the lead
