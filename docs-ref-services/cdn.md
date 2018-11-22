---
title: Azure CDN-Bibliotheken für Python
description: Referenz zu Azure CDN-Bibliotheken für Python
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
ms.openlocfilehash: 06e6c8786ebbd88b7d3996b640af96a23cd5689b
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2018
ms.locfileid: "52275534"
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
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/cdn/management)
