---
title: "Service Bus-Bibliotheken für Python"
description: "Referenzdokumentation für die Python-Clientbibliotheken und -Verwaltungsbibliotheken für Service Bus"
keywords: Azure, Python, SDK, API, Messaging, PubSub, Pub-Sub, Nachrichtenbroker
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.devlang: python
ms.service: service-bus
ms.openlocfilehash: 6c0bc66fbe8194b5b8f34ee8e29945b03ba8c242
ms.sourcegitcommit: d7c26ac167cf6a6491358ac3153f268bc90e55e9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/24/2018
---
# <a name="service-bus-libraries-for-python"></a><span data-ttu-id="e1b06-104">Service Bus-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="e1b06-104">Service Bus libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="e1b06-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="e1b06-105">Overview</span></span>

<span data-ttu-id="e1b06-106">Microsoft Azure Service Bus unterstützt einen Satz cloudbasierter, nachrichtenorientierter Middlewaretechnologien, darunter zuverlässiges Message Queuing und dauerhaftes Veröffentlichungs-/Abonnementmessaging.</span><span class="sxs-lookup"><span data-stu-id="e1b06-106">Microsoft Azure Service Bus supports a set of cloud-based, message-oriented middleware technologies including reliable message queuing and durable publish/subscribe messaging.</span></span> 

## <a name="install-the-libraries"></a><span data-ttu-id="e1b06-107">Installieren der Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="e1b06-107">Install the libraries</span></span>
```bash
pip install azure-mgmt-servicebus
```

## <a name="servicebus-queues"></a><span data-ttu-id="e1b06-108">ServiceBus-Warteschlangen</span><span class="sxs-lookup"><span data-stu-id="e1b06-108">ServiceBus Queues</span></span>
<span data-ttu-id="e1b06-109">ServiceBus-Warteschlangen stellen eine Alternative zu Storage-Warteschlangen dar. Sie sind in Szenarien nützlich, in denen komplexere Messagingfeatures (größere Nachrichten, Nachrichtensortierung, einzelne schädliche Lesevorgänge, zeitgesteuerte Zustellung) mit pushbasierter Zustellung und langen Abrufvorgängen erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="e1b06-109">ServiceBus Queues are an alternative to Storage Queues that might be useful in scenarios where more advanced messaging features are needed (larger message sizes, message ordering, single-operation destructive reads, scheduled delivery) using push-style delivery (using long polling).</span></span>

<span data-ttu-id="e1b06-110">Der Dienst kann SAS-Authentifizierung (Shared Access Signature) oder ACS-Authentifizierung nutzen.</span><span class="sxs-lookup"><span data-stu-id="e1b06-110">The service can use Shared Access Signature authentication, or ACS authentication.</span></span>

<span data-ttu-id="e1b06-111">Für Service Bus-Namespaces, die nach August 2014 über das Azure-Portal erstellt wurden, wird die ACS-Authentifizierung nicht mehr unterstützt.</span><span class="sxs-lookup"><span data-stu-id="e1b06-111">Service bus namespaces created using the Azure portal after August 2014 no longer support ACS authentication.</span></span> <span data-ttu-id="e1b06-112">Sie können mit dem Azure SDK Namespaces erstellen, die mit ACS kompatibel sind.</span><span class="sxs-lookup"><span data-stu-id="e1b06-112">You can create ACS compatible namespaces with the Azure SDK.</span></span>

### <a name="shared-access-signature-authentication"></a><span data-ttu-id="e1b06-113">SAS-Authentifizierung (Shared Access Signature)</span><span class="sxs-lookup"><span data-stu-id="e1b06-113">Shared Access Signature Authentication</span></span>

<span data-ttu-id="e1b06-114">Wenn Sie SAS-Authentifizierung verwenden möchten, erstellen Sie den Service Bus-Dienst wie folgt:</span><span class="sxs-lookup"><span data-stu-id="e1b06-114">To use Shared Access Signature authentication, create the service bus service with:</span></span>

```python
from azure.servicebus import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

### <a name="acs-authentication"></a><span data-ttu-id="e1b06-115">ACS-Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="e1b06-115">ACS Authentication</span></span>

<span data-ttu-id="e1b06-116">Wenn Sie ACS-Authentifizierung verwenden möchten, erstellen Sie den Service Bus-Dienst wie folgt:</span><span class="sxs-lookup"><span data-stu-id="e1b06-116">To use ACS authentication, create the service bus service with:</span></span>

```python
from azure.servicebus import ServiceBusService

account_key = '' # DEFAULT KEY from Azure portal
issuer = 'owner' # DEFAULT ISSUER from Azure portal
sbs = ServiceBusService(service_namespace,
                        account_key=account_key,
                        issuer=issuer)
```
### <a name="sending-and-receiving-messages"></a><span data-ttu-id="e1b06-117">Senden und Empfangen von Nachrichten</span><span class="sxs-lookup"><span data-stu-id="e1b06-117">Sending and Receiving Messages</span></span>

<span data-ttu-id="e1b06-118">Mit der **create\_queue**-Methode können Sie sicherstellen, dass eine Warteschlange vorhanden ist:</span><span class="sxs-lookup"><span data-stu-id="e1b06-118">The **create\_queue** method can be used to ensure a queue exists:</span></span>

```python
sbs.create_queue('taskqueue')
```
<span data-ttu-id="e1b06-119">Anschließend kann die **send\_queue\_message**-Methode aufgerufen werden, um die Nachricht in die Warteschlange einzufügen:</span><span class="sxs-lookup"><span data-stu-id="e1b06-119">The **send\_queue\_message** method can then be called to insert the message into the queue:</span></span>

```python
from azure.servicebus import Message

msg = Message('Hello World!')
sbs.send_queue_message('taskqueue', msg)
```
<span data-ttu-id="e1b06-120">Dann können Sie die **send\_queue\_message_batch**-Methode aufrufen, um mehrere Nachrichten auf einmal zu senden:</span><span class="sxs-lookup"><span data-stu-id="e1b06-120">The **send\_queue\_message_batch** method can then be called to send several messages at once:</span></span>

```python
from azure.servicebus import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
```
<span data-ttu-id="e1b06-121">Anschließend kann die **receive\_queue\_message**-Methode aufgerufen werden, um die Nachricht aus der Warteschlange zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="e1b06-121">It is then possible to call the **receive\_queue\_message** method to dequeue the message.</span></span>

```python
msg = sbs.receive_queue_message('taskqueue')
```

## <a name="servicebus-topics"></a><span data-ttu-id="e1b06-122">ServiceBus-Themen</span><span class="sxs-lookup"><span data-stu-id="e1b06-122">ServiceBus Topics</span></span>

<span data-ttu-id="e1b06-123">ServiceBus-Themen sind (neben ServiceBus-Warteschlangen) eine weitere Abstraktion, die die Implementierung von Pub/Sub-Szenarien vereinfacht.</span><span class="sxs-lookup"><span data-stu-id="e1b06-123">ServiceBus topics are an abstraction on top of ServiceBus Queues that make pub/sub scenarios easy to implement.</span></span>

<span data-ttu-id="e1b06-124">Mit der **create\_topic**-Methode können Sie ein Thema auf Serverseite erstellen:</span><span class="sxs-lookup"><span data-stu-id="e1b06-124">The **create\_topic** method can be used to create a server-side topic:</span></span>

```python
sbs.create_topic('taskdiscussion')
```
<span data-ttu-id="e1b06-125">Mit der **send\_topic\_message**-Methode kann eine Nachricht an ein Thema gesendet werden:</span><span class="sxs-lookup"><span data-stu-id="e1b06-125">The **send\_topic\_message** method can be used to send a message to a topic:</span></span>

```python
from azure.servicebus import Message

msg = Message(b'Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
```

<span data-ttu-id="e1b06-126">Mit der **send\_topic\_message_batch**-Methode können mehrere Nachrichten auf einmal gesendet werden:</span><span class="sxs-lookup"><span data-stu-id="e1b06-126">The **send\_topic\_message_batch** method can be used to send several messages at once:</span></span>

```python
from azure.servicebus import Message

msg1 = Message(b'Hello World!')
msg2 = Message(b'Hello World again!')
sbs.send_topic_message_batch('taskdiscussion', [msg1, msg2])
```

<span data-ttu-id="e1b06-127">Beachten Sie, dass in Python 3 eine str-Nachricht UFT-8-codiert ist and Sie die Codierung in Python 2 selbst verwalten müssen.</span><span class="sxs-lookup"><span data-stu-id="e1b06-127">Please consider that in Python 3 a str message will be utf-8 encoded and you should have to manage your encoding yourself in Python 2.</span></span>

<span data-ttu-id="e1b06-128">Ein Client kann dann ein Abonnement erstellen und mit der Verarbeitung von Nachrichten beginnen, indem er die **create\_subscription**-Methode gefolgt von der **receive\_subscription\_message**-Methode aufruft.</span><span class="sxs-lookup"><span data-stu-id="e1b06-128">A client can then create a subscription and start consuming messages by calling the **create\_subscription** method followed by the **receive\_subscription\_message** method.</span></span> <span data-ttu-id="e1b06-129">Beachten Sie, dass vor dem Erstellen des Abonnements gesendete Nachrichten nicht empfangen werden.</span><span class="sxs-lookup"><span data-stu-id="e1b06-129">Please note that any messages sent before the subscription is created will not be received.</span></span>

```python
from azure.servicebus import Message

sbs.create_subscription('taskdiscussion', 'client1')
msg = Message('Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
msg = sbs.receive_subscription_message('taskdiscussion', 'client1')
```

## <a name="event-hub"></a><span data-ttu-id="e1b06-130">Event Hub</span><span class="sxs-lookup"><span data-stu-id="e1b06-130">Event Hub</span></span>

<span data-ttu-id="e1b06-131">Event Hubs ermöglichen die Erfassung von Ereignisströmen bei hohem Durchsatz von unterschiedlichen Geräten und Diensten.</span><span class="sxs-lookup"><span data-stu-id="e1b06-131">Event Hubs enable the collection of event streams at high throughput, from a diverse set of devices and services.</span></span>

<span data-ttu-id="e1b06-132">Mit der **create\_event\_hub**-Methode können Sie einen Event Hub erstellen:</span><span class="sxs-lookup"><span data-stu-id="e1b06-132">The **create\_event\_hub** method can be used to create an event hub:</span></span>

```python
sbs.create_event_hub('myhub')
```
<span data-ttu-id="e1b06-133">So senden Sie ein Ereignis:</span><span class="sxs-lookup"><span data-stu-id="e1b06-133">To send an event:</span></span>

```python
sbs.send_event('myhub', '{ "DeviceId":"dev-01", "Temperature":"37.0" }')
```
<span data-ttu-id="e1b06-134">Der Ereignisinhalt ist die Ereignisnachricht oder eine JSON-codierte Zeichenfolge mit mehreren Nachrichten.</span><span class="sxs-lookup"><span data-stu-id="e1b06-134">The event content is the event message or JSON-encoded string that contains multiple messages.</span></span>

## <a name="advanced-features"></a><span data-ttu-id="e1b06-135">Erweiterte Funktionen</span><span class="sxs-lookup"><span data-stu-id="e1b06-135">Advanced features</span></span>

### <a name="broker-properties-and-user-properties"></a><span data-ttu-id="e1b06-136">Brokereigenschaften und Benutzereigenschaften</span><span class="sxs-lookup"><span data-stu-id="e1b06-136">Broker Properties and User Properties</span></span>

<span data-ttu-id="e1b06-137">In diesem Abschnitt wird die Verwendung der [hier](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties) beschriebenen Broker- und Benutzereigenschaften erläutert:</span><span class="sxs-lookup"><span data-stu-id="e1b06-137">This section describes how to use Broker and User properties defined [here](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties):</span></span>

```python
sent_msg = Message(b'This is the third message',
                    broker_properties={'Label': 'M3'},
                    custom_properties={'Priority': 'Medium',
                                        'Customer': 'ABC'}
            )
```
<span data-ttu-id="e1b06-138">Sie können „datetime“, „int“, „float“ oder „boolean“ verwenden.</span><span class="sxs-lookup"><span data-stu-id="e1b06-138">You can use datetime, int, float or boolean</span></span>

```python
props = {'hello': 'world',
            'number': 42,
            'active': True,
            'deceased': False,
            'large': 8555111000,
            'floating': 3.14,
            'dob': datetime(2011, 12, 14),
            'double_quote_message': 'This "should" work fine',
            'quote_message': "This 'should' work fine"}
sent_msg = Message(b'message with properties', custom_properties=props)
```
<span data-ttu-id="e1b06-139">Aus Gründen der Kompatibilität mit einer älteren Version dieser Bibliothek kann `broker_properties` auch als JSON-Zeichenfolge definiert werden.</span><span class="sxs-lookup"><span data-stu-id="e1b06-139">For compatibility reason with old version of this library, `broker_properties` could also be defined as a JSON string.</span></span>
<span data-ttu-id="e1b06-140">In diesem Fall müssen Sie eine gültige JSON-Zeichenfolge schreiben. Von Python wird vor der Übermittlung an die Rest-API keine Überprüfung ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="e1b06-140">If this situation, you're responsible to write a valid JSON string, no check will be made by Python before sending to the RestAPI.</span></span>

```python
broker_properties = '{"ForcePersistence": false, "Label": "My label"}'
sent_msg = Message(b'receive message',
                    broker_properties = broker_properties
)
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e1b06-141">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="e1b06-141">Explore the Management APIs</span></span>](/python/api/overview/azure/servicebus/management)