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
ms.openlocfilehash: 59ae3628b4a810db8fee21aacf46c13054dc8cd3
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2017
---
# <a name="azure-dns-libraries-for-python"></a><span data-ttu-id="652f1-104">Azure DNS-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="652f1-104">Azure DNS libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="652f1-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="652f1-105">Overview</span></span>

<span data-ttu-id="652f1-106">[Azure DNS](/azure/dns/dns-overview) ist ein Hostingdienst für DNS-Domänen, der die DNS-Auflösung über die Microsoft Azure-Infrastruktur durchführt.</span><span class="sxs-lookup"><span data-stu-id="652f1-106">[Azure DNS](/azure/dns/dns-overview) is a hosting service for DNS domains that provides DNS resolution via the Azure infrastructure.</span></span>

<span data-ttu-id="652f1-107">Informationen zu den ersten Schritten mit Azure DNS finden Sie unter [Erste Schritte mit Azure DNS im Azure-Portal](/azure/dns/dns-getstarted-portal).</span><span class="sxs-lookup"><span data-stu-id="652f1-107">To get started with Azure DNS, see [Get started with Azure DNS using the Azure portal](/azure/dns/dns-getstarted-portal).</span></span>

## <a name="management-apis"></a><span data-ttu-id="652f1-108">Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="652f1-108">Management APIs</span></span>

<span data-ttu-id="652f1-109">Erstellen und verwalten Sie mit der Verwaltungs-API DNS-Zonen und -Einträge.</span><span class="sxs-lookup"><span data-stu-id="652f1-109">Create and manage DNS zones and records with the management API.</span></span>

<span data-ttu-id="652f1-110">Installieren Sie das Verwaltungspaket mit pip.</span><span class="sxs-lookup"><span data-stu-id="652f1-110">Install the management package with pip.</span></span>

```bash
pip install azure-mgmt-dns
```

### <a name="example"></a><span data-ttu-id="652f1-111">Beispiel</span><span class="sxs-lookup"><span data-stu-id="652f1-111">Example</span></span>

<span data-ttu-id="652f1-112">Erstellen Sie eine neue DNS-Zone:</span><span class="sxs-lookup"><span data-stu-id="652f1-112">Create a new DNS zone.</span></span>

```python
from azure.mgmt.dns import DnsManagementClient

dns_client = DnsManagementClient(credentials, 'your-subscription-id')
zone = dns_client.zones.create_or_update('resource-group',
                                         'zone_name_no_dot',
                                         {
                                            "location": "global"
                                         })

```

> [!div class="nextstepaction"]
> [<span data-ttu-id="652f1-113">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="652f1-113">Explore the Management APIs</span></span>](/python/api/overview/azure/dns/managementlibrary)
