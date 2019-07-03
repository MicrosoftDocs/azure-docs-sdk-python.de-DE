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
# <a name="azure-scheduler-libraries-for-python"></a><span data-ttu-id="15c52-104">Azure Scheduler-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="15c52-104">Azure Scheduler libraries for python</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="15c52-105">Installieren der Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="15c52-105">Install the libraries</span></span>

## <a name="management"></a><span data-ttu-id="15c52-106">Verwaltung</span><span class="sxs-lookup"><span data-stu-id="15c52-106">Management</span></span>

```bash
pip install azure-mgmt-scheduler
```
## <a name="example"></a><span data-ttu-id="15c52-107">Beispiel</span><span class="sxs-lookup"><span data-stu-id="15c52-107">Example</span></span>

### <a name="create-the-management-client"></a><span data-ttu-id="15c52-108">Erstellen des Verwaltungsclients</span><span class="sxs-lookup"><span data-stu-id="15c52-108">Create the management client</span></span>

<span data-ttu-id="15c52-109">Der folgende Code erstellt eine Instanz des Verwaltungsclients.</span><span class="sxs-lookup"><span data-stu-id="15c52-109">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="15c52-110">Sie müssen Ihre ``subscription_id`` angeben. Diese ID kann aus der [Abonnementliste](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping) abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="15c52-110">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="15c52-111">Informationen zur Azure Active Directory-Authentifizierung mit dem Python SDK sowie zum Erstellen einer ``Credentials``-Instanz finden Sie im Artikel zur [Authentifizierung bei der Ressourcenverwaltung](/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="15c52-111">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

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

### <a name="create-a-job-collection"></a><span data-ttu-id="15c52-112">Erstellen einer Auftragssammlung</span><span class="sxs-lookup"><span data-stu-id="15c52-112">Create a job collection</span></span>

<span data-ttu-id="15c52-113">Der folgende Code erstellt eine Auftragssammlung unter einer vorhandenen Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="15c52-113">The following code creates a job collection under an existing resource group.</span></span>
<span data-ttu-id="15c52-114">Informationen zum Erstellen oder Verwalten von Ressourcengruppen finden Sie im Artikel zur [Ressourcenverwaltung](/python/api/overview/azure/azure.mgmt.resource).</span><span class="sxs-lookup"><span data-stu-id="15c52-114">To create or manage resource groups, see [Resource Management](/python/api/overview/azure/azure.mgmt.resource).</span></span>

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
> [<span data-ttu-id="15c52-115">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="15c52-115">Explore the Management APIs</span></span>](/python/api/overview/azure/scheduler/management)