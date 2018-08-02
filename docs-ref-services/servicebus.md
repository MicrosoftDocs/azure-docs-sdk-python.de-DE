---
title: Service Bus-Bibliotheken für Python
description: Referenzdokumentation für die Python-Clientbibliotheken und -Verwaltungsbibliotheken für Service Bus
keywords: Azure, Python, SDK, API, Messaging, PubSub, Pub-Sub, Nachrichtenbroker
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.devlang: python
ms.service: service-bus
ms.openlocfilehash: 02c172ff1a54d060c6af36a5a5daa5dcbff8795c
ms.sourcegitcommit: e35ec475d4b9d8061d0528a93aa8e1c4b7db6c0d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/02/2018
ms.locfileid: "39418955"
---
# <a name="service-bus-libraries-for-python"></a>Service Bus-Bibliotheken für Python

## <a name="overview"></a>Übersicht

Microsoft Azure Service Bus unterstützt einen Satz cloudbasierter, nachrichtenorientierter Middlewaretechnologien, darunter zuverlässiges Message Queuing und dauerhaftes Veröffentlichungs-/Abonnementmessaging. 

## <a name="install-the-libraries"></a>Installieren der Bibliotheken
```bash
pip install azure-servicebus
```

## <a name="servicebus-queues"></a>ServiceBus-Warteschlangen
ServiceBus-Warteschlangen stellen eine Alternative zu Storage-Warteschlangen dar. Sie sind in Szenarien nützlich, in denen komplexere Messagingfeatures (größere Nachrichten, Nachrichtensortierung, einzelne schädliche Lesevorgänge, zeitgesteuerte Zustellung) mit pushbasierter Zustellung und langen Abrufvorgängen erforderlich sind.

Der Dienst kann SAS-Authentifizierung (Shared Access Signature) oder ACS-Authentifizierung nutzen.

Für Service Bus-Namespaces, die nach August 2014 über das Azure-Portal erstellt wurden, wird die ACS-Authentifizierung nicht mehr unterstützt. Sie können mit dem Azure SDK Namespaces erstellen, die mit ACS kompatibel sind.

### <a name="shared-access-signature-authentication"></a>SAS-Authentifizierung (Shared Access Signature)

Wenn Sie SAS-Authentifizierung verwenden möchten, erstellen Sie den Service Bus-Dienst wie folgt:

```python
from azure.servicebus import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

### <a name="acs-authentication"></a>ACS-Authentifizierung

Wenn Sie ACS-Authentifizierung verwenden möchten, erstellen Sie den Service Bus-Dienst wie folgt:

```python
from azure.servicebus import ServiceBusService

account_key = '' # DEFAULT KEY from Azure portal
issuer = 'owner' # DEFAULT ISSUER from Azure portal
sbs = ServiceBusService(service_namespace,
                        account_key=account_key,
                        issuer=issuer)
```
### <a name="sending-and-receiving-messages"></a>Senden und Empfangen von Nachrichten

Mit der **create\_queue**-Methode können Sie sicherstellen, dass eine Warteschlange vorhanden ist:

```python
sbs.create_queue('taskqueue')
```
Anschließend kann die **send\_queue\_message**-Methode aufgerufen werden, um die Nachricht in die Warteschlange einzufügen:

```python
from azure.servicebus import Message

msg = Message('Hello World!')
sbs.send_queue_message('taskqueue', msg)
```
Dann können Sie die **send\_queue\_message_batch**-Methode aufrufen, um mehrere Nachrichten auf einmal zu senden:

```python
from azure.servicebus import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
```
Anschließend kann die **receive\_queue\_message**-Methode aufgerufen werden, um die Nachricht aus der Warteschlange zu entfernen.

```python
msg = sbs.receive_queue_message('taskqueue')
```

## <a name="servicebus-topics"></a>ServiceBus-Themen

ServiceBus-Themen sind (neben ServiceBus-Warteschlangen) eine weitere Abstraktion, die die Implementierung von Pub/Sub-Szenarien vereinfacht.

Mit der **create\_topic**-Methode können Sie ein Thema auf Serverseite erstellen:

```python
sbs.create_topic('taskdiscussion')
```
Mit der **send\_topic\_message**-Methode kann eine Nachricht an ein Thema gesendet werden:

```python
from azure.servicebus import Message

msg = Message(b'Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
```

Mit der **send\_topic\_message_batch**-Methode können mehrere Nachrichten auf einmal gesendet werden:

```python
from azure.servicebus import Message

msg1 = Message(b'Hello World!')
msg2 = Message(b'Hello World again!')
sbs.send_topic_message_batch('taskdiscussion', [msg1, msg2])
```

Beachten Sie, dass in Python 3 eine str-Nachricht UFT-8-codiert ist and Sie die Codierung in Python 2 selbst verwalten müssen.

Ein Client kann dann ein Abonnement erstellen und mit der Verarbeitung von Nachrichten beginnen, indem er die **create\_subscription**-Methode gefolgt von der **receive\_subscription\_message**-Methode aufruft. Beachten Sie, dass vor dem Erstellen des Abonnements gesendete Nachrichten nicht empfangen werden.

```python
from azure.servicebus import Message

sbs.create_subscription('taskdiscussion', 'client1')
msg = Message('Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
msg = sbs.receive_subscription_message('taskdiscussion', 'client1')
```

## <a name="event-hub"></a>Event Hub

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

## <a name="advanced-features"></a>Erweiterte Funktionen

### <a name="broker-properties-and-user-properties"></a>Brokereigenschaften und Benutzereigenschaften

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

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/servicebus/management)
