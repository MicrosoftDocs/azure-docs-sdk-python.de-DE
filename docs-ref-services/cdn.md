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
ms.openlocfilehash: 92d6dd6ce55964bc48bb9bc654e8dec25f6b8344
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
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
