---
title: "Azure-Netzwerk-Bibliotheken für Python"
description: "Referenz zu Azure-Netzwerk-Bibliotheken für Python"
keywords: Azure, Python, SDK, API, Netzwerk
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 07/10/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: ed6ddfe4d1f4d860952369a75e10166a1f22c483
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2017
---
# <a name="azure-network-libraries-for-python"></a>Azure-Netzwerk-Bibliotheken für Python

## <a name="overview"></a>Übersicht

[Azure Virtual Network](/azure/virtual-network/virtual-networks-overview) ermöglicht das Herstellen einer Verbindung mit Azure-Ressourcen sowie das Herstellen einer Verbindung zwischen den Ressourcen und Ihrem lokalen Netzwerk.

Informationen zu den ersten Schritten mit Azure Virtual Network finden Sie unter [Erstellen Ihres ersten virtuellen Netzwerks](/azure/virtual-network/virtual-network-get-started-vnet-subnet).

## <a name="management-apis"></a>Verwaltungs-APIs

Mit den Verwaltungs-APIs können Sie virtuelle Azure-Netzwerke überprüfen, verwalten und konfigurieren.

Im Gegensatz zu anderen Azure-Python-APIs stehen für Netzwerk-APIs explizite versionsspezifische Pakete zur Verfügung. Sie müssen sie nicht einzeln importieren, da die Paketinformationen im Clientkonstruktor angegeben sind.

Installieren Sie das Verwaltungspaket mit pip.

```bash
pip install azure-mgmt-network
```

### <a name="example"></a>Beispiel

Erstellen eines virtuellen Netzwerks und eines zugewiesenen Subnetzes:

```python
from azure.mgmt.network import NetworkManagementClient

GROUP_NAME = 'resource-group'
VNET_NAME = 'your-vnet-identifier'
LOCATION = 'region'
SUBNET_NAME = 'your-subnet-identifier'

network_client = NetworkManagementClient(credentials, 'your-subscription-id')

async_vnet_creation = network_client.virtual_networks.create_or_update(
    GROUP_NAME,
    VNET_NAME,
    {
        'location': LOCATION,
        'address_space': {
            'address_prefixes': ['10.0.0.0/16']
        }
    }
)
async_vnet_creation.wait()

# Create Subnet
async_subnet_creation = network_client.subnets.create_or_update(
    GROUP_NAME,
    VNET_NAME,
    SUBNET_NAME,
    {'address_prefix': '10.0.0.0/24'}
)
subnet_info = async_subnet_creation.result()
```

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/network/managementlibrary)

### <a name="samples"></a>Beispiele

* [Erste Schritte mit Azure Resource Manager für Lastenausgleichsmodule in Python][1]

Zeigen Sie die [vollständige Liste](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=virtual%20network) von Beispielen für Azure Virtual Network an.

[1]: [https://azure.microsoft.com/en-us/resources/samples/network-python-manage-loadbalancer/]
