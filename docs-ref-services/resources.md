---
title: Azure-Ressourcenbibliotheken für Python
description: Referenz zu Azure-Ressourcenbibliotheken für Python
keywords: Azure, Python, SDK, API, Ressourcen
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 08/11/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: d924a8aea18d9b59ec8c78d85dce8fe0ce7c8d6c
ms.sourcegitcommit: d521a7350216461eb2fa68152c4975f55152f831
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/06/2017
ms.locfileid: "26327988"
---
# <a name="azure-resources-libraries-for-python"></a><span data-ttu-id="d820a-104">Azure-Ressourcenbibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="d820a-104">Azure Resources libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="d820a-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="d820a-105">Overview</span></span> 
<span data-ttu-id="d820a-106">Mit [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) können Sie Ressourcen in Gruppen bereitstellen, überwachen und verwalten.</span><span class="sxs-lookup"><span data-stu-id="d820a-106">Deploy, monitor, and manage resources in groups with [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="management-api"></a><span data-ttu-id="d820a-107">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="d820a-107">Management API</span></span>
<span data-ttu-id="d820a-108">Verwenden Sie die Verwaltungs-API zum Erstellen von Ressourcengruppen und Bereitstellen von Ressourcen aus Vorlagen.</span><span class="sxs-lookup"><span data-stu-id="d820a-108">Use the management API to create resource groups and deploy resources from templates.</span></span>

```bash
pip install azure-mgmt-resource
```
### <a name="example"></a><span data-ttu-id="d820a-109">Beispiel</span><span class="sxs-lookup"><span data-stu-id="d820a-109">Example</span></span> 
<span data-ttu-id="d820a-110">Erstellen Sie eine neue Ressourcengruppe in der Azure-Region „USA, Osten“.</span><span class="sxs-lookup"><span data-stu-id="d820a-110">Create a new resource group in the Azure Eastern US region.</span></span>

```python
from azure.mgmt.resource import ResourceManagementClient

LOCATION = 'eastus'
GROUP_NAME ='sample_resource_group'

resource_client = ResourceManagementClient(credentials, subscription_id)
resource_client.resource_groups.create_or_update(GROUP_NAME, {'location': LOCATION})
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="d820a-111">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="d820a-111">Explore the Management APIs</span></span>](/python/api/overview/azure/azure.mgmt.resource)

## <a name="samples"></a><span data-ttu-id="d820a-112">Beispiele</span><span class="sxs-lookup"><span data-stu-id="d820a-112">Samples</span></span>
[<span data-ttu-id="d820a-113">Manage Azure resources and resource groups (Verwalten von Azure-Ressourcen und -Ressourcengruppen)</span><span class="sxs-lookup"><span data-stu-id="d820a-113">Manage Azure resources and resource groups</span></span>](https://github.com/Azure-Samples/resource-manager-python-resources-and-groups)

<span data-ttu-id="d820a-114">Zeigen Sie die [vollständige Liste](https://azure.microsoft.com/resources/samples/?platform=python&term=resource) mit Azure Resource Manager-Beispielen an.</span><span class="sxs-lookup"><span data-stu-id="d820a-114">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=resource) of Azure Resource Manager samples.</span></span>
