---
title: "Azure DNS-Bibliotheken für Python"
description: "Referenz zu Azure DNS-Bibliotheken für Python"
keywords: Azure, Python, SDK, API, DNS
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 07/10/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 294373469b1792821253ae46ab51fa0c06a74ffa
ms.sourcegitcommit: d7c26ac167cf6a6491358ac3153f268bc90e55e9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/24/2018
---
# <a name="azure-dns-libraries-for-python"></a><span data-ttu-id="d64ff-104">Azure DNS-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="d64ff-104">Azure DNS libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="d64ff-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="d64ff-105">Overview</span></span>

<span data-ttu-id="d64ff-106">[Azure DNS](/azure/dns/dns-overview) ist ein Hostingdienst für DNS-Domänen, der die DNS-Auflösung über die Microsoft Azure-Infrastruktur durchführt.</span><span class="sxs-lookup"><span data-stu-id="d64ff-106">[Azure DNS](/azure/dns/dns-overview) is a hosting service for DNS domains that provides DNS resolution via the Azure infrastructure.</span></span>

<span data-ttu-id="d64ff-107">Informationen zu den ersten Schritten mit Azure DNS finden Sie unter [Erste Schritte mit Azure DNS im Azure-Portal](/azure/dns/dns-getstarted-portal).</span><span class="sxs-lookup"><span data-stu-id="d64ff-107">To get started with Azure DNS, see [Get started with Azure DNS using the Azure portal](/azure/dns/dns-getstarted-portal).</span></span>

## <a name="management-apipythonapioverviewazurednsmanagement"></a>[<span data-ttu-id="d64ff-108">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="d64ff-108">Management API</span></span>](/python/api/overview/azure/dns/management)

```bash
pip install azure-mgmt-dns
```

## <a name="create-the-management-client"></a><span data-ttu-id="d64ff-109">Erstellen des Verwaltungsclients</span><span class="sxs-lookup"><span data-stu-id="d64ff-109">Create the management client</span></span>

<span data-ttu-id="d64ff-110">Der folgende Code erstellt eine Instanz des Verwaltungsclients.</span><span class="sxs-lookup"><span data-stu-id="d64ff-110">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="d64ff-111">Sie müssen Ihre ``subscription_id`` angeben. Diese ID kann aus der [Abonnementliste](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping) abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="d64ff-111">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="d64ff-112">Informationen zur Azure Active Directory-Authentifizierung mit dem Python SDK sowie zum Erstellen einer ``Credentials``-Instanz finden Sie im Artikel zur [Authentifizierung bei der Ressourcenverwaltung](/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="d64ff-112">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python 
from azure.mgmt.dns import DnsManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

dns_client = DnsManagementClient(
    credentials,
    subscription_id
)
```

## <a name="create-dns-zone"></a><span data-ttu-id="d64ff-113">Erstellen einer DNS-Zone</span><span class="sxs-lookup"><span data-stu-id="d64ff-113">Create DNS zone</span></span>
```python
# The only valid value is 'global', otherwise you will get a:
# The subscription is not registered for the resource type 'dnszones' in the location 'westus'.
zone = dns_client.zones.create_or_update(
    'MyResourceGroup',
    'pydns.com',
    {
        'location': 'global'
    }
)
```
    
## <a name="create-a-record-set"></a><span data-ttu-id="d64ff-114">Erstellen einer Datensatzgruppe</span><span class="sxs-lookup"><span data-stu-id="d64ff-114">Create a Record Set</span></span>
```python
record_set = dns_client.record_sets.create_or_update(
    'MyResourceGroup',
    'pydns.com',
    'MyRecordSet',
    'A',
    {
            "ttl": 300,
            "arecords": [
                {
                "ipv4_address": "1.2.3.4"
                },
                {
                "ipv4_address": "1.2.3.5"
                }
            ]
    }
)
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="d64ff-115">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="d64ff-115">Explore the Management APIs</span></span>](/python/api/overview/azure/dns/management)
