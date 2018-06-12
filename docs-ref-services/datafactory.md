---
title: Azure Data Factory-Bibliotheken für Python
description: Referenz zu Azure Data Factory-Bibliotheken für Python
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 05/10/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 05d93f7d1838c110c3ba77f7abd3967f7870774b
ms.sourcegitcommit: d65549030a0edb50d75482f79aac0962d1dacb57
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/05/2018
ms.locfileid: "34759047"
---
# <a name="azure-data-factory-libraries-for-python"></a><span data-ttu-id="f2d08-103">Azure Data Factory-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="f2d08-103">Azure Data Factory libraries for Python</span></span>

<span data-ttu-id="f2d08-104">Kombinieren von Datenspeicherungs-, Verschiebungs- und Verarbeitungsdiensten in automatisierten Datenpipelines mit [Azure Data Factory](/azure/data-factory/)</span><span class="sxs-lookup"><span data-stu-id="f2d08-104">Compose data storage, movement, and processing services into automated data pipelines with [Azure Data Factory](/azure/data-factory/)</span></span>

<span data-ttu-id="f2d08-105">[Erfahren Sie mehr](/azure/data-factory/introduction) über Data Factory, und führen Sie mit der Schnellstartanleitung zum [Erstellen einer Data Factory und Pipeline mithilfe von Python](/azure/data-factory/quickstart-create-data-factory-python) die ersten Schritte aus.</span><span class="sxs-lookup"><span data-stu-id="f2d08-105">[Learn more](/azure/data-factory/introduction) about Data Factory and get started with the [Create a data factory and pipeline using Python quickstart](/azure/data-factory/quickstart-create-data-factory-python).</span></span> 

## <a name="management-module"></a><span data-ttu-id="f2d08-106">Verwaltungsmodul</span><span class="sxs-lookup"><span data-stu-id="f2d08-106">Management module</span></span>

<span data-ttu-id="f2d08-107">Über das Verwaltungsmodul können Sie Data Factory-Instanzen in Ihrem Abonnement erstellen und verwalten.</span><span class="sxs-lookup"><span data-stu-id="f2d08-107">Create and manage Data Factory instances in your subscription with the management module.</span></span>

### <a name="installation"></a><span data-ttu-id="f2d08-108">Installation</span><span class="sxs-lookup"><span data-stu-id="f2d08-108">Installation</span></span>

<span data-ttu-id="f2d08-109">Installieren Sie das Paket mithilfe von [pip](https://pip.pypa.io/en/stable/quickstart/).</span><span class="sxs-lookup"><span data-stu-id="f2d08-109">Install the package with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```bash
pip install azure-mgmt-datafactory 
```

### <a name="example"></a><span data-ttu-id="f2d08-110">Beispiel</span><span class="sxs-lookup"><span data-stu-id="f2d08-110">Example</span></span> 

<span data-ttu-id="f2d08-111">Erstellen Sie eine Data Factory-Instanz in Ihrem Abonnement in der Region „USA, Osten“.</span><span class="sxs-lookup"><span data-stu-id="f2d08-111">Create a Data Factory in your subscription on the East US region.</span></span>

```python
from azure.common.credentials import ServicePrincipalCredentials
from azure.mgmt.resource import ResourceManagementClient
from azure.mgmt.datafactory import DataFactoryManagementClient
from azure.mgmt.datafactory.models import *
import time

#Create a data factory
subscription_id = '<Specify your Azure Subscription ID>'
credentials = ServicePrincipalCredentials(client_id='<Active Directory application/client ID>', secret='<client secret>', tenant='<Active Directory tenant ID>')
adf_client = DataFactoryManagementClient(credentials, subscription_id)

rg_params = {'location':'eastus'}
df_params = {'location':'eastus'}  

df_resource = Factory(location='eastus')
df = adf_client.factories.create_or_update(rg_name, df_name, df_resource)
print_item(df)
while df.provisioning_state != 'Succeeded':
    df = adf_client.factories.get(rg_name, df_name)
    time.sleep(1)
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="f2d08-112">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="f2d08-112">Explore the Management APIs</span></span>](/python/api/overview/azure/datafactory/management)