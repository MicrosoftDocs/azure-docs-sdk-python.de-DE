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
# <a name="azure-dns-libraries-for-python"></a>Azure DNS-Bibliotheken für Python

## <a name="overview"></a>Übersicht

[Azure DNS](/azure/dns/dns-overview) ist ein Hostingdienst für DNS-Domänen, der die DNS-Auflösung über die Microsoft Azure-Infrastruktur durchführt.

Informationen zu den ersten Schritten mit Azure DNS finden Sie unter [Erste Schritte mit Azure DNS im Azure-Portal](/azure/dns/dns-getstarted-portal).

## <a name="management-apipythonapioverviewazurednsmanagement"></a>[Verwaltungs-API](/python/api/overview/azure/dns/management)

```bash
pip install azure-mgmt-dns
```

## <a name="create-the-management-client"></a>Erstellen des Verwaltungsclients

Der folgende Code erstellt eine Instanz des Verwaltungsclients.

Sie müssen Ihre ``subscription_id`` angeben. Diese ID kann aus der [Abonnementliste](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping) abgerufen werden.

Informationen zur Azure Active Directory-Authentifizierung mit dem Python SDK sowie zum Erstellen einer ``Credentials``-Instanz finden Sie im Artikel zur [Authentifizierung bei der Ressourcenverwaltung](/python/azure/python-sdk-azure-authenticate).

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

## <a name="create-dns-zone"></a>Erstellen einer DNS-Zone
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
    
## <a name="create-a-record-set"></a>Erstellen einer Datensatzgruppe
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
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/dns/management)
