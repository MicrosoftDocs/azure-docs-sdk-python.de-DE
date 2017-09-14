---
title: "Azure CDN-Bibliotheken für Python"
description: "Referenz zu Azure CDN-Bibliotheken für Python"
keywords: Azure, Python, SDK, API, CDN
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 07/10/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: c704b32ff5fd6db922ef9c296142832455088562
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cdn-libraries-for-python"></a>Azure CDN-Bibliotheken für Python

## <a name="overview"></a>Übersicht

[Azure Content Delivery Network (CDN)](https://docs.microsoft.com/en-us/azure/cdn/cdn-overview) ermöglicht die Bereitstellung von Caches für Webinhalte, um die weltweite Verfügbarkeit von hoher Bandbreite zu gewährleisten.

Informationen zu den ersten Schritten mit Azure CDN finden Sie unter [Erste Schritte mit Azure CDN](https://docs.microsoft.com/en-us/azure/cdn/cdn-create-new-endpoint).

## <a name="management-apis"></a>Verwaltungs-APIs

Mit der Verwaltungs-API können Sie Azure CDNs erstellen, abfragen und verwalten.

Installieren Sie das Verwaltungspaket über pip.

```bash
pip install azure-mgmt-cdn
```

### <a name="example"></a>Beispiel

Erstellen eines CDN-Profils mit einem definierten Endpunkt:

```python
from azure.mgmt.cdn import CdnManagementClient

cdn_client = CdnManagementClient(credentials, 'your-subscription-id')
profile_poller = cdn_client.profiles.create('my-resource-group',
                                            'cdn-name',
                                            {
                                                "location": "some_region", 
                                                "sku": {
                                                    "name": "sku_tier"
                                                } 
                                            })
profile = profile_poller.result()

endpoint_poller = client.endpoints.create('my-resource-group',
                                          'cdn-name',
                                          'unique-endpoint-name', 
                                          { 
                                              "location": "any_region", 
                                              "origins": [
                                                  {
                                                      "name": "origin_name", 
                                                      "host_name": "url"
                                                  }]
                                          })
endpoint = endpoint_poller.result()
```

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/cdn/managementlibrary)
