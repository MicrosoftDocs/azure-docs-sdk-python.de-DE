---
title: Azure Event Grid-Bibliotheken für Python
description: ''
keywords: Azure, Python, SDK, API, Event Grid
author: lisawong19
ms.author: routlaw
manager: routlaw
ms.date: 08/21/2017
ms.topic: article
ms.devlang: python
ms.service: event-grid
ms.openlocfilehash: e5df1078116f13f959923eac3e0c7b5789545278
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534295"
---
# <a name="event-grid-libraries-for-python"></a>Event Grid-Bibliotheken für Python


Azure Event Grid ist ein vollständig verwalteter intelligenter Dienst für das Ereignisrouting, der eine einheitliche Ereignisnutzung mithilfe eines Veröffentlichen/Abonnieren-Modells ermöglicht.

[Weitere Informationen](/azure/event-grid/overview) zu Azure Event Grid und erste Schritte mit dem [Tutorial zu Azure Blob Storage-Ereignissen](/azure/storage/blobs/storage-blob-event-quickstart) 

## <a name="publish-sdk"></a>Veröffentlichungs-SDK

Mit dem Veröffentlichungs-SDK von Azure Event Grid können Sie Ereignisse authentifizieren, erstellen, verarbeiten und in Themen veröffentlichen.

### <a name="installation"></a>Installation 

Installieren Sie das Paket mithilfe von [pip](https://pip.pypa.io/en/stable/quickstart/).

```bash
pip install azure-eventgrid
```

### <a name="example"></a>Beispiel 

Der folgende Code veröffentlicht ein Ereignis in einem Thema. Sie können den Schlüssel und Endpunkt des Themas über das Azure-Portal oder die Azure-Befehlszeilenschnittstelle abrufen:

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

```python
from datetime import datetime
from azure.eventgrid import EventGridClient
from msrest.authentication import TopicCredentials

def publish_event(self):

        credentials = TopicCredentials(
            self.settings.EVENT_GRID_KEY
        )
        event_grid_client = EventGridClient(credentials)
        event_grid_client.publish_events(
            "your-endpoint-here",
            events=[{
                'id' : "dbf93d79-3859-4cac-8055-51e3b6b54bea",
                'subject' : "Sample subject",
                'data': {
                    'key': 'Sample Data'
                },
                'event_type': 'SampleEventType',
                'event_time': datetime(2018, 5, 2),
                'data_version': 1
            }]
        )
```

> [!div class="nextstepaction"]
> [Informationen zu den Client-APIs](/python/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a>Verwaltungs-SDK

Das Verwaltungs-SDK ermöglicht Ihnen das Erstellen, Aktualisieren und Löschen von Event Grid-Instanzen, -Themen und -Abonnements.

### <a name="installation"></a>Installation 

Installieren Sie das Paket mithilfe von [pip](https://pip.pypa.io/en/stable/quickstart/).

```bash
pip install azure-mgmt-eventgrid
```

### <a name="example"></a>Beispiel

Der folgende Code erstellt ein benutzerdefiniertes Thema und abonniert einen Endpunkt für das Thema. Der Code sendet anschließend über HTTPS ein Ereignis an das Thema.
RequestBin ist ein Open Source-Drittanbietertool, mit dem Sie einen Endpunkt erstellen und Anforderungen anzeigen können, die an ihn gesendet werden. Wechseln Sie zu [RequestBin](https://requestbin.com), und klicken Sie auf **Create a RequestBin** (RequestBin erstellen). Kopieren Sie die Bin-URL. Sie wird zum Abonnieren des Themas benötigt.

```python
from azure.mgmt.resource import ResourceManagementClient
from azure.mgmt.eventgrid import EventGridManagementClient
import requests

RESOURCE_GROUP_NAME = 'gridResourceGroup'
TOPIC_NAME = 'gridTopic1234'
LOCATION = 'westus2'
SUBSCRIPTION_ID = 'YOUR_SUBSCRIPTION_ID'
SUBSCRIPTION_NAME = 'gridSubscription'
REQUEST_BIN_URL = 'YOUR_REQUEST_BIN_URL'

# create resource group
resource_client = ResourceManagementClient(credentials, SUBSCRIPTION_ID)
resource_client.resource_groups.create_or_update(
    RESOURCE_GROUP_NAME,
    {
        'location': LOCATION
    }
)

event_client = EventGridManagementClient(credentials, SUBSCRIPTION_ID)

# create a custom topic
event_client.topics.create_or_update(RESOURCE_GROUP_NAME, TOPIC_NAME, LOCATION)

# subscribe to a topic
scope = '/subscriptions/'+SUBSCRIPTION_ID+'/resourceGroups/'+RESOURCE_GROUP_NAME+'/providers/Microsoft.EventGrid/topics/'+TOPIC_NAME
event_client.event_subscriptions.create(scope, SUBSCRIPTION_NAME,
    {
        'destination': {
            'endpoint_url': REQUEST_BIN_URL
        }
    }
)

# send an event to topic
# get endpoint url
url = event_client.event_subscriptions.get_full_url(scope, SUBSCRIPTION_NAME).endpoint_url
# get key
key = event_client.topics.list_shared_access_keys(RESOURCE_GROUP_NAME,TOPIC_NAME).key1
headers = {'aeg-sas-key': key}
s = requests.get('https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json')
r = requests.post(url, data=s, headers=headers)
print(r.status_code)
print(r.content)
```
Navigieren Sie zu der zuvor erstellten RequestBin-URL, um das eben gesendete Ereignis anzuzeigen.

Bereinigen von Ressourcen
```azurecli-interactive
az group delete --name gridResourceGroup
```

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/eventgrid/management)

## <a name="learn-more"></a>Weitere Informationen

[Receive events using the Event Grid SDK](/azure/event-grid/receive-events) (Empfangen von Ereignissen mithilfe des Event Grid SDK)
