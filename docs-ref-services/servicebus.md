---
title: Service Bus-Bibliotheken für Python
description: Referenzdokumentation für die Python-Clientbibliotheken und -Verwaltungsbibliotheken für Service Bus
keywords: Azure, Python, SDK, API, Messaging, PubSub, Pub-Sub, Nachrichtenbroker
author: annatisch
ms.author: antisch
manager: mayurid
ms.date: 01/15/2019
ms.topic: article
ms.devlang: python
ms.service: service-bus
ms.openlocfilehash: 540a2a248f7a2abcc83517bc4a4ef96ef03e8a9f
ms.sourcegitcommit: fba77bdf8eb9f49621be94544d9fef88aff98c14
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/23/2019
ms.locfileid: "54747740"
---
# <a name="service-bus-libraries-for-python"></a><span data-ttu-id="cbd22-104">Service Bus-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="cbd22-104">Service Bus libraries for Python</span></span>

<span data-ttu-id="cbd22-105">Microsoft Azure Service Bus unterstützt einen Satz cloudbasierter, nachrichtenorientierter Middlewaretechnologien, darunter zuverlässiges Message Queuing und dauerhaftes Veröffentlichungs-/Abonnementmessaging.</span><span class="sxs-lookup"><span data-stu-id="cbd22-105">Microsoft Azure Service Bus supports a set of cloud-based, message-oriented middleware technologies including reliable message queuing and durable publish/subscribe messaging.</span></span>

