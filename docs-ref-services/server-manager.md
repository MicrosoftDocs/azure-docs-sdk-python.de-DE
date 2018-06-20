---
title: Azure-Server-Manager-Bibliotheken für Python
description: Referenz zu Azure-Server-Manager-Bibliotheken für Python
keywords: Azure, Python, SDK, API, Server-Manager
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/22/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 480513a76683c97fdac8d2a65b38fde0fffb6dcd
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
ms.locfileid: "29479233"
---
# <a name="azure-server-manager-libraries-for-python"></a><span data-ttu-id="60016-104">Azure-Server-Manager-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="60016-104">Azure Server Manager libraries for python</span></span>

## <a name="management-apipythonapioverviewazureservermanagermanagement"></a>[<span data-ttu-id="60016-105">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="60016-105">Management API</span></span>](/python/api/overview/azure/servermanager/management)

```bash
pip install azure-mgmt-servermanager
```

## <a name="create-the-management-client"></a><span data-ttu-id="60016-106">Erstellen des Verwaltungsclients</span><span class="sxs-lookup"><span data-stu-id="60016-106">Create the management client</span></span>

<span data-ttu-id="60016-107">Der folgende Code erstellt eine Instanz des Verwaltungsclients.</span><span class="sxs-lookup"><span data-stu-id="60016-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="60016-108">Sie müssen Ihre ``subscription_id`` angeben. Diese ID kann aus der [Abonnementliste](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping) abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="60016-108">You will need to provide your ``subscription_id`` which can be retrieved from your [subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="60016-109">Informationen zur Azure Active Directory-Authentifizierung mit dem Python SDK sowie zum Erstellen einer ``Credentials``-Instanz finden Sie im Artikel zur [Authentifizierung bei der Ressourcenverwaltung](/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="60016-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.servermanager import ServerManagement
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

servermanager_client = ServerManagement(
    credentials,
    subscription_id
)
``` 

## <a name="create-gateway"></a><span data-ttu-id="60016-110">Erstellen des Gateways</span><span class="sxs-lookup"><span data-stu-id="60016-110">Create gateway</span></span>
```python
gateway_async = servermanager_client.gateway.create(
    'MyResourceGroup',
    'MyGateway',
    'centralus'
)
gateway = gateway_async.result() # Blocking wait
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="60016-111">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="60016-111">Explore the Management APIs</span></span>](/python/api/overview/azure/servermanager/management)