# Hooks

Hooks are a way to for us to contact your server when an event occurs in lemlist. You can list, add or delete hooks.

## List All Hooks

```shell
curl https://api.lemlist.com/api/hooks \
  --user ":YourApiKey"
```

> The above command returns JSON structured like this:

```json
[{
  "_id": "hoo_aadabFv7dRoP2L8GJ",
  "targetUrl": "https://youserver.com/lemlist-hook",
  "createdAt": "2018-11-27T12:19:26.608Z"
}]
```

This endpoint retrieves the list of all hooks.

### HTTP Request

`GET https://api.lemlist.com/api/hooks`

### Query Parameters

No parameters.


## Add a Hook

```shell
curl -X POST https://api.lemlist.com/api/hooks \
  --data '{"targetUrl":"https://youserver.com/lemlist-hook"}' \
  --header "Content-Type: application/json" \
  --user ":YourApiKey"
```

> The above command returns JSON structured like this:

```json
{
  "_id": "hoo_aadabFv7dRoP2L8GJ",
  "targetUrl": "https://youserver.com/lemlist-hook",
  "createdAt": "2018-11-27T12:19:26.608Z"
}
```

This endpoint adds a hook in our system. Each time an event happen, we'll call `targetUrl` with the event data as an object. To know more about the data passed, see [activities](/#get-activities)

For mails sent through the composer, the `emailsSent` event is not fired

### HTTP Request

`POST https://api.lemlist.com/api/hooks`

### Body Parameters

Body is optional. If set, It must be a JSON object with one of those parameters.

Parameter | Description
--------- | -----------
type | (Optional) We'll call this hook only if the event is of the type `type`. `type` can be `contacted`, `hooked`, `attracted`, `warmed`, `interested`, `skipped`, `notInterested`, `emailsSent`, `emailsOpened`, `emailsClicked`, `emailsReplied`, `emailsBounced`, `emailsSendFailed`, `emailsFailed`, `emailsUnsubscribed`, `emailsInterested`, `emailsNotInterested`, `opportunitiesDone`, `aircallCreated`, `aircallEnded`, `aircallDone`, `aircallInterested`, `aircallNotInterested`, `apiDone`, `apiInterested`, `apiNotInterested`, `apiFailed`, `linkedinVisitDone`, `linkedinVisitFailed`, `linkedinInviteDone`, `linkedinInviteFailed`, `linkedinInviteAccepted`, `linkedinReplied`, `linkedinSent`, `linkedinInterested`, `linkedinNotInterested`, `linkedinSendFailed`, `manualInterested`, `manualNotInterested`, `paused`, `resumed`.
campaignId | (Optional) We'll call this hook only for this `campaignId`.
isFirst | (Optional) We'll call this hook only the first time this activity happened.


## Delete a Hook

```shell
curl -X DELETE https://api.lemlist.com/api/hooks/hoo_123456 \
  --user ":YourApiKey"
```

> The above command returns JSON structured like this:

```json
{
  "_id": "hoo_aadabFv7dRoP2L8GJ",
  "targetUrl": "https://youserver.com/lemlist-hook",
  "createdAt": "2018-11-27T12:19:26.608Z"
}
```

This endpoint delete a hook.

### HTTP Request

`DELETE https://api.lemlist.com/api/hooks/:_id`

### URL Parameters

Parameter | Description
--------- | -----------
_id | The ID of the hook that we have to remove.
