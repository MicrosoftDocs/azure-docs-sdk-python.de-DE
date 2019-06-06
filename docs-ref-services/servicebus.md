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
ms.openlocfilehash: 014f34b6ba3d3a2a8ce15afcd826195d6051f98a
ms.sourcegitcommit: 434186988284e0a8268a9de11645912a81226d6b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/29/2019
ms.locfileid: "66376766"
---
# <a name="service-bus-libraries-for-python"></a>Service Bus-Bibliotheken für Python

Microsoft Azure Service Bus unterstützt einen Satz cloudbasierter, nachrichtenorientierter Middlewaretechnologien, darunter zuverlässiges Message Queuing und dauerhaftes Veröffentlichungs-/Abonnementmessaging.

* [SDK-Quellcode](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus)
* [SDK-Referenzdokumentation](https://docs.microsoft.com/python/api/overview/azure/servicebus/client?view=azure-python)

## <a name="whats-new-in-v0500"></a>Neuerungen in v0.50.0

Ab Version 0.50.0 ist eine neue AMQP-basierte API zum Senden und Empfangen von Nachrichten verfügbar. Dieses Update umfasst **wichtige Änderungen**.

Erfahren Sie im Abschnitt zur [Migration von v0.21.1 zu v0.50.0](#migration-from-v0211-to-v0500), ob ein Upgrade für Sie zu diesem Zeitpunkt sinnvoll ist.

Mit der neuen AMQP-basierten API profitieren Sie von einer zuverlässigeren Nachrichtenübergabe sowie einer besseren Leistung und Unterstützung erweiterter Features.
Die neue API unterstützt zudem asynchrone Vorgänge (basierend auf Asyncio) für das Senden, Empfangen und Verarbeiten von Nachrichten.

Eine Dokumentation zu den älteren HTTP-basierten Vorgängen finden Sie im Abschnitt zur [Verwendung HTTP-basierter Vorgänge der Legacy-API](#using-http-based-operations-of-the-legacy-api).

## <a name="prerequisites"></a>Voraussetzungen

* Azure-Abonnement ([Erstellen Sie ein kostenloses Konto.](https://azure.microsoft.com/free/))
* Azure [Service Bus-Namespace und Anmeldeinformationen für die Verwaltung](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-create-namespace-portal)
* [Python 2.7-3.7](https://www.python.org/downloads/)

## <a name="installation"></a>Installation

```bash
pip install azure-servicebus
```

## <a name="connect-to-azure-service-bus"></a>Herstellen der Verbindung mit Azure Service Bus

### <a name="get-credentials"></a>Abrufen von Anmeldeinformationen

Verwenden Sie den folgenden Azure CLI-Codeausschnitt, um eine Umgebungsvariable mit der Service Bus-Verbindungszeichenfolge zu füllen (Sie finden diesen Wert auch im Azure-Portal). Der Ausschnitt ist für die Bash-Shell formatiert.

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

### <a name="create-client"></a>Erstellen des Clients

Nach dem Auffüllen der `SB_CONN_STR`-Umgebungsvariablen können Sie das ServiceBusClient-Element erstellen.

```python
import os
from azure.servicebus import ServiceBusClient

connection_str = os.environ['SB_CONN_STR']

sb_client = ServiceBusClient.from_connection_string(connection_str)
```

Verwenden Sie für asynchrone Vorgänge den `azure.servicebus.aio`-Namespace.

```python
import os
from azure.servicebus.aio import ServiceBusClient

connection_str = os.environ['SB_CONN_STR']

sb_client = ServiceBusClient.from_connection_string(connection_str)
```

## <a name="service-bus-queues"></a>Service Bus-Warteschlangen

Service Bus-Warteschlangen stellen eine Alternative zu Storage-Warteschlangen dar. Sie sind in Szenarien nützlich, in denen komplexere Messagingfeatures (größere Nachrichten, Nachrichtensortierung, einzelne schädliche Lesevorgänge, zeitgesteuerte Zustellung) mit pushbasierter Zustellung und langen Abrufvorgängen erforderlich sind.

### <a name="create-queue"></a>Erstellen einer Warteschlange

Dadurch wird eine neue Warteschlange im Service Bus-Namespace erstellt. Wenn innerhalb des Namespace bereits eine Warteschlange vorhanden ist, wird ein Fehler ausgelöst.

```python
sb_client.create_queue("MyQueue")
```

Sie können auch optionale Parameter festlegen, um das Verhalten der Warteschlange zu konfigurieren.

```python
sb_client.create_queue(
    "MySessionQueue",
    requires_session=True  # Create a sessionful queue
    max_delivery_count=5  # Max delivery attempts per message
)
```

### <a name="get-a-queue-client"></a>Abrufen eines Warteschlangenclients

Ein QueueClient-Element kann zum Senden und Empfangen von Nachrichten über die Warteschlange sowie für weitere Vorgänge verwendet werden.

```python
queue_client = sb_client.get_queue("MyQueue")
```

### <a name="sending-messages"></a>Senden von Nachrichten

Der Warteschlangenclient kann mehrere Nachrichten gleichzeitig senden:

```python
from azure.servicebus import Message

message = Message("Hello World")
queue_client.send(message)

message_one = Message("First")
message_two = Message("Second")
queue_client.send([message_one, message_two])
```

Bei jedem Aufruf von „QueueClient.send“ wird eine neue Dienstverbindung erstellt. Wenn Sie die gleiche Verbindung für mehrere Sendeaufrufe wiederverwenden möchten, können Sie einen Absender öffnen:

```python
message_one = Message("First")
message_two = Message("Second")

with queue_client.get_sender() as sender:
    sender.send(message_one)
    sender.send(message_two)
```

Wenn Sie einen asynchronen Client verwenden, nutzen die oben aufgeführten Vorgänge die Async-Syntax:

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

### <a name="receiving-messages"></a>Empfangen von Nachrichten

Nachrichten können als fortlaufender Iterator von einer Warteschlange empfangen werden. Der Standardmodus für den Empfang von Nachrichten ist [PeekLock](https://docs.microsoft.com/rest/api/servicebus/peek-lock-message-non-destructive-read). Jede Nachricht muss explizit abgeschlossen werden, damit sie aus der Warteschlange entfernt wird.

```python
messages = queue_client.get_receiver()
for message in messages:
    print(message)
    message.complete()
```

Die Dienstverbindung bleibt während des gesamten Iterators geöffnet. Wenn Sie den Nachrichtenstream nur teilweise durchlaufen, sollten Sie den Empfänger in einer `with`-Anweisung ausführen, um sicherzustellen, dass die Verbindung geschlossen wurde:

```python
with queue_client.get_receiver() as messages:
    for message in messages:
        print(message)
        message.complete()
        break
```
Wenn Sie einen asynchronen Client verwenden, nutzen die oben aufgeführten Vorgänge die Async-Syntax:

```python
async with queue_client.get_receiver() as messages:
    async for message in messages:
        print(message)
        await message.complete()
        break
```

## <a name="service-bus-topics-and-subscriptions"></a>Service Bus-Themen und -Abonnements

Service Bus-Themen und -Abonnements sind neben Service Bus-Warteschlangen eine weitere Abstraktion, die eine 1:n-Kommunikation mit dem Muster „Veröffentlichen/Abonnieren“ bereitstellt. Nachrichten werden an ein Thema gesendet und für mindestens ein zugeordnetes Abonnement bereitgestellt. Das ist für die Skalierung in Szenarien mit sehr vielen Benutzern hilfreich.

### <a name="create-topic"></a>Thema erstellen

Hiermit wird eine neues Thema im Service Bus-Namespace erstellt. Wenn bereits ein Thema mit dem gleichen Namen vorhanden ist, wird ein Fehler ausgelöst.

```python
sb_client.create_topic("MyTopic")
```

### <a name="get-a-topic-client"></a>Abrufen eines Themenclients

Ein TopicClient-Element kann zum Senden von Nachrichten an das Thema sowie für andere Vorgänge verwendet werden.

```python
topic_client = sb_client.get_topic("MyTopic")
```

### <a name="create-subscription"></a>Erstellen des Abonnements

Hiermit wird ein neues Abonnement für das angegebene Thema innerhalb des Service Bus-Namespace erstellt.

```python
sb_client.create_subscription("MyTopic", "MySubscription")
```

### <a name="get-a-subscription-client"></a>Abrufen eines Abonnementclients

Ein SubscriptionClient-Element kann zum Empfangen von Nachrichten aus der Warteschlange sowie für weitere Vorgänge verwendet werden.

```python
topic_client = sb_client.get_subscription("MyTopic", "MySubscription")
```

## <a name="migration-from-v0211-to-v0500"></a>Migration von v0.21.1 zu v0.50.0

In Version 0.50.0 wurden wichtige Änderungen eingeführt. Die ursprüngliche HTTP-basierte API ist auch in v0.50.0 weiterhin verfügbar. Jedoch ist sie jetzt unter einem neuen Namespace vorhanden: `azure.servicebus.control_client`.

### <a name="should-i-upgrade"></a>Sollte ich ein Upgrade durchführen?

Das neue Paket (v0.50.0) bietet keine Verbesserungen in HTTP-basierten Vorgängen über v0.21.1. Die HTTP-basierte API ist bis auf die Verfügbarkeit unter einem neuen Namespace identisch. Wenn Sie nur HTTP-basierte Vorgänge verwenden möchten (`create_queue`, `delete_queue` usw.), bietet Ihnen ein Upgrade zu diesem Zeitpunkt keine weiteren Vorteile.

### <a name="how-do-i-migrate-my-code-to-the-new-version"></a>Wie migriere ich meinen Code zur neuen Version?

Code, der für v0.21.0 geschrieben wird, kann durch einfaches Ändern des Import-Namespace zur Version 0.50.0 portiert werden:

```python
# from azure.servicebus import ServiceBusService  <- This will now raise an ImportError
from azure.servicebus.control_client import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

## <a name="using-http-based-operations-of-the-legacy-api"></a>Verwenden von HTTP-basierten Vorgängen der Legacy-API

Die folgende Dokumentation beschreibt die Legacy-API und sollte verwendet werden, wenn Sie vorhandenen Code zu v0.50.0 portieren möchten, ohne weitere Änderungen vorzunehmen. Diese Referenz kann auch als Leitfaden dienen, wenn Sie v0.21.1 verwenden.
Wenn Sie neuen Code schreiben, empfehlen wir Ihnen, die oben beschriebene neue API zu verwenden.

### <a name="service-bus-queues"></a>Service Bus-Warteschlangen

#### <a name="shared-access-signature-sas-authentication"></a>SAS-Authentifizierung (Shared Access Signature)

Wenn Sie SAS-Authentifizierung verwenden möchten, erstellen Sie den Service Bus-Dienst wie folgt:

```python
from azure.servicebus.control_client import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

#### <a name="access-control-service-acs-authentication"></a>ACS-Authentifizierung (Access Control Service)

ACS wird für neue Service Bus-Namespaces nicht unterstützt. Wir empfehlen das [Migrieren von Anwendungen zur SAS-Authentifizierung](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-migrate-acs-sas). Um die ACS-Authentifizierung in einem älteren Service Bus-Namespace zu verwenden, erstellen Sie ServiceBusService mit:

```python
from azure.servicebus.control_client import ServiceBusService

account_key = '' # DEFAULT KEY from Azure portal
issuer = 'owner' # DEFAULT ISSUER from Azure portal
sbs = ServiceBusService(service_namespace,
                        account_key=account_key,
                        issuer=issuer)
```

#### <a name="sending-and-receiving-messages"></a>Senden und Empfangen von Nachrichten

Mit der **create\_queue**-Methode können Sie sicherstellen, dass eine Warteschlange vorhanden ist:

```python
sbs.create_queue('taskqueue')
```

Anschließend kann die **send\_queue\_message**-Methode aufgerufen werden, um die Nachricht in die Warteschlange einzufügen:

```python
from azure.servicebus.control_client import Message

msg = Message('Hello World!')
sbs.send_queue_message('taskqueue', msg)
```

Dann können Sie die **send\_queue\_message_batch**-Methode aufrufen, um mehrere Nachrichten auf einmal zu senden:

```python
from azure.servicebus.control_client import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
```

Anschließend kann die **receive\_queue\_message**-Methode aufgerufen werden, um die Nachricht aus der Warteschlange zu entfernen.

```python
msg = sbs.receive_queue_message('taskqueue')
```

### <a name="service-bus-topics"></a>Service Bus-Themen

Mit der **create\_topic**-Methode können Sie ein Thema auf Serverseite erstellen:

```python
sbs.create_topic('taskdiscussion')
```

Mit der **send\_topic\_message**-Methode kann eine Nachricht an ein Thema gesendet werden:

```python
from azure.servicebus.control_client import Message

msg = Message(b'Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
```

Mit der **send\_topic\_message_batch**-Methode können mehrere Nachrichten auf einmal gesendet werden:

```python
from azure.servicebus.control_client import Message

msg1 = Message(b'Hello World!')
msg2 = Message(b'Hello World again!')
sbs.send_topic_message_batch('taskdiscussion', [msg1, msg2])
```

Beachten Sie, dass in Python 3 eine str-Nachricht UFT-8-codiert ist and Sie die Codierung in Python 2 selbst verwalten müssen.

Ein Client kann dann ein Abonnement erstellen und mit der Verarbeitung von Nachrichten beginnen, indem er die **create\_subscription**-Methode gefolgt von der **receive\_subscription\_message**-Methode aufruft. Beachten Sie, dass vor dem Erstellen des Abonnements gesendete Nachrichten nicht empfangen werden.

```python
from azure.servicebus.control_client import Message

sbs.create_subscription('taskdiscussion', 'client1')
msg = Message('Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
msg = sbs.receive_subscription_message('taskdiscussion', 'client1')
```

### <a name="event-hub"></a>Event Hub

Event Hubs ermöglichen die Erfassung von Ereignisströmen bei hohem Durchsatz von unterschiedlichen Geräten und Diensten.

Mit der **create\_event\_hub**-Methode können Sie einen Event Hub erstellen:

```python
sbs.create_event_hub('myhub')
```

So senden Sie ein Ereignis:

```python
sbs.send_event('myhub', '{ "DeviceId":"dev-01", "Temperature":"37.0" }')
```

Der Ereignisinhalt ist die Ereignisnachricht oder eine JSON-codierte Zeichenfolge mit mehreren Nachrichten.

### <a name="advanced-features"></a>Erweiterte Funktionen

#### <a name="broker-properties-and-user-properties"></a>Brokereigenschaften und Benutzereigenschaften

In diesem Abschnitt wird die Verwendung der [hier](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties) beschriebenen Broker- und Benutzereigenschaften erläutert:

```python
sent_msg = Message(b'This is the third message',
                   broker_properties={'Label': 'M3'},
                   custom_properties={'Priority': 'Medium',
                                      'Customer': 'ABC'}
            )
```

Sie können „datetime“, „int“, „float“ oder „boolean“ verwenden.

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

Aus Gründen der Kompatibilität mit einer älteren Version dieser Bibliothek kann `broker_properties` auch als JSON-Zeichenfolge definiert werden.
In diesem Fall müssen Sie eine gültige JSON-Zeichenfolge schreiben. Von Python wird vor der Übermittlung an die Rest-API keine Überprüfung ausgeführt.

```python
broker_properties = '{"ForcePersistence": false, "Label": "My label"}'
sent_msg = Message(b'receive message',
                   broker_properties = broker_properties
)
```

## <a name="next-steps"></a>Nächste Schritte

* [Dokumentation zu Service Bus](https://docs.microsoft.com/azure/service-bus-messaging)
* [SDK-Quellcode](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus)
* [SDK-Referenzdokumentation](https://docs.microsoft.com/python/api/overview/azure/servicebus/client?view=azure-python)
* [Weitere Beispiele](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus/examples)
