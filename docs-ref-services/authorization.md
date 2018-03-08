---
title: "Azure-Autorisierungsbibliotheken für Python"
description: "Referenz zu Azure-Autorisierungsbibliotheken für Python"
keywords: Azure, Python, SDK, API, Autorisierung
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: ba8814b22ee07a27181b214c6cc49607d4bc5d50
ms.sourcegitcommit: 757bf84535fd9d8299c4b51ec92a5ab1926cb671
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2018
---
# <a name="azure-authorization-libraries-for-python"></a><span data-ttu-id="98459-104">Azure-Autorisierungsbibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="98459-104">Azure Authorization libraries for python</span></span>

## <a name="management-apipythonapioverviewazureauthorizationmanagement"></a>[<span data-ttu-id="98459-105">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="98459-105">Management API</span></span>](/python/api/overview/azure/authorization/management)

```bash
pip install azure-mgmt-authorization
```

## <a name="create-the-management-client"></a><span data-ttu-id="98459-106">Erstellen des Verwaltungsclients</span><span class="sxs-lookup"><span data-stu-id="98459-106">Create the management client</span></span>

<span data-ttu-id="98459-107">Der folgende Code erstellt eine Instanz des Verwaltungsclients.</span><span class="sxs-lookup"><span data-stu-id="98459-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="98459-108">Sie müssen Ihre ``subscription_id`` angeben. Diese ID kann aus der [Abonnementliste](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping) abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="98459-108">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="98459-109">Informationen zur Azure Active Directory-Authentifizierung mit dem Python SDK sowie zum Erstellen einer ``Credentials``-Instanz finden Sie im Artikel zur [Authentifizierung bei der Ressourcenverwaltung](/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="98459-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.authorization import AuthorizationManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

authorization_client = AuthorizationManagementClient(
    credentials,
    subscription_id
)
``` 

## <a name="check-permissions-for-a-resource-group"></a><span data-ttu-id="98459-110">Überprüfen der Berechtigungen für eine Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="98459-110">Check permissions for a resource group</span></span>

<span data-ttu-id="98459-111">Der folgende Code überprüft die Berechtigungen in einer bestimmten Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="98459-111">The following code checks permissions in a given resource group.</span></span>
<span data-ttu-id="98459-112">Informationen zum Erstellen oder Verwalten von Ressourcengruppen finden Sie im Artikel zur [Ressourcenverwaltung](/python/api/overview/azure/azure.mgmt.resource).</span><span class="sxs-lookup"><span data-stu-id="98459-112">To create or manage resource groups, see [Resource Management](/python/api/overview/azure/azure.mgmt.resource).</span></span>

```python
from azure.mgmt.redis.models import Sku, RedisCreateOrUpdateParameters

group_name = 'myresourcegroup'
permissions = self.authorization_client.permissions.list_for_resource_group(
    group_name
)
# permissions is a iterable of Permissions instances
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="98459-113">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="98459-113">Explore the Management APIs</span></span>](/python/api/overview/azure/authorization/management)

