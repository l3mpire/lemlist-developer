# Activities

## Get Activities

```shell
curl https://api.lemlist.com/api/activities \
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
  "emailId": "eml_aabhRvzfe9sFErQ2b",
  "sequenceTested": "A",
  "stepTested": "A"
}]
```

This endpoint retrieves the last 100 activities.

### HTTP Request

`GET https://api.lemlist.com/api/activities`

### Query Parameters

Parameter | Description
--------- | -----------
type | (Optional) The type of activity you want to retrieve. Can be `aircallCreated`, `aircallDone`, `aircallEnded`, `aircallInterested`, `aircallNotInterested`, `annotated`, `apiDone`, `apiFailed`, `apiInterested`, `apiNotInterested`, `apiUnsubscribed`, `conditionChosen`, `emailsBounced`, `emailsClicked`, `emailsDone`, `emailsFailed`, `emailsInterested`, `emailsNotInterested`, `emailsOpened`, `emailsReplied`, `emailsSent`, `emailsUnsubscribed`, `linkedinDone`, `linkedinDone`, `linkedinInterested`, `linkedinInviteAccepted`, `linkedinInviteDone`, `linkedinInviteFailed`, `linkedinNotInterested`, `linkedinOpened`, `linkedinReplied`, `linkedinSendFailed`, `linkedinSent`, `linkedinVisitFailed`, `linkedinVoiceNoteDone`, `linkedinVoiceNoteFailed`, `manualDone`, `manualInterested`, `manualNotInterested`, `meetingBooked`, `paused`, `resumed`, `sendToAnotherCampaign`, `skipped`, `snoozed`, `contacted`, `hooked`, `attracted`, `warmed`, `interested`, `notInterested`. You can retrieve the documentation of the `type` parameter here: <a href="https://help.lemlist.com/en/articles/9423940-api-get-activities-list-of-activities-type" target="_blank">Activity Types</a>.
campaignId | (Optional) Retrieve activities of this `campaignId`.
isFirst | (Optional) Only retrieve the first time this activity happened.
offset | (Optional) Offset from the start. For pagination.
limit | (Optional) Number of campaigns to retrieve. 100 per default ( and 100 max ).
