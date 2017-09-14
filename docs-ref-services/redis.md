---
title: "Azure Redis-Bibliotheken für Python"
description: "Referenzdokumentation für die Python-Clientbibliotheken für Redis"
keywords: Azure, Python, Redis, API, SDK, Datenbank, NoSQL
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 06/26/2017
ms.topic: article
ms.devlang: python
ms.service: redis
ms.openlocfilehash: 3ba8d972e91fad229c1489800edeca08760254e6
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2017
---
# <a name="azure-redis-cache-libraries-for-python"></a>Azure Redis Cache-Bibliotheken für Python

## <a name="overview"></a>Übersicht

Azure Redis Cache basiert auf dem beliebten Open Source-Redis-Projekt. Sie erhalten Zugriff auf eine sichere, dedizierte Redis-Instanz, die von Microsoft verwaltet wird und auf die aus Ihren Azure-Apps zugegriffen werden kann.

Redis ist ein erweiterter Schlüsselwertspeicher, bei dem Schlüssel Datenstrukturen wie Zeichenfolgen, Hashes, Listen, Sätze und sortierte Sätze enthalten können. Redis unterstützt einen Satz automatischer Vorgänge für diese Datentypen.

Informieren Sie sich über [Azure Redis Cache](https://docs.microsoft.com/azure/redis-cache/).

## <a name="management-api"></a>Verwaltungs-API

Über die Redis-Verwaltungs-API können Sie die Redis-Ressourcen in Ihrem Abonnement erstellen und verwalten.

```bash
pip install redis
pip install azure-mgmt-redis
```

### <a name="example"></a>Beispiel

Im folgenden Beispiel wird ein neuer Redis-Cache erstellt:

```python
from azure.mgmt.redis import RedisManagementClient
from azure.mgmt.redis.models import Sku, RedisCreateOrUpdateParameters

redis_client = RedisManagementClient(
    credentials,
    subscription_id
)
group_name = 'myresourcegroup'
cache_name = 'mycachename'
redis_cache = redis_client.redis.create_or_update(
    group_name,
    cache_name,
    RedisCreateOrUpdateParameters(
        sku = Sku(name = 'Basic', family = 'C', capacity = '1'),
        location = "East US"
    )
)
# redis_cache is a RedisResourceWithAccessKey instance
```

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/redis/managementlibrary)

