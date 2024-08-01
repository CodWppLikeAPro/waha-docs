---
title: "🏷️ Labels"
description: "Labels (available in WhatsApp Business)"
lead: ""
date: 2020-10-06T08:48:45+00:00
lastmod: 2020-10-06T08:48:45+00:00
draft: false
images: [ ]
weight: 292
---

You can work with [WhatsApp Labels](https://faq.whatsapp.com/3398508707096369/?cms_platform=android)
available in WhatsApp Business using the API!
![](whatsapp-labels.png)

## Features

Here's the list of features that are available by [**🏭 Engines**]({{< relref "/docs/how-to/engines" >}}):

{{< include file="content/en/docs/how-to/labels/features.md" >}}

## Endpoints

### Get list of labels

You can get a list of labels for the session using the endpoint:

```bash
GET /api/{session}/labels
```

Response:

```json

[
  {
    "id": "1",
    "name": "New Client",
    "color": 1,
    "colorHex": "#64c4ff"
  },
  ...
]
```

### Get chats by label id

You can get a list of chats by label id using the endpoint:

```bash
GET /api/{session}/labels/{labelId}/chats
```

ℹ️ Response right now depends on
[**🏭 Engine**]({{< relref "/docs/how-to/engines" >}})
you're using,
the same way as
[**💬 Chats**]({{< relref "/docs/how-to/chats" >}})

### Get labels by chat id

You can get a list of labels by chat id using the endpoint:

```bash
GET /api/{session}/labels/chats/{chatId}/
```

Response:

```json
[
  {
    "id": "1",
    "name": "New Client",
    "color": 1,
    "colorHex": "#64c4ff"
  },
  ...
]
```

### Update labels to chat

```bash
PUT /api/{session}/labels/chats/{chatId}/
```

**Upsert label**:

👉 You need to provide **the full list of labels** you want to set to the chat. All other labels will be removed.

```json
{
  "labels": [
    {
      "id": "1"
    }
  ]
}
```

**Remove labels**:

```json
{
  "labels": []
}

```

## Webhooks

### labels.upsert

```json
{
  "event": "label.upsert",
  "session": "default",
  "payload": {
    "id": "10",
    "name": "Label Name",
    "color": 14,
    "colorHex": "#00a0f2"
  },
  "engine": "NOWEB",
  ...
}

```

### labels.removed

```json
{
  "event": "label.removed",
  "session": "default",
  "payload": {
    "id": "10",
    "name": "",
    "color": 14,
    "colorHex": "#00a0f2"
  },
  "engine": "NOWEB",
  ...
}

```

### labels.chat.added

```json
{
  "event": "label.chat.added",
  "session": "default",
  "payload": {
    "labelId": "6",
    "chatId": "11111111111@c.us",
    "label": null <=== right after scanning QR it can be null. 
  },
  "engine": "NOWEB",
  ...
}
```

### labels.chat.removed

```json
{
  "event": "label.chat.removed",
  "session": "default",
  "payload": {
    "labelId": "6",
    "chatId": "11111111111@c.us",
    "label": null
  },
  "engine": "NOWEB",
  ...
}
```
