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
# <a name="azure-dns-libraries-for-python"></a>Azure DNS-Bibliotheken für Python

## <a name="overview"></a>Übersicht

[Azure DNS](/azure/dns/dns-overview) ist ein Hostingdienst für DNS-Domänen, der die DNS-Auflösung über die Microsoft Azure-Infrastruktur durchführt.

Informationen zu den ersten Schritten mit Azure DNS finden Sie unter [Erste Schritte mit Azure DNS im Azure-Portal](/azure/dns/dns-getstarted-portal).

## <a name="management-apis"></a>Verwaltungs-APIs

Erstellen und verwalten Sie mit der Verwaltungs-API DNS-Zonen und -Einträge.

Installieren Sie das Verwaltungspaket mit pip.

```bash
pip install azure-mgmt-dns
```

### <a name="example"></a>Beispiel

Erstellen Sie eine neue DNS-Zone:

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
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/dns/managementlibrary)
