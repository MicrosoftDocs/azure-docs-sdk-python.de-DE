---
title: Azure-Netzwerk-Bibliotheken für Python
description: Referenz zu Azure-Netzwerk-Bibliotheken für Python
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
ms.openlocfilehash: f468f844becc2f0fe07d892c725c00df4669f4e3
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2018
ms.locfileid: "52273026"
---
# <a name="azure-network-libraries-for-python"></a><span data-ttu-id="d2fbe-104">Azure-Netzwerk-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="d2fbe-104">Azure Network libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="d2fbe-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="d2fbe-105">Overview</span></span>

<span data-ttu-id="d2fbe-106">[Azure Virtual Network](/azure/virtual-network/virtual-networks-overview) ermöglicht das Herstellen einer Verbindung mit Azure-Ressourcen sowie das Herstellen einer Verbindung zwischen den Ressourcen und Ihrem lokalen Netzwerk.</span><span class="sxs-lookup"><span data-stu-id="d2fbe-106">[Azure Virtual Network](/azure/virtual-network/virtual-networks-overview) allows you to connect Azure resources, and also connect them to your on-premises network.</span></span>

<span data-ttu-id="d2fbe-107">Informationen zu den ersten Schritten mit Azure Virtual Network finden Sie unter [Erstellen Ihres ersten virtuellen Netzwerks](/azure/virtual-network/virtual-network-get-started-vnet-subnet).</span><span class="sxs-lookup"><span data-stu-id="d2fbe-107">To get started with Azure Virtual Network, see [Create your first virtual network](/azure/virtual-network/virtual-network-get-started-vnet-subnet).</span></span>

## <a name="management-apis"></a><span data-ttu-id="d2fbe-108">Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="d2fbe-108">Management APIs</span></span>

<span data-ttu-id="d2fbe-109">Mit den Verwaltungs-APIs können Sie virtuelle Azure-Netzwerke überprüfen, verwalten und konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="d2fbe-109">Inspect, manage, and configure Azure virtual networks with the management APIs.</span></span>

<span data-ttu-id="d2fbe-110">Im Gegensatz zu anderen Azure-Python-APIs stehen für Netzwerk-APIs explizite versionsspezifische Pakete zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="d2fbe-110">Unlike other Azure python APIs, the networking APIs are explicitly versioned into separage packages.</span></span> <span data-ttu-id="d2fbe-111">Sie müssen sie nicht einzeln importieren, da die Paketinformationen im Clientkonstruktor angegeben sind.</span><span class="sxs-lookup"><span data-stu-id="d2fbe-111">You do not need to import them individually since the package information is specified in the client constructor.</span></span>

<span data-ttu-id="d2fbe-112">Installieren Sie das Verwaltungspaket mit pip.</span><span class="sxs-lookup"><span data-stu-id="d2fbe-112">Install the management package with pip.</span></span>

```bash
pip install azure-mgmt-network
```

### <a name="example"></a><span data-ttu-id="d2fbe-113">Beispiel</span><span class="sxs-lookup"><span data-stu-id="d2fbe-113">Example</span></span>

<span data-ttu-id="d2fbe-114">Erstellen eines virtuellen Netzwerks und eines zugewiesenen Subnetzes:</span><span class="sxs-lookup"><span data-stu-id="d2fbe-114">Create a virtual network and an associated subnet.</span></span>

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
> [<span data-ttu-id="d2fbe-115">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="d2fbe-115">Explore the Management APIs</span></span>](/python/api/overview/azure/network/management)

### <a name="samples"></a><span data-ttu-id="d2fbe-116">Beispiele</span><span class="sxs-lookup"><span data-stu-id="d2fbe-116">Samples</span></span>

* [<span data-ttu-id="d2fbe-117">Erste Schritte mit Azure Resource Manager für Lastenausgleichsmodule in Python</span><span class="sxs-lookup"><span data-stu-id="d2fbe-117">Getting started with Azure Resource Manager for load balancers in Python</span></span>](https://azure.microsoft.com/en-us/resources/samples/network-python-manage-loadbalancer/)

<span data-ttu-id="d2fbe-118">Zeigen Sie die [vollständige Liste](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=virtual%20network) von Beispielen für Azure Virtual Network an.</span><span class="sxs-lookup"><span data-stu-id="d2fbe-118">View the [complete list](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=virtual%20network) of Azure Virtual Network samples.</span></span>
