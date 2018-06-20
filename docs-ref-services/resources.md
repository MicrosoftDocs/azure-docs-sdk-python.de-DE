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
# <a name="azure-resources-libraries-for-python"></a>Azure-Ressourcenbibliotheken für Python

## <a name="overview"></a>Übersicht 
Mit [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) können Sie Ressourcen in Gruppen bereitstellen, überwachen und verwalten.

## <a name="management-api"></a>Verwaltungs-API
Verwenden Sie die Verwaltungs-API zum Erstellen von Ressourcengruppen und Bereitstellen von Ressourcen aus Vorlagen.

```bash
pip install azure-mgmt-resource
```
### <a name="example"></a>Beispiel 
Erstellen Sie eine neue Ressourcengruppe in der Azure-Region „USA, Osten“.

```python
from azure.mgmt.resource import ResourceManagementClient

LOCATION = 'eastus'
GROUP_NAME ='sample_resource_group'

resource_client = ResourceManagementClient(credentials, subscription_id)
resource_client.resource_groups.create_or_update(GROUP_NAME, {'location': LOCATION})
```

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/azure.mgmt.resource)

## <a name="samples"></a>Beispiele
[Manage Azure resources and resource groups (Verwalten von Azure-Ressourcen und -Ressourcengruppen)](https://github.com/Azure-Samples/resource-manager-python-resources-and-groups)

Zeigen Sie die [vollständige Liste](https://azure.microsoft.com/resources/samples/?platform=python&term=resource) mit Azure Resource Manager-Beispielen an.
