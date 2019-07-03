---
title: Azure Scheduler-Bibliotheken für Python
description: Referenz zu Azure Scheduler-Bibliotheken für Python
keywords: Azure, Python, SDK, API, Scheduler
author: lisawong19
ms.author: routlaw
manager: mbaldwin
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 73c33ff808212fade192ca7c7c05a8e64d3fafda
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534213"
---
# <a name="azure-scheduler-libraries-for-python"></a>Azure Scheduler-Bibliotheken für Python

## <a name="install-the-libraries"></a>Installieren der Bibliotheken

## <a name="management"></a>Verwaltung

```bash
pip install azure-mgmt-scheduler
```
## <a name="example"></a>Beispiel

### <a name="create-the-management-client"></a>Erstellen des Verwaltungsclients

Der folgende Code erstellt eine Instanz des Verwaltungsclients.

Sie müssen Ihre ``subscription_id`` angeben. Diese ID kann aus der [Abonnementliste](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping) abgerufen werden.

Informationen zur Azure Active Directory-Authentifizierung mit dem Python SDK sowie zum Erstellen einer ``Credentials``-Instanz finden Sie im Artikel zur [Authentifizierung bei der Ressourcenverwaltung](/python/azure/python-sdk-azure-authenticate).

```python
from azure.mgmt.scheduler import SchedulerManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

scheduler_client = SchedulerManagementClient(
    credentials,
    subscription_id
)
```

### <a name="create-a-job-collection"></a>Erstellen einer Auftragssammlung

Der folgende Code erstellt eine Auftragssammlung unter einer vorhandenen Ressourcengruppe.
Informationen zum Erstellen oder Verwalten von Ressourcengruppen finden Sie im Artikel zur [Ressourcenverwaltung](/python/api/overview/azure/azure.mgmt.resource).

```python
from azure.mgmt.scheduler.models import JobCollectionDefinition, JobCollectionProperties, Sku

group_name = 'myresourcegroup'
job_collection_name = "myjobcollection"
scheduler_client.job_collections.create_or_update(
    group_name,
    job_collection_name,
    JobCollectionDefinition(
        location = "West US",
        properties = JobCollectionProperties(
            sku = Sku(
                name="Free"
            )
        )
    )
)
# scheduler_client is a JobCollectionDefinition instance
```

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/scheduler/management)