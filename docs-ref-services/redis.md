---
title: Azure Redis-Bibliotheken für Python
description: Referenzdokumentation für die Python-Clientbibliotheken für Redis
keywords: Azure, Python, Redis, API, SDK, Datenbank, NoSQL
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 06/26/2017
ms.topic: article
ms.devlang: python
ms.service: redis
ms.openlocfilehash: c2f8ebcbcbd7b71c1fa96e46a8148a3c0b88877f
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
ms.locfileid: "29479243"
---
# <a name="azure-redis-cache-libraries-for-python"></a><span data-ttu-id="54dd4-104">Azure Redis Cache-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="54dd4-104">Azure Redis Cache libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="54dd4-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="54dd4-105">Overview</span></span>

<span data-ttu-id="54dd4-106">Azure Redis Cache basiert auf dem beliebten Open Source-Redis-Projekt.</span><span class="sxs-lookup"><span data-stu-id="54dd4-106">Azure Redis Cache is based on the popular open source Redis project.</span></span> <span data-ttu-id="54dd4-107">Sie erhalten Zugriff auf eine sichere, dedizierte Redis-Instanz, die von Microsoft verwaltet wird und auf die aus Ihren Azure-Apps zugegriffen werden kann.</span><span class="sxs-lookup"><span data-stu-id="54dd4-107">It gives you access to a secure, dedicated Redis instance, managed by Microsoft and accessible from your Azure apps.</span></span>

<span data-ttu-id="54dd4-108">Redis ist ein erweiterter Schlüsselwertspeicher, bei dem Schlüssel Datenstrukturen wie Zeichenfolgen, Hashes, Listen, Sätze und sortierte Sätze enthalten können.</span><span class="sxs-lookup"><span data-stu-id="54dd4-108">Redis is an advanced key-value store, where keys can contain data structures such as strings, hashes, lists, sets, and sorted sets.</span></span> <span data-ttu-id="54dd4-109">Redis unterstützt einen Satz automatischer Vorgänge für diese Datentypen.</span><span class="sxs-lookup"><span data-stu-id="54dd4-109">Redis supports a set of atomic operations on these data types.</span></span>

<span data-ttu-id="54dd4-110">Informieren Sie sich über [Azure Redis Cache](https://docs.microsoft.com/azure/redis-cache/).</span><span class="sxs-lookup"><span data-stu-id="54dd4-110">Learn more about [Azure Redis Cache](https://docs.microsoft.com/azure/redis-cache/).</span></span>

## <a name="management-api"></a><span data-ttu-id="54dd4-111">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="54dd4-111">Management API</span></span>

<span data-ttu-id="54dd4-112">Über die Redis-Verwaltungs-API können Sie die Redis-Ressourcen in Ihrem Abonnement erstellen und verwalten.</span><span class="sxs-lookup"><span data-stu-id="54dd4-112">Create and manage your Redis resources in your subscription with the Redis management API.</span></span>

```bash
pip install redis
pip install azure-mgmt-redis
```

### <a name="example"></a><span data-ttu-id="54dd4-113">Beispiel</span><span class="sxs-lookup"><span data-stu-id="54dd4-113">Example</span></span>

<span data-ttu-id="54dd4-114">Im folgenden Beispiel wird ein neuer Redis-Cache erstellt:</span><span class="sxs-lookup"><span data-stu-id="54dd4-114">The following example creates a new Redis cache:</span></span>

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
> [<span data-ttu-id="54dd4-115">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="54dd4-115">Explore the Management APIs</span></span>](/python/api/overview/azure/redis/management)

