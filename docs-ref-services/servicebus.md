---
title: "Service Bus-Bibliotheken für Python"
description: "Referenzdokumentation für die Python-Clientbibliotheken und -Verwaltungsbibliotheken für Service Bus"
keywords: Azure, Python, SDK, API, Messaging, PubSub, Pub-Sub, Nachrichtenbroker
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/26/2017
ms.topic: article
ms.devlang: python
ms.service: service-bus
ms.openlocfilehash: bf7be945f2c7a3daea93ff4e5b770459c00632c8
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2017
---
# <a name="service-bus-libraries-for-python"></a>Service Bus-Bibliotheken für Python

## <a name="overview"></a>Übersicht

Microsoft Azure Service Bus unterstützt einen Satz cloudbasierter, nachrichtenorientierter Middlewaretechnologien, darunter zuverlässiges Message Queuing und dauerhaftes Veröffentlichungs-/Abonnementmessaging. 

## <a name="install-the-libraries"></a>Installieren der Bibliotheken
```bash
pip install azure-mgmt-servicebus
```

## <a name="example"></a>Beispiel
Senden von Nachrichten an eine Warteschlange

```python
from azure.servicebus import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
# dequeue the message
msg = sbs.receive_queue_message('taskqueue')
```
> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/servicebus/managementlibrary)

