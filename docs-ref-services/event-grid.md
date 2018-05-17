---
title: Azure Event Grid-Bibliotheken für Python
description: ''
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
ms.openlocfilehash: e68504b3ba5834a145af1231eacc076e424a2256
ms.sourcegitcommit: 560362db0f65307c8b02b7b7ad8642b5c4aa6294
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/08/2018
---
# <a name="event-grid-libraries-for-python"></a><span data-ttu-id="7bc71-103">Event Grid-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="7bc71-103">Event Grid libraries for Python</span></span>


<span data-ttu-id="7bc71-104">Azure Event Grid ist ein vollständig verwalteter intelligenter Dienst für das Ereignisrouting, der eine einheitliche Ereignisnutzung mithilfe eines Veröffentlichen/Abonnieren-Modells ermöglicht.</span><span class="sxs-lookup"><span data-stu-id="7bc71-104">Azure Event Grid is a fully-managed intelligent event routing service that allows for uniform event consumption using a publish-subscribe model.</span></span>

<span data-ttu-id="7bc71-105">[Weitere Informationen](/azure/event-grid/overview) zu Azure Event Grid und erste Schritte mit dem [Tutorial zu Azure Blob Storage-Ereignissen](/azure/storage/blobs/storage-blob-event-quickstart)</span><span class="sxs-lookup"><span data-stu-id="7bc71-105">[Learn more](/azure/event-grid/overview) about Azure Event Grid and get started with the [Azure Blob storage event tutorial](/azure/storage/blobs/storage-blob-event-quickstart).</span></span> 

## <a name="publish-sdk"></a><span data-ttu-id="7bc71-106">Veröffentlichungs-SDK</span><span class="sxs-lookup"><span data-stu-id="7bc71-106">Publish SDK</span></span>

<span data-ttu-id="7bc71-107">Mit dem Veröffentlichungs-SDK von Azure Event Grid können Sie Ereignisse authentifizieren, erstellen, verarbeiten und in Themen veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="7bc71-107">Authenticate, create, handle, and publish events to topics using the Azure Event Grid publish SDK.</span></span>

### <a name="installation"></a><span data-ttu-id="7bc71-108">Installation</span><span class="sxs-lookup"><span data-stu-id="7bc71-108">Installation</span></span> 

<span data-ttu-id="7bc71-109">Installieren Sie das Paket mithilfe von [pip](https://pip.pypa.io/en/stable/quickstart/).</span><span class="sxs-lookup"><span data-stu-id="7bc71-109">Install the package with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```bash
pip install azure-eventgrid
```

### <a name="example"></a><span data-ttu-id="7bc71-110">Beispiel</span><span class="sxs-lookup"><span data-stu-id="7bc71-110">Example</span></span> 

<span data-ttu-id="7bc71-111">Der folgende Code veröffentlicht ein Ereignis in einem Thema.</span><span class="sxs-lookup"><span data-stu-id="7bc71-111">The following code publishes an event to a topic.</span></span> <span data-ttu-id="7bc71-112">Sie können den Schlüssel und Endpunkt des Themas über das Azure-Portal oder die Azure-Befehlszeilenschnittstelle abrufen:</span><span class="sxs-lookup"><span data-stu-id="7bc71-112">You can retrieve the topic key and endpoint through the Azure Portal or through the Azure CLI:</span></span>

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
> [<span data-ttu-id="7bc71-113">Informationen zu den Client-APIs</span><span class="sxs-lookup"><span data-stu-id="7bc71-113">Explore the Client APIs</span></span>](/python/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a><span data-ttu-id="7bc71-114">Verwaltungs-SDK</span><span class="sxs-lookup"><span data-stu-id="7bc71-114">Management SDK</span></span>

<span data-ttu-id="7bc71-115">Das Verwaltungs-SDK ermöglicht Ihnen das Erstellen, Aktualisieren und Löschen von Event Grid-Instanzen, -Themen und -Abonnements.</span><span class="sxs-lookup"><span data-stu-id="7bc71-115">Create, update, or delete Event Grid instances, topics, and subscriptions with the management SDK.</span></span>

### <a name="installation"></a><span data-ttu-id="7bc71-116">Installation</span><span class="sxs-lookup"><span data-stu-id="7bc71-116">Installation</span></span> 

<span data-ttu-id="7bc71-117">Installieren Sie das Paket mithilfe von [pip](https://pip.pypa.io/en/stable/quickstart/).</span><span class="sxs-lookup"><span data-stu-id="7bc71-117">Install the package with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```bash
pip install azure-mgmt-eventgrid
```

### <a name="example"></a><span data-ttu-id="7bc71-118">Beispiel</span><span class="sxs-lookup"><span data-stu-id="7bc71-118">Example</span></span>

<span data-ttu-id="7bc71-119">Der folgende Code erstellt ein benutzerdefiniertes Thema und abonniert einen Endpunkt für das Thema.</span><span class="sxs-lookup"><span data-stu-id="7bc71-119">The following creates a custom topic and subscribes an endpoint to the topic.</span></span> <span data-ttu-id="7bc71-120">Der Code sendet anschließend über HTTPS ein Ereignis an das Thema.</span><span class="sxs-lookup"><span data-stu-id="7bc71-120">The code then sends an event to the topic through HTTPS.</span></span>
<span data-ttu-id="7bc71-121">RequestBin ist ein Open Source-Drittanbietertool, mit dem Sie einen Endpunkt erstellen und Anforderungen anzeigen können, die an ihn gesendet werden.</span><span class="sxs-lookup"><span data-stu-id="7bc71-121">RequestBin is an open source, third-party tool that enables you to create an endpoint, and view requests that are sent to it.</span></span> <span data-ttu-id="7bc71-122">Wechseln Sie zu [RequestBin](https://requestb.in/), und klicken Sie auf **Create a RequestBin** (RequestBin erstellen).</span><span class="sxs-lookup"><span data-stu-id="7bc71-122">Go to [RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span> <span data-ttu-id="7bc71-123">Kopieren Sie die Bin-URL. Sie wird zum Abonnieren des Themas benötigt.</span><span class="sxs-lookup"><span data-stu-id="7bc71-123">Copy the bin URL, because you need it when subscribing to the topic.</span></span>

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
<span data-ttu-id="7bc71-124">Navigieren Sie zu der zuvor erstellten RequestBin-URL, um das eben gesendete Ereignis anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="7bc71-124">Browse to the RequestBin URL created earlier to see the event just sent.</span></span>

<span data-ttu-id="7bc71-125">Bereinigen von Ressourcen</span><span class="sxs-lookup"><span data-stu-id="7bc71-125">Clean up resources</span></span>
```azurecli-interactive
az group delete --name gridResourceGroup
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="7bc71-126">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="7bc71-126">Explore the Management APIs</span></span>](/python/api/overview/azure/eventgrid/management)

## <a name="learn-more"></a><span data-ttu-id="7bc71-127">Weitere Informationen</span><span class="sxs-lookup"><span data-stu-id="7bc71-127">Learn more</span></span>

<span data-ttu-id="7bc71-128">[Receive events using the Event Grid SDK](/azure/event-grid/receive-events) (Empfangen von Ereignissen mithilfe des Event Grid SDK)</span><span class="sxs-lookup"><span data-stu-id="7bc71-128">[Receive events using the Event Grid SDK](/azure/event-grid/receive-events)</span></span>