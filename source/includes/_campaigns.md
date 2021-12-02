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
  "name": "Campaign1",
  "labels": ["label 1", "label 2"]
}, {
  "_id": "cam_aaXwBiebA8pWPKqpK",
  "name": "Campaign2"
}]
```

This endpoint retrieves the list of all campaigns.

### HTTP Request

`GET https://api.lemlist.com/api/campaigns`

### Query Parameters

Parameter | Description
--------- | -----------
offset | (Optional) Offset from the start. For pagination.
limit | (Optional) Number of campaigns to retrieve. 100 per default ( and 100 max ).


## Start Export of a Campaign

```shell
curl https://api.lemlist.com/api/campaigns/cam_123456/export/start \
  --user ":YourApiKey"
```
> The above command returns an export ID for the campaign `cam_123456`


```shell
{
  "ok": true,
  "status": {
    "exportId": "exp_123456",
    "teamId": "team_123456",
    "campaignId": "cam_123456",
    "status": "pending",
    "startedAt": "2020-01-01T00:00:00.000Z"
  }
}
```

> returned object in case of success, note the `exportId` property

```shell
{
  "ok": false,
  "message": "An error occurred"
}
```

> returned object in case of failure


This endpoint start an asynchronous export of all the statistics of a campaign. The final export result is a CSV file.

You first start an export, get an export ID, and then periodically check the status of the export with the /status endpoint. You should stop as soon as you have a status that is different than "pending".

It is "export ID based" and not "campaign ID based" so multiple exports on the same campaign can be done (let's say one started by a user in the application and another by a script).

### HTTP Request

`GET https://api.lemlist.com/api/campaigns/:campaignId/export/start`

### URL Parameters

Parameter | Description
--------- | -----------
campaignId | The ID of the campaign to export.

## Get status of a campaign export

```shell
curl https://api.lemlist.com/api/campaigns/cam_123456/export/exp_123456/status \
  --user ":YourApiKey"
```
> The above command returns the status of a export


```shell
{
  "ok": true,
  "status": {
    "exportId": "exp_123456",
    "teamId": "team_123456",
    "campaignId": "cam_123456",
    "status": "done",
    "startedAt": "2020-01-01T00:00:00.000Z"
    "endedAt": "2020-01-01T00:00:00.000Z"
    "url": "https://api.lemlist.com/api/files/exports/fil_exp_my_campaign.csv"
  }
}
```

> returned object in case of success, note the `status` and `url` properties


This endpoint checks the status of an asynchronous export.

campaignId and exportId are required.

In the returned object :

* `status` can be "pending", "done", or "error".
* `url` gives the final CSV file URL (only if the status is "done").

### Expiration time

Status are available for 2h only. An export that is still pending after 2h will be considered as failed and HTTP request statusCode will be 404.
When you obtain the CSV file URL, you have to download the file in a 24 hours time frame. After that, the file will be deleted.


### HTTP Request

`GET https://api.lemlist.com/api/campaigns/:campaignId/export/:exportId/status`

### URL Parameters

Parameter | Description
--------- | -----------
campaignId | The ID of the campaign that was exported with the /start endpoint.
exportId | The ID of the export that was returned by the /start endpoint.


## Synchronously Export Statistics of a Campaign <span style="color:red">(DEPRECATED)</span>

```shell
curl https://api.lemlist.com/api/campaigns/cam_123456/export \
  --user ":YourApiKey"
```

> The above command returns the CSV file for the campaign `cam_123456`

This endpoint downloads a CSV file that contains all the statistics of a campaign.

This synchronous endpoint is DEPRECATED since Dec, 3rd 2021 and will be removed in a future version. Please use the /start asynchronous endpoint instead.

### HTTP Request

`GET https://api.lemlist.com/api/campaigns/:campaignId/export`

### URL Parameters

Parameter | Description
--------- | -----------
campaignId | The ID of the campaign to retrieve.


## Export Leads of a Campaign

```shell
curl https://api.lemlist.com/api/campaigns/cam_123456/export/list?state=all \
  --user ":YourApiKey"
```

> The above command returns the CSV file for the campaign `cam_123456`

This endpoint downloads a CSV file that contains all the leads of a campaign.

### HTTP Request

`GET https://api.lemlist.com/api/campaigns/:campaignId/export/list?state=all`  

### URL Parameters

Parameter | Description
--------- | -----------
campaignId | The ID of the campaign to retrieve.

### Query Parameters

Parameter | Description
--------- | -----------
state=all | Filter to export only the specified states, all will export all states. Possible states are imported, scanned, skipped, reviewed, contacted, hooked, attracted, warmed, notInterested, interested, emailsBounced, failed, emailsUnsubscribed

State | Description
----- | -----------
imported | All the leads that were imported without any other processing (not scanned, no step sent, not reviewed...)
scanned | All the leads that were scanned by linkedIn, or dropcontact
skipped | All the leads that were skipped during review
reviewed | All the leads that were reviewed
contacted | All the leads that were contacted (a step was done for this lead, without any response or click yet)
hooked | All the leads that opened an email or linkedIn
attracted | All the leads that clicked in an email, accepted a linkedIn invite 
warmed | All the leads that replied to an email, or a linkedIn
notInterested | All the leads that were mark as notInterested
interested | All the leads that were mark as interested
emailsBounced | All the leads where at least one step bounced, either an email or a linkedIn or an api call
emailsUnsubscribed | All the leads that were an unsubscribe
failed | Deprecated, use emailsBounced

## Add a Lead in a Campaign

```shell
curl -X POST https://api.lemlist.com/api/campaigns/cam_aa7uvyxECcni5KXBM/leads/richard@piedpiper.com \
  -H "Content-Type: application/json" \
  --data '{"firstName":"Richard","lastName":"Hendricks","companyName":"Piedpiper","icebreaker":"Icebreaker text",\
  "phone":"(555) 555-1234","picture":"https://piedpiper.com/richard-hendricks.jpg",\
  "linkedinUrl":"https://www.linkedin.com/in/richard-hendricks/"}' \
  --user ":YourApiKey"
```

> The above command returns JSON structured like this:

```json
{
  "campaignId": "cam_aa7uvyxECcni5KXBM",
  "campaignName": "Campaign1",
  "leadUrl":"https://api.lemlist.com/api/leads/richard%40piedpiper.com",
  "_id":"lea_aaNfSAHJoa4gj86Px",
  "isPaused":false,
  "email":"richard@piedpiper.com",
  "firstName":"Richard",
  "lastName":"Hendricks",
  "companyName":"Piedpiper",
  "icebreaker":"Icebreaker text",
  "phone":"(555) 555-1234",
  "picture":"https://piedpiper.com/richard-hendricks.jpg",
  "linkedinUrl":"https://www.linkedin.com/in/richard-hendricks/"
}
```

This endpoint adds a lead in a specific campaign. If the lead doesn't exist, it'll be created, then inserted to the campaign. The creator of the lead is the campaign's sender

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
  --data '{"firstName":"Richard","lastName":"Hendricks","companyName":"Piedpiper","icebreaker":"Icebreaker text",\
  "phone":"(555) 555-1234","picture":"https://piedpiper.com/richard-hendricks.jpg",\
  "linkedinUrl":"https://www.linkedin.com/in/richard-hendricks/"}' \
  --user ":YourApiKey"
```

> The above command returns JSON structured like this:

```json
{
  "campaignId": "cam_aa7uvyxECcni5KXBM",
  "campaignName": "Campaign1",
  "leadUrl":"https://api.lemlist.com/api/leads/richard%40piedpiper.com",
  "_id":"lea_aaNfSAHJoa4gj86Px",
  "isPaused":false,
  "email":"richard@piedpiper.com",
  "firstName":"Richard",
  "lastName":"Hendricks",
  "companyName":"Piedpiper",
  "icebreaker":"Icebreaker text",
  "phone":"(555) 555-1234",
  "picture":"https://piedpiper.com/richard-hendricks.jpg",
  "linkedinUrl":"https://www.linkedin.com/in/richard-hendricks/"
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
icebreaker | Icebreaker text of the lead.
phone | Phone number of the lead.
picture | Picture url of the lead.
linkedinUrl | Linkedin url of the lead.
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

If no body is specified a 400 error will be returned.

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

This endpoint will unsubscribe a lead from all campaigns if he belongs to the specified campaign.


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
