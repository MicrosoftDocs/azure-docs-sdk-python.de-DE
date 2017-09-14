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
# <a name="service-bus-libraries-for-python"></a><span data-ttu-id="67aa4-104">Service Bus-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="67aa4-104">Service Bus libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="67aa4-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="67aa4-105">Overview</span></span>

<span data-ttu-id="67aa4-106">Microsoft Azure Service Bus unterstützt einen Satz cloudbasierter, nachrichtenorientierter Middlewaretechnologien, darunter zuverlässiges Message Queuing und dauerhaftes Veröffentlichungs-/Abonnementmessaging.</span><span class="sxs-lookup"><span data-stu-id="67aa4-106">Microsoft Azure Service Bus supports a set of cloud-based, message-oriented middleware technologies including reliable message queuing and durable publish/subscribe messaging.</span></span> 

## <a name="install-the-libraries"></a><span data-ttu-id="67aa4-107">Installieren der Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="67aa4-107">Install the libraries</span></span>
```bash
pip install azure-mgmt-servicebus
```

## <a name="example"></a><span data-ttu-id="67aa4-108">Beispiel</span><span class="sxs-lookup"><span data-stu-id="67aa4-108">Example</span></span>
<span data-ttu-id="67aa4-109">Senden von Nachrichten an eine Warteschlange</span><span class="sxs-lookup"><span data-stu-id="67aa4-109">Send messages to a queue.</span></span>

```python
from azure.servicebus import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
# dequeue the message
msg = sbs.receive_queue_message('taskqueue')
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="67aa4-110">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="67aa4-110">Explore the Management APIs</span></span>](/python/api/overview/azure/servicebus/managementlibrary)