* [<span data-ttu-id="cbd22-106">SDK-Quellcode</span><span class="sxs-lookup"><span data-stu-id="cbd22-106">SDK source code</span></span>](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus)
* [<span data-ttu-id="cbd22-107">SDK-Referenzdokumentation</span><span class="sxs-lookup"><span data-stu-id="cbd22-107">SDK reference documentation</span></span>](https://docs.microsoft.com/python/api/overview/azure/servicebus/client?view=azure-python)

## <a name="whats-new-in-v0500"></a><span data-ttu-id="cbd22-108">Neuerungen in v0.50.0</span><span class="sxs-lookup"><span data-stu-id="cbd22-108">What's new in v0.50.0?</span></span>
<span data-ttu-id="cbd22-109">Ab Version 0.50.0 ist eine neue AMQP-basierte API zum Senden und Empfangen von Nachrichten verfügbar.</span><span class="sxs-lookup"><span data-stu-id="cbd22-109">As of version 0.50.0 a new AMQP-based API is available for sending and receiving messages.</span></span> <span data-ttu-id="cbd22-110">Dieses Update umfasst **wichtige Änderungen**.</span><span class="sxs-lookup"><span data-stu-id="cbd22-110">This update involves **breaking changes**.</span></span>
<span data-ttu-id="cbd22-111">Erfahren Sie im Abschnitt zur [Migration von v0.21.1 zu v0.50.0](#migration-from-v0211-to-v0500), ob ein Upgrade für Sie zu diesem Zeitpunkt sinnvoll ist.</span><span class="sxs-lookup"><span data-stu-id="cbd22-111">Please read [Migration from v0.21.1 to v0.50.0](#migration-from-v0211-to-v0500) to determine if upgrading is right for you at this time.</span></span>

<span data-ttu-id="cbd22-112">Mit der neuen AMQP-basierten API profitieren Sie von einer zuverlässigeren Nachrichtenübergabe sowie einer besseren Leistung und Unterstützung erweiterter Features.</span><span class="sxs-lookup"><span data-stu-id="cbd22-112">The new AMQP-based API offers improved message passing reliability, performance and expanded feature support going forward.</span></span>
<span data-ttu-id="cbd22-113">Die neue API unterstützt zudem asynchrone Vorgänge (basierend auf Asyncio) für das Senden, Empfangen und Verarbeiten von Nachrichten.</span><span class="sxs-lookup"><span data-stu-id="cbd22-113">The new API also offers support for asynchronous operations (based on asyncio) for sending, receiving and handling messages.</span></span>

<span data-ttu-id="cbd22-114">Eine Dokumentation zu den älteren HTTP-basierten Vorgängen finden Sie im Abschnitt zur [Verwendung HTTP-basierter Vorgänge der Legacy-API](#using-http-based-operations-of-the-legacy-api).</span><span class="sxs-lookup"><span data-stu-id="cbd22-114">For documentation on the legacy HTTP-based operations please see [Using HTTP-based operations of the legacy API](#using-http-based-operations-of-the-legacy-api).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="cbd22-115">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="cbd22-115">Prerequisites</span></span>

* <span data-ttu-id="cbd22-116">Azure-Abonnement ([Erstellen Sie ein kostenloses Konto.](https://azure.microsoft.com/free/))</span><span class="sxs-lookup"><span data-stu-id="cbd22-116">Azure subscription - [Create a free account](https://azure.microsoft.com/free/)</span></span>
* <span data-ttu-id="cbd22-117">Azure [Service Bus-Namespace und Anmeldeinformationen für die Verwaltung](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-create-namespace-portal)</span><span class="sxs-lookup"><span data-stu-id="cbd22-117">Azure [Service Bus namespace and management credentials](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-create-namespace-portal)</span></span>
* [<span data-ttu-id="cbd22-118">Python 2.7-3.7</span><span class="sxs-lookup"><span data-stu-id="cbd22-118">Python 2.7-3.7</span></span>](https://www.python.org/downloads/)


## <a name="installation"></a><span data-ttu-id="cbd22-119">Installation</span><span class="sxs-lookup"><span data-stu-id="cbd22-119">Installation</span></span>
```bash
pip install azure-servicebus
```

## <a name="connect-to-azure-service-bus"></a><span data-ttu-id="cbd22-120">Herstellen der Verbindung mit Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="cbd22-120">Connect to Azure Service Bus</span></span>

### <a name="get-credentials"></a><span data-ttu-id="cbd22-121">Abrufen von Anmeldeinformationen</span><span class="sxs-lookup"><span data-stu-id="cbd22-121">Get credentials</span></span>
<span data-ttu-id="cbd22-122">Verwenden Sie den folgenden Azure CLI-Codeausschnitt, um eine Umgebungsvariable mit der Service Bus-Verbindungszeichenfolge zu füllen (Sie finden diesen Wert auch im Azure-Portal).</span><span class="sxs-lookup"><span data-stu-id="cbd22-122">Use the Azure CLI snippet below to populate an environment variable with the Service Bus connection string (you can also find this value in the Azure portal).</span></span> <span data-ttu-id="cbd22-123">Der Ausschnitt ist für die Bash-Shell formatiert.</span><span class="sxs-lookup"><span data-stu-id="cbd22-123">The snippet is formatted for the Bash shell.</span></span>

```Bash
RES_GROUP=<resource-group-name>
NAMESPACE=<servicebus-namespace>

export SB_CONN_STR=$(az servicebus namespace authorization-rule keys list \
 --resource-group $RES_GROUP \
 --namespace-name $NAMESPACE \
 --name RootManageSharedAccessKey \
 --query primaryConnectionString \
 --output tsv)
```

### <a name="create-client"></a><span data-ttu-id="cbd22-124">Erstellen des Clients</span><span class="sxs-lookup"><span data-stu-id="cbd22-124">Create client</span></span>
<span data-ttu-id="cbd22-125">Nach dem Auffüllen der `SB_CONN_STR`-Umgebungsvariablen können Sie das ServiceBusClient-Element erstellen.</span><span class="sxs-lookup"><span data-stu-id="cbd22-125">Once you've populated the `SB_CONN_STR` environment variable, you can create the ServiceBusClient.</span></span>
```python
import os
from azure.servicebus import ServiceBusClient

connection_str = os.environ['SB_CONN_STR']

sb_client = ServiceBusClient.from_connection_string(connection_str)
```
<span data-ttu-id="cbd22-126">Verwenden Sie für asynchrone Vorgänge den `azure.servicebus.aio`-Namespace.</span><span class="sxs-lookup"><span data-stu-id="cbd22-126">If you wish to use asynchronous operations, please use the `azure.servicebus.aio` namespace.</span></span>
```python
import os
from azure.servicebus.aio import ServiceBusClient

connection_str = os.environ['SB_CONN_STR']

sb_client = ServiceBusClient.from_connection_string(connection_str)
```


## <a name="service-bus-queues"></a><span data-ttu-id="cbd22-127">Service Bus-Warteschlangen</span><span class="sxs-lookup"><span data-stu-id="cbd22-127">Service Bus queues</span></span>
<span data-ttu-id="cbd22-128">Service Bus-Warteschlangen stellen eine Alternative zu Storage-Warteschlangen dar. Sie sind in Szenarien nützlich, in denen komplexere Messagingfeatures (größere Nachrichten, Nachrichtensortierung, einzelne schädliche Lesevorgänge, zeitgesteuerte Zustellung) mit pushbasierter Zustellung und langen Abrufvorgängen erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="cbd22-128">Service Bus queues are an alternative to Storage queues that might be useful in scenarios where more advanced messaging features are needed (larger message sizes, message ordering, single-operation destructive reads, scheduled delivery) using push-style delivery (using long polling).</span></span>

### <a name="create-queue"></a><span data-ttu-id="cbd22-129">Erstellen einer Warteschlange</span><span class="sxs-lookup"><span data-stu-id="cbd22-129">Create queue</span></span>
<span data-ttu-id="cbd22-130">Dadurch wird eine neue Warteschlange im Service Bus-Namespace erstellt.</span><span class="sxs-lookup"><span data-stu-id="cbd22-130">This creates a new queue within the Service Bus namespace.</span></span> <span data-ttu-id="cbd22-131">Wenn innerhalb des Namespace bereits eine Warteschlange vorhanden ist, wird ein Fehler ausgelöst.</span><span class="sxs-lookup"><span data-stu-id="cbd22-131">If a queue of the same name already exists within the namespace an error will be raised.</span></span> 
```python
sb_client.create_queue("MyQueue")
```
<span data-ttu-id="cbd22-132">Sie können auch optionale Parameter festlegen, um das Verhalten der Warteschlange zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="cbd22-132">Optional parameters to configure the queue behaviour can also be specified.</span></span>
```python
sb_client.create_queue(
    "MySessionQueue",
    requires_session=True  # Create a sessionful queue
    max_delivery_count=5  # Max delivery attempts per message
)
```

### <a name="get-a-queue-client"></a><span data-ttu-id="cbd22-133">Abrufen eines Warteschlangenclients</span><span class="sxs-lookup"><span data-stu-id="cbd22-133">Get a queue client</span></span>
<span data-ttu-id="cbd22-134">Ein QueueClient-Element kann zum Senden und Empfangen von Nachrichten über die Warteschlange sowie für weitere Vorgänge verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="cbd22-134">A QueueClient can be used to send and receive messages from the queue, along with other operations.</span></span>
```python
queue_client = sb_client.get_queue("MyQueue")
```

### <a name="sending-messages"></a><span data-ttu-id="cbd22-135">Senden von Nachrichten</span><span class="sxs-lookup"><span data-stu-id="cbd22-135">Sending messages</span></span>
<span data-ttu-id="cbd22-136">Der Warteschlangenclient kann mehrere Nachrichten gleichzeitig senden:</span><span class="sxs-lookup"><span data-stu-id="cbd22-136">The queue client can send one or more messages at a time:</span></span>
```python
from azure.servicebus import Message

message = Message("Hello World")
queue_client.send(message)

message_one = Message("First")
message_two = Message("Second")
queue_client.send([message_one, message_two])
```
<span data-ttu-id="cbd22-137">Bei jedem Aufruf von „QueueClient.send“ wird eine neue Dienstverbindung erstellt.</span><span class="sxs-lookup"><span data-stu-id="cbd22-137">Each call to QueueClient.send will create a new service connection.</span></span> <span data-ttu-id="cbd22-138">Wenn Sie die gleiche Verbindung für mehrere Sendeaufrufe wiederverwenden möchten, können Sie einen Absender öffnen:</span><span class="sxs-lookup"><span data-stu-id="cbd22-138">To reuse the same connection for multiple send calls, you can open a sender:</span></span>
```python
message_one = Message("First")
message_two = Message("Second")

with queue_client.get_sender() as sender:
    sender.send(message_one)
    sender.send(message_two)
```
<span data-ttu-id="cbd22-139">Wenn Sie einen asynchronen Client verwenden, nutzen die oben aufgeführten Vorgänge die Async-Syntax:</span><span class="sxs-lookup"><span data-stu-id="cbd22-139">If you are using an asynchronous client, the above operations will use async syntax:</span></span>
```python
from azure.servicebus.aio import Message

message = Message("Hello World")
await queue_client.send(message)

message_one = Message("First")
message_two = Message("Second")
async with queue_client.get_sender() as sender:
    await sender.send(message_one)
    await sender.send(message_two)
```


### <a name="receiving-messages"></a><span data-ttu-id="cbd22-140">Empfangen von Nachrichten</span><span class="sxs-lookup"><span data-stu-id="cbd22-140">Receiving messages</span></span>
<span data-ttu-id="cbd22-141">Nachrichten können als fortlaufender Iterator von einer Warteschlange empfangen werden.</span><span class="sxs-lookup"><span data-stu-id="cbd22-141">Messages can be received from a queue as a continuous iterator.</span></span> <span data-ttu-id="cbd22-142">Der Standardmodus für den Empfang von Nachrichten ist [PeekLock](https://docs.microsoft.com/rest/api/servicebus/peek-lock-message-non-destructive-read). Jede Nachricht muss explizit abgeschlossen werden, damit sie aus der Warteschlange entfernt wird.</span><span class="sxs-lookup"><span data-stu-id="cbd22-142">The default mode for message receiving is [PeekLock](https://docs.microsoft.com/rest/api/servicebus/peek-lock-message-non-destructive-read), which requires each message to be explicitly completed in order that it be removed from the queue.</span></span>
```python
messages = queue_client.get_receiver()
for message in messages:
    print(message)
    message.complete()
```
<span data-ttu-id="cbd22-143">Die Dienstverbindung bleibt während des gesamten Iterators geöffnet.</span><span class="sxs-lookup"><span data-stu-id="cbd22-143">The service connection will remain open for the entirety of the iterator.</span></span>
<span data-ttu-id="cbd22-144">Wenn Sie den Nachrichtenstream nur teilweise durchlaufen, sollten Sie den Empfänger in einer `with`-Anweisung ausführen, um sicherzustellen, dass die Verbindung geschlossen wurde:</span><span class="sxs-lookup"><span data-stu-id="cbd22-144">If you find yourself only partially iterating the message stream, you should run the receiver in a `with` statement to ensure the connection is closed:</span></span>
```python
with queue_client.get_receiver() as messages:
    for message in messages:
        print(message)
        message.complete()
        break
```
<span data-ttu-id="cbd22-145">Wenn Sie einen asynchronen Client verwenden, nutzen die oben aufgeführten Vorgänge die Async-Syntax:</span><span class="sxs-lookup"><span data-stu-id="cbd22-145">If you are using an asynchronous client, the above operations will use async syntax:</span></span>
```python
async with queue_client.get_receiver() as messages:
    async for message in messages:
        print(message)
        await message.complete()
        break
```

## <a name="service-bus-topics-and-subscriptions"></a><span data-ttu-id="cbd22-146">Service Bus-Themen und -Abonnements</span><span class="sxs-lookup"><span data-stu-id="cbd22-146">Service Bus topics and subscriptions</span></span>

<span data-ttu-id="cbd22-147">Service Bus-Themen und -Abonnements sind neben Service Bus-Warteschlangen eine weitere Abstraktion, die eine 1:n-Kommunikation mit dem Muster „Veröffentlichen/Abonnieren“ bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="cbd22-147">Service Bus topics and subscriptions are an abstraction on top of Service Bus queues that provide a one-to-many form of communication, in a publish/subscribe pattern.</span></span> <span data-ttu-id="cbd22-148">Nachrichten werden an ein Thema gesendet und für mindestens ein zugeordnetes Abonnement bereitgestellt. Das ist für die Skalierung in Szenarien mit sehr vielen Benutzern hilfreich.</span><span class="sxs-lookup"><span data-stu-id="cbd22-148">Messages are sent to a topic and delivered to one or more associated subscriptions, which is useful for scaling to large numbers of recipients.</span></span>

### <a name="create-topic"></a><span data-ttu-id="cbd22-149">Thema erstellen</span><span class="sxs-lookup"><span data-stu-id="cbd22-149">Create topic</span></span>
<span data-ttu-id="cbd22-150">Hiermit wird eine neues Thema im Service Bus-Namespace erstellt.</span><span class="sxs-lookup"><span data-stu-id="cbd22-150">This creates a new topic within the Service Bus namespace.</span></span> <span data-ttu-id="cbd22-151">Wenn bereits ein Thema mit dem gleichen Namen vorhanden ist, wird ein Fehler ausgelöst.</span><span class="sxs-lookup"><span data-stu-id="cbd22-151">If a topic of the same name already exists an error will be raised.</span></span> 
```python
sb_client.create_topic("MyTopic")
```

### <a name="get-a-topic-client"></a><span data-ttu-id="cbd22-152">Abrufen eines Themenclients</span><span class="sxs-lookup"><span data-stu-id="cbd22-152">Get a topic client</span></span>
<span data-ttu-id="cbd22-153">Ein TopicClient-Element kann zum Senden von Nachrichten an das Thema sowie für andere Vorgänge verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="cbd22-153">A TopicClient can be used to send messages to the topic, along with other operations.</span></span>
```python
topic_client = sb_client.get_topic("MyTopic")
```

### <a name="create-subscription"></a><span data-ttu-id="cbd22-154">Erstellen des Abonnements</span><span class="sxs-lookup"><span data-stu-id="cbd22-154">Create subscription</span></span>
<span data-ttu-id="cbd22-155">Hiermit wird ein neues Abonnement für das angegebene Thema innerhalb des Service Bus-Namespace erstellt.</span><span class="sxs-lookup"><span data-stu-id="cbd22-155">This creates a new subscription for the specified topic within the Service Bus namespace.</span></span>
```python
sb_client.create_subscription("MyTopic", "MySubscription")
```

### <a name="get-a-subscription-client"></a><span data-ttu-id="cbd22-156">Abrufen eines Abonnementclients</span><span class="sxs-lookup"><span data-stu-id="cbd22-156">Get a subscription client</span></span>
<span data-ttu-id="cbd22-157">Ein SubscriptionClient-Element kann zum Empfangen von Nachrichten aus der Warteschlange sowie für weitere Vorgänge verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="cbd22-157">A SubscriptionClient can be used to receive messages from the topic, along with other operations.</span></span>
```python
topic_client = sb_client.get_subscription("MyTopic", "MySubscription")
```

## <a name="migration-from-v0211-to-v0500"></a><span data-ttu-id="cbd22-158">Migration von v0.21.1 zu v0.50.0</span><span class="sxs-lookup"><span data-stu-id="cbd22-158">Migration from v0.21.1 to v0.50.0</span></span>
<span data-ttu-id="cbd22-159">In Version 0.50.0 wurden wichtige Änderungen eingeführt.</span><span class="sxs-lookup"><span data-stu-id="cbd22-159">Major breaking changes were introduced in version 0.50.0.</span></span>
<span data-ttu-id="cbd22-160">Die ursprüngliche HTTP-basierte API ist auch in v0.50.0 weiterhin verfügbar. Jedoch ist sie jetzt unter einem neuen Namespace vorhanden: `azure.servicebus.control_client`.</span><span class="sxs-lookup"><span data-stu-id="cbd22-160">The original HTTP-based API is still available in v0.50.0 - however it now exists under a new namesapce: `azure.servicebus.control_client`.</span></span>

### <a name="should-i-upgrade"></a><span data-ttu-id="cbd22-161">Sollte ich ein Upgrade durchführen?</span><span class="sxs-lookup"><span data-stu-id="cbd22-161">Should I upgrade?</span></span>
<span data-ttu-id="cbd22-162">Das neue Paket (v0.50.0) bietet keine Verbesserungen in HTTP-basierten Vorgängen über v0.21.1.</span><span class="sxs-lookup"><span data-stu-id="cbd22-162">The new package (v0.50.0) offers no improvements in HTTP-based operations over v0.21.1.</span></span> <span data-ttu-id="cbd22-163">Die HTTP-basierte API ist bis auf die Verfügbarkeit unter einem neuen Namespace identisch.</span><span class="sxs-lookup"><span data-stu-id="cbd22-163">The HTTP-based API is identical except that it now exists under a new namespace.</span></span> <span data-ttu-id="cbd22-164">Wenn Sie nur HTTP-basierte Vorgänge verwenden möchten (`create_queue`, `delete_queue` usw.), bietet Ihnen ein Upgrade zu diesem Zeitpunkt keine weiteren Vorteile.</span><span class="sxs-lookup"><span data-stu-id="cbd22-164">For this reason if you only wish to use HTTP-based operations (`create_queue`, `delete_queue` etc) - there will be no additional benefit in upgrading at this time.</span></span>


### <a name="how-do-i-migrate-my-code-to-the-new-version"></a><span data-ttu-id="cbd22-165">Wie migriere ich meinen Code zur neuen Version?</span><span class="sxs-lookup"><span data-stu-id="cbd22-165">How do I migrate my code to the new version?</span></span>
<span data-ttu-id="cbd22-166">Code, der für v0.21.0 geschrieben wird, kann durch einfaches Ändern des Import-Namespace zur Version 0.50.0 portiert werden:</span><span class="sxs-lookup"><span data-stu-id="cbd22-166">Code written against v0.21.0 can be ported to version 0.50.0 by simply changing the import namespace:</span></span>

```python
# from azure.servicebus import ServiceBusService  <- This will now raise an ImportError
from azure.servicebus.control_client import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

## <a name="using-http-based-operations-of-the-legacy-api"></a><span data-ttu-id="cbd22-167">Verwenden von HTTP-basierten Vorgängen der Legacy-API</span><span class="sxs-lookup"><span data-stu-id="cbd22-167">Using HTTP-based operations of the legacy API</span></span>
<span data-ttu-id="cbd22-168">Die folgende Dokumentation beschreibt die Legacy-API und sollte verwendet werden, wenn Sie vorhandenen Code zu v0.50.0 portieren möchten, ohne weitere Änderungen vorzunehmen.</span><span class="sxs-lookup"><span data-stu-id="cbd22-168">The following documentation describes the legacy API and should be used for those wishing to port existing code to v0.50.0 without making any additional changes.</span></span> <span data-ttu-id="cbd22-169">Diese Referenz kann auch als Leitfaden dienen, wenn Sie v0.21.1 verwenden.</span><span class="sxs-lookup"><span data-stu-id="cbd22-169">This reference can also be used as guidance by those using v0.21.1.</span></span>
<span data-ttu-id="cbd22-170">Wenn Sie neuen Code schreiben, empfehlen wir Ihnen, die oben beschriebene neue API zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="cbd22-170">For those writing new code, we recommend using the new API described above.</span></span>

### <a name="service-bus-queues"></a><span data-ttu-id="cbd22-171">Service Bus-Warteschlangen</span><span class="sxs-lookup"><span data-stu-id="cbd22-171">Service Bus queues</span></span>

#### <a name="shared-access-signature-sas-authentication"></a><span data-ttu-id="cbd22-172">SAS-Authentifizierung (Shared Access Signature)</span><span class="sxs-lookup"><span data-stu-id="cbd22-172">Shared Access Signature (SAS) authentication</span></span>

<span data-ttu-id="cbd22-173">Wenn Sie SAS-Authentifizierung verwenden möchten, erstellen Sie den Service Bus-Dienst wie folgt:</span><span class="sxs-lookup"><span data-stu-id="cbd22-173">To use Shared Access Signature authentication, create the service bus service with:</span></span>

```python
from azure.servicebus.control_client import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

#### <a name="access-control-service-acs-authentication"></a><span data-ttu-id="cbd22-174">ACS-Authentifizierung (Access Control Service)</span><span class="sxs-lookup"><span data-stu-id="cbd22-174">Access Control Service (ACS) authentication</span></span>
<span data-ttu-id="cbd22-175">ACS wird auf neuen Service Bus-Namespaces nicht mehr unterstützt.</span><span class="sxs-lookup"><span data-stu-id="cbd22-175">ACS is no longer supported on new Service Bus namespaces.</span></span> <span data-ttu-id="cbd22-176">Wir empfehlen das [Migrieren von Anwendungen zur SAS-Authentifizierung](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-migrate-acs-sas).</span><span class="sxs-lookup"><span data-stu-id="cbd22-176">We recommend [migrating applications to SAS authentication](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-migrate-acs-sas).</span></span>
<span data-ttu-id="cbd22-177">Um die ACS-Authentifizierung in einem älteren Service Bus-Namespace zu verwenden, erstellen Sie ServiceBusService mit:</span><span class="sxs-lookup"><span data-stu-id="cbd22-177">To use ACS authentication within an older Service Bus namesapce, create the ServiceBusService with:</span></span>

```python
from azure.servicebus.control_client import ServiceBusService

account_key = '' # DEFAULT KEY from Azure portal
issuer = 'owner' # DEFAULT ISSUER from Azure portal
sbs = ServiceBusService(service_namespace,
                        account_key=account_key,
                        issuer=issuer)
```
#### <a name="sending-and-receiving-messages"></a><span data-ttu-id="cbd22-178">Senden und Empfangen von Nachrichten</span><span class="sxs-lookup"><span data-stu-id="cbd22-178">Sending and receiving messages</span></span>

<span data-ttu-id="cbd22-179">Mit der **create\_queue**-Methode können Sie sicherstellen, dass eine Warteschlange vorhanden ist:</span><span class="sxs-lookup"><span data-stu-id="cbd22-179">The **create\_queue** method can be used to ensure a queue exists:</span></span>

```python
sbs.create_queue('taskqueue')
```
<span data-ttu-id="cbd22-180">Anschließend kann die **send\_queue\_message**-Methode aufgerufen werden, um die Nachricht in die Warteschlange einzufügen:</span><span class="sxs-lookup"><span data-stu-id="cbd22-180">The **send\_queue\_message** method can then be called to insert the message into the queue:</span></span>

```python
from azure.servicebus.control_client import Message

msg = Message('Hello World!')
sbs.send_queue_message('taskqueue', msg)
```
<span data-ttu-id="cbd22-181">Dann können Sie die **send\_queue\_message_batch**-Methode aufrufen, um mehrere Nachrichten auf einmal zu senden:</span><span class="sxs-lookup"><span data-stu-id="cbd22-181">The **send\_queue\_message_batch** method can then be called to send several messages at once:</span></span>

```python
from azure.servicebus.control_client import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
```
<span data-ttu-id="cbd22-182">Anschließend kann die **receive\_queue\_message**-Methode aufgerufen werden, um die Nachricht aus der Warteschlange zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="cbd22-182">It is then possible to call the **receive\_queue\_message** method to dequeue the message.</span></span>

```python
msg = sbs.receive_queue_message('taskqueue')
```

### <a name="service-bus-topics"></a><span data-ttu-id="cbd22-183">Service Bus-Themen</span><span class="sxs-lookup"><span data-stu-id="cbd22-183">Service Bus topics</span></span>

<span data-ttu-id="cbd22-184">Mit der **create\_topic**-Methode können Sie ein Thema auf Serverseite erstellen:</span><span class="sxs-lookup"><span data-stu-id="cbd22-184">The **create\_topic** method can be used to create a server-side topic:</span></span>

```python
sbs.create_topic('taskdiscussion')
```
<span data-ttu-id="cbd22-185">Mit der **send\_topic\_message**-Methode kann eine Nachricht an ein Thema gesendet werden:</span><span class="sxs-lookup"><span data-stu-id="cbd22-185">The **send\_topic\_message** method can be used to send a message to a topic:</span></span>

```python
from azure.servicebus.control_client import Message

msg = Message(b'Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
```

<span data-ttu-id="cbd22-186">Mit der **send\_topic\_message_batch**-Methode können mehrere Nachrichten auf einmal gesendet werden:</span><span class="sxs-lookup"><span data-stu-id="cbd22-186">The **send\_topic\_message_batch** method can be used to send several messages at once:</span></span>

```python
from azure.servicebus.control_client import Message

msg1 = Message(b'Hello World!')
msg2 = Message(b'Hello World again!')
sbs.send_topic_message_batch('taskdiscussion', [msg1, msg2])
```

<span data-ttu-id="cbd22-187">Beachten Sie, dass in Python 3 eine str-Nachricht UFT-8-codiert ist and Sie die Codierung in Python 2 selbst verwalten müssen.</span><span class="sxs-lookup"><span data-stu-id="cbd22-187">Please consider that in Python 3 a str message will be utf-8 encoded and you should have to manage your encoding yourself in Python 2.</span></span>

<span data-ttu-id="cbd22-188">Ein Client kann dann ein Abonnement erstellen und mit der Verarbeitung von Nachrichten beginnen, indem er die **create\_subscription**-Methode gefolgt von der **receive\_subscription\_message**-Methode aufruft.</span><span class="sxs-lookup"><span data-stu-id="cbd22-188">A client can then create a subscription and start consuming messages by calling the **create\_subscription** method followed by the **receive\_subscription\_message** method.</span></span> <span data-ttu-id="cbd22-189">Beachten Sie, dass vor dem Erstellen des Abonnements gesendete Nachrichten nicht empfangen werden.</span><span class="sxs-lookup"><span data-stu-id="cbd22-189">Please note that any messages sent before the subscription is created will not be received.</span></span>

```python
from azure.servicebus.control_client import Message

sbs.create_subscription('taskdiscussion', 'client1')
msg = Message('Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
msg = sbs.receive_subscription_message('taskdiscussion', 'client1')
```

### <a name="event-hub"></a><span data-ttu-id="cbd22-190">Event Hub</span><span class="sxs-lookup"><span data-stu-id="cbd22-190">Event Hub</span></span>

<span data-ttu-id="cbd22-191">Event Hubs ermöglichen die Erfassung von Ereignisströmen bei hohem Durchsatz von unterschiedlichen Geräten und Diensten.</span><span class="sxs-lookup"><span data-stu-id="cbd22-191">Event Hubs enable the collection of event streams at high throughput, from a diverse set of devices and services.</span></span>

<span data-ttu-id="cbd22-192">Mit der **create\_event\_hub**-Methode können Sie einen Event Hub erstellen:</span><span class="sxs-lookup"><span data-stu-id="cbd22-192">The **create\_event\_hub** method can be used to create an event hub:</span></span>

```python
sbs.create_event_hub('myhub')
```
<span data-ttu-id="cbd22-193">So senden Sie ein Ereignis:</span><span class="sxs-lookup"><span data-stu-id="cbd22-193">To send an event:</span></span>

```python
sbs.send_event('myhub', '{ "DeviceId":"dev-01", "Temperature":"37.0" }')
```
<span data-ttu-id="cbd22-194">Der Ereignisinhalt ist die Ereignisnachricht oder eine JSON-codierte Zeichenfolge mit mehreren Nachrichten.</span><span class="sxs-lookup"><span data-stu-id="cbd22-194">The event content is the event message or JSON-encoded string that contains multiple messages.</span></span>

### <a name="advanced-features"></a><span data-ttu-id="cbd22-195">Erweiterte Funktionen</span><span class="sxs-lookup"><span data-stu-id="cbd22-195">Advanced features</span></span>

#### <a name="broker-properties-and-user-properties"></a><span data-ttu-id="cbd22-196">Brokereigenschaften und Benutzereigenschaften</span><span class="sxs-lookup"><span data-stu-id="cbd22-196">Broker properties and user properties</span></span>

<span data-ttu-id="cbd22-197">In diesem Abschnitt wird die Verwendung der [hier](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties) beschriebenen Broker- und Benutzereigenschaften erläutert:</span><span class="sxs-lookup"><span data-stu-id="cbd22-197">This section describes how to use Broker and User properties defined [here](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties):</span></span>

```python
sent_msg = Message(b'This is the third message',
                   broker_properties={'Label': 'M3'},
                   custom_properties={'Priority': 'Medium',
                                      'Customer': 'ABC'}
            )
```
<span data-ttu-id="cbd22-198">Sie können „datetime“, „int“, „float“ oder „boolean“ verwenden.</span><span class="sxs-lookup"><span data-stu-id="cbd22-198">You can use datetime, int, float or boolean</span></span>

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
<span data-ttu-id="cbd22-199">Aus Gründen der Kompatibilität mit einer älteren Version dieser Bibliothek kann `broker_properties` auch als JSON-Zeichenfolge definiert werden.</span><span class="sxs-lookup"><span data-stu-id="cbd22-199">For compatibility reason with old version of this library, `broker_properties` could also be defined as a JSON string.</span></span>
<span data-ttu-id="cbd22-200">In diesem Fall müssen Sie eine gültige JSON-Zeichenfolge schreiben. Von Python wird vor der Übermittlung an die Rest-API keine Überprüfung ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="cbd22-200">If this situation, you're responsible to write a valid JSON string, no check will be made by Python before sending to the RestAPI.</span></span>

```python
broker_properties = '{"ForcePersistence": false, "Label": "My label"}'
sent_msg = Message(b'receive message',
                   broker_properties = broker_properties
)
```

## <a name="next-steps"></a><span data-ttu-id="cbd22-201">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="cbd22-201">Next Steps</span></span>
* [<span data-ttu-id="cbd22-202">Dokumentation zu Service Bus</span><span class="sxs-lookup"><span data-stu-id="cbd22-202">Service Bus documentation</span></span>](https://docs.microsoft.com/azure/service-bus-messaging)
* [<span data-ttu-id="cbd22-203">SDK-Quellcode</span><span class="sxs-lookup"><span data-stu-id="cbd22-203">SDK source code</span></span>](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus)
* [<span data-ttu-id="cbd22-204">SDK-Referenzdokumentation</span><span class="sxs-lookup"><span data-stu-id="cbd22-204">SDK reference documentation</span></span>](https://docs.microsoft.com/python/api/overview/azure/servicebus/client?view=azure-python)
* [<span data-ttu-id="cbd22-205">Weitere Beispiele</span><span class="sxs-lookup"><span data-stu-id="cbd22-205">Additional samples</span></span>](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus/examples)
