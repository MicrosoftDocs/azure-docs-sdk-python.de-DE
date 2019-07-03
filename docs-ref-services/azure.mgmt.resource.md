---
title: Azure-Ressourcenbibliotheken für Python
description: ''
keywords: Azure, Python, SDK, API, Ressourcen
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 06/19/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: resources
ms.openlocfilehash: d708a5e7296b166b6e55b9b7b0d995e72e264267
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534371"
---
# <a name="azure-resources-libraries-for-python"></a><span data-ttu-id="0e34a-103">Azure-Ressourcenbibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="0e34a-103">Azure Resources libraries for Python</span></span> 

## <a name="overview"></a><span data-ttu-id="0e34a-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="0e34a-104">Overview</span></span> 
<span data-ttu-id="0e34a-105">Verwalten von Azure-Ressourcen in Ressourcengruppen</span><span class="sxs-lookup"><span data-stu-id="0e34a-105">Manage Azure resources in resource groups.</span></span>

| <span data-ttu-id="0e34a-106">Paket</span><span class="sxs-lookup"><span data-stu-id="0e34a-106">Package</span></span>  |  <span data-ttu-id="0e34a-107">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="0e34a-107">Description</span></span> |
|---|---|
|<span data-ttu-id="0e34a-108">[azure.mgmt.resource.features][1]</span><span class="sxs-lookup"><span data-stu-id="0e34a-108">[azure.mgmt.resource.features][1]</span></span>|<span data-ttu-id="0e34a-109">Die Steuerung für die Azure-Featureanzeige (Azure Feature Exposure Control, AFEC) ist ein Mechanismus, mit dem Ressourcenanbieter die Anzeige von Features für Benutzer steuern können.</span><span class="sxs-lookup"><span data-stu-id="0e34a-109">Azure Feature Exposure Control (AFEC) provides a mechanism for the resource providers to control feature exposure to users.</span></span>|
|<span data-ttu-id="0e34a-110">[azure.mgmt.resource.links][2]</span><span class="sxs-lookup"><span data-stu-id="0e34a-110">[azure.mgmt.resource.links][2]</span></span>|<span data-ttu-id="0e34a-111">Azure-Ressourcen können verknüpft werden, um logische Beziehungen zu bilden.</span><span class="sxs-lookup"><span data-stu-id="0e34a-111">Azure resources can be linked together to form logical relationships.</span></span> <span data-ttu-id="0e34a-112">Sie können Verknüpfungen zwischen Ressourcen aus verschiedenen Ressourcengruppen herstellen.</span><span class="sxs-lookup"><span data-stu-id="0e34a-112">You can establish links between resources belonging to different resource groups.</span></span>|
|<span data-ttu-id="0e34a-113">[azure.mgmt.resource.locks][3]</span><span class="sxs-lookup"><span data-stu-id="0e34a-113">[azure.mgmt.resource.locks][3]</span></span>|<span data-ttu-id="0e34a-114">Azure-Ressourcen können gesperrt werden, um zu verhindern, dass andere Benutzer in Ihrer Organisation Ressourcen löschen oder ändern.</span><span class="sxs-lookup"><span data-stu-id="0e34a-114">Azure resources can be locked to prevent other users in your organization from deleting or modifying resources.</span></span>|
|<span data-ttu-id="0e34a-115">[azure.mgmt.resource.managedapplications][4]</span><span class="sxs-lookup"><span data-stu-id="0e34a-115">[azure.mgmt.resource.managedapplications][4]</span></span>|<span data-ttu-id="0e34a-116">Über ARM verwaltete Anwendungen (Geräte)</span><span class="sxs-lookup"><span data-stu-id="0e34a-116">ARM managed applications (appliances).</span></span>|
|<span data-ttu-id="0e34a-117">[azure.mgmt.resource.policy][5]</span><span class="sxs-lookup"><span data-stu-id="0e34a-117">[azure.mgmt.resource.policy][5]</span></span>|<span data-ttu-id="0e34a-118">Zur Verwaltung und Steuerung des Ressourcenzugriffs können Sie benutzerdefinierte Richtlinien definieren und bereichsweise zuweisen.</span><span class="sxs-lookup"><span data-stu-id="0e34a-118">To manage and control access to your resources, you can define customized policies and assign them at a scope.</span></span>|
|<span data-ttu-id="0e34a-119">[azure.mgmt.resource.resources][6]</span><span class="sxs-lookup"><span data-stu-id="0e34a-119">[azure.mgmt.resource.resources][6]</span></span>| <span data-ttu-id="0e34a-120">Stellt Vorgänge für die Arbeit mit Ressourcen und Ressourcengruppen bereit.</span><span class="sxs-lookup"><span data-stu-id="0e34a-120">Provides operations for working with resources and resource groups.</span></span>|
|<span data-ttu-id="0e34a-121">[azure.mgmt.resource.subscriptions][7]</span><span class="sxs-lookup"><span data-stu-id="0e34a-121">[azure.mgmt.resource.subscriptions][7]</span></span>|<span data-ttu-id="0e34a-122">Alle Ressourcengruppen und Ressourcen befinden sich in Abonnements.</span><span class="sxs-lookup"><span data-stu-id="0e34a-122">All resource groups and resources exist within subscriptions.</span></span> <span data-ttu-id="0e34a-123">Diese Vorgänge ermöglichen das Abrufen von Informationen zu Abonnements und Mandanten.</span><span class="sxs-lookup"><span data-stu-id="0e34a-123">These operation enable you get information about your subscriptions and tenants.</span></span>|

[1]: /python/api/azure.mgmt.resource.features
[2]: /python/api/azure.mgmt.resource.links
[3]: /python/api/azure.mgmt.resource.locks
[4]: /python/api/azure.mgmt.resource.managedapplications
[5]: /python/api/azure.mgmt.resource.policy
[6]: /python/api/azure.mgmt.resource.resources
[7]: /python/api/azure.mgmt.resource.subscriptions

## <a name="install-the-libraries"></a><span data-ttu-id="0e34a-124">Installieren der Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="0e34a-124">Install the libraries</span></span> 
```bash
pip install azure-mgmt-resource
```

## <a name="example"></a><span data-ttu-id="0e34a-125">Beispiel</span><span class="sxs-lookup"><span data-stu-id="0e34a-125">Example</span></span>
<span data-ttu-id="0e34a-126">Hier sehen Sie ein Beispiel zum Erstellen einer Ressourcengruppe:</span><span class="sxs-lookup"><span data-stu-id="0e34a-126">The following is an example of how to create a resource group.</span></span> 

```python
from azure.mgmt.resource import ResourceManagementClient
client = ResourceManagementClient(credentials, subscription_id)
client.resource_groups.create(RESOURCE_GROUP_NAME, {'location':'eastus'})
```

<span data-ttu-id="0e34a-127">Sehen Sie sich weiteren [Python-Beispielcode](https://azure.microsoft.com/resources/samples/?platform=python) an, den Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="0e34a-127">Explore more [sample Python code](https://azure.microsoft.com/resources/samples/?platform=python) you can use in your apps.</span></span> 