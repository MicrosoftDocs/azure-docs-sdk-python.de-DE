---
title: "Azure Event Grid-Bibliotheken für Python"
description: 
keywords: Azure, Python, SDK, API, Event Grid
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 08/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: event-grid
ms.openlocfilehash: a50a203a0733f25f2a88d6f4a43c6bddc388d3e7
ms.sourcegitcommit: 79afc8a1b427e26ecea7bdc0b7b3c898f143360f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2017
---
# <a name="event-grid-libraries-for-python"></a><span data-ttu-id="ac5c1-103">Event Grid-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="ac5c1-103">Event Grid libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="ac5c1-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="ac5c1-104">Overview</span></span>
<span data-ttu-id="ac5c1-105">Azure Event Grid ist ein vollständig verwalteter intelligenter Dienst für das Ereignisrouting, der eine einheitliche Ereignisnutzung mithilfe eines Veröffentlichen/Abonnieren-Modells ermöglicht.</span><span class="sxs-lookup"><span data-stu-id="ac5c1-105">Azure Event Grid is a fully-managed intelligent event routing service that allows for uniform event consumption using a publish-subscribe model.</span></span>

## <a name="management-api"></a><span data-ttu-id="ac5c1-106">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="ac5c1-106">Management API</span></span>
```bash
pip install azure-mgmt-eventgrid
```

### <a name="example"></a><span data-ttu-id="ac5c1-107">Beispiel</span><span class="sxs-lookup"><span data-stu-id="ac5c1-107">Example</span></span>
<span data-ttu-id="ac5c1-108">Mit dem folgenden Beispiel wird ein benutzerdefiniertes Thema erstellt, das Thema abonniert und das Ereignis ausgelöst, um das Ergebnis anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="ac5c1-108">The following creates a custom topic, subscribes to the topic, and triggers the event to view the result.</span></span> <span data-ttu-id="ac5c1-109">RequestBin ist ein Open Source-Drittanbietertool, mit dem Sie einen Endpunkt erstellen und Anforderungen anzeigen können, die an ihn gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="ac5c1-109">RequestBin is an open source, third-party tool that enables you to create an endpoint, and view requests that are sent to it.</span></span> <span data-ttu-id="ac5c1-110">Wechseln Sie zu [RequestBin](https://requestb.in/), und klicken Sie auf **Create a RequestBin** (RequestBin erstellen).</span><span class="sxs-lookup"><span data-stu-id="ac5c1-110">Go to [RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span> <span data-ttu-id="ac5c1-111">Kopieren Sie die Bin-URL. Sie wird zum Abonnieren des Themas benötigt.</span><span class="sxs-lookup"><span data-stu-id="ac5c1-111">Copy the bin URL, because you need it when subscribing to the topic.</span></span>

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
<span data-ttu-id="ac5c1-112">Navigieren Sie zu der zuvor erstellten RequestBin-URL, um das eben gesendete Ereignis anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="ac5c1-112">Browse to the RequestBin URL created earlier to see the event just sent.</span></span>

<span data-ttu-id="ac5c1-113">Bereinigen von Ressourcen</span><span class="sxs-lookup"><span data-stu-id="ac5c1-113">Clean up resources</span></span>
```azurecli-interactive
az group delete --name gridResourceGroup
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="ac5c1-114">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="ac5c1-114">Explore the Management APIs</span></span>](/python/api/overview/azure/eventgrid/managementlibrary)

