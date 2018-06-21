---
title: Azure-Autorisierungsbibliotheken für Python
description: Referenz zu Azure-Autorisierungsbibliotheken für Python
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
ms.openlocfilehash: a3db490357ec35c0780d7dd16114b9041458373d
ms.sourcegitcommit: 86f7f40295271ef94272642efb89b471aae99a2c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/18/2018
ms.locfileid: "35720041"
---
# <a name="azure-authorization-libraries-for-python"></a>Azure-Autorisierungsbibliotheken für Python

## <a name="management-apipythonapioverviewazureauthorizationmanagement"></a>[Verwaltungs-API](/python/api/overview/azure/authorization/management)

```bash
pip install azure-mgmt-authorization
```

## <a name="create-the-management-client"></a>Erstellen des Verwaltungsclients

Der folgende Code erstellt eine Instanz des Verwaltungsclients.

Sie müssen Ihre ``subscription_id`` angeben. Diese ID kann aus der [Abonnementliste](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping) abgerufen werden.

Informationen zur Azure Active Directory-Authentifizierung mit dem Python SDK sowie zum Erstellen einer ``Credentials``-Instanz finden Sie im Artikel zur [Authentifizierung bei der Ressourcenverwaltung](/python/azure/python-sdk-azure-authenticate).

```python
from azure.mgmt.authorization import AuthorizationManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password'       # Your password
)

authorization_client = AuthorizationManagementClient(
    credentials,
    subscription_id
)
``` 

## <a name="check-permissions-for-a-resource-group"></a>Überprüfen der Berechtigungen für eine Ressourcengruppe

Der folgende Code überprüft die Berechtigungen in einer bestimmten Ressourcengruppe.
Informationen zum Erstellen oder Verwalten von Ressourcengruppen finden Sie im Artikel zur [Ressourcenverwaltung](/python/api/overview/azure/azure.mgmt.resource).

```python
from azure.mgmt.redis.models import Sku, RedisCreateOrUpdateParameters

group_name = 'myresourcegroup'
permissions = self.authorization_client.permissions.list_for_resource_group(
    group_name
)
# permissions is a iterable of Permissions instances
```

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/authorization/management)

