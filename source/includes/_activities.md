# Activities

## Get Team Information

```shell
curl https://app.lemlist.com/api/activities \
  --user ":YourApiKey"
```

> The above command returns JSON structured like this:

```json
[{
  "_id": "act_aaXiFy3Y7BNSuYwDr",
  "isFirst": true,
  "type": "emailsSent",
  "teamId": "tea_aaqam5a3BkY8zje24",
  "createdAt": "2018-08-24T14:56:39.172Z",
  "sendUserId": "usr_aawMB5Gd5JJCFYvjp",
  "sendUserEmail": "richard@piedpiper.com",
  "sendUserName": "Richard Hendricks",
  "leadId": "lea_aafF6i3BjsDRDNAWN",
  "leadFirstName": "Jeanne",
  "leadLastName": "Doe",
  "leadEmail": "jeanne@doe.com",
  "campaignId": "cam_aaktcZg9z9xJKQgqK",
  "campaignName": "Campaign1",
  "listId": "lst_aa5tgpggEfYeJ9vbJ",
  "sequenceId": "seq_aaPoZgbALLQhcLmqz",
  "sequenceStep": 2,
  "emailTemplateId": "etp_aatuEkEztDPm32b23",
  "emailTemplateName": "Sales: The Honest One",
  "emailId": "eml_aaFHxT2ejiz7apYnn"
},{
  "_id": "act_aavmrPCCZGMSsCSNw",
  "isFirst": true,
  "type": "emailsSent",
  "teamId": "tea_aqam5a3BkY8zje24",
  "createdAt": "2018-08-24T14:51:35.726Z",
  "sendUserId": "usr_aawMB5Gd5JJCFYvjp",
  "sendUserEmail": "richard@piedpiper.com",
  "sendUserName": "Richard Hendricks",
  "leadId": "lea_aafF6i3BjsDRDNAWN",
  "leadFirstName": "Jeanne",
  "leadLastName": "Doe",
  "leadEmail": "jeanne",
  "campaignId": "cam_aaktcZg9z9xJKQgqK",
  "campaignName": "Campaign1",
  "listId": "lst_aa5tgpggEfYeJ9vbJ",
  "sequenceId": "seq_aaPoZgbALLQhcLmqz",
  "sequenceStep": 1,
  "emailTemplateId": "etp_aak9yNgefLCCB7ghA",
  "emailTemplateName": "I Just Call",
  "emailId": "eml_aabhRvzfe9sFErQ2b"
}]
```

This endpoint retrieves the last 100 activities.

### HTTP Request

`GET https://app.lemlist.com/api/activities`

### Query Parameters

Parameter | Description
--------- | -----------
type | (Optional) The type of activity you want to retrieve. Can be `emailsSent`, `emailsOpened`, `emailsClicked`, `emailsReplied`, `emailsBounced`, `emailsSendFailed`, `emailsUnsubscribed`.
campaignId | (Optional) Retrieve activities of this `campaignId`.
isFirst | (Optional) Only retrieve the first time this activity happened.
