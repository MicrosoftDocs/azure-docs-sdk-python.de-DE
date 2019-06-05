---
title: Azure Batch-Bibliotheken für Python
description: Referenzdokumentation für die Python-Batch-Bibliotheken
keywords: Azure, Python, SDK, API, Batch, Verarbeitung, Planung, lange Ausführungszeit
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/31/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: batch
ms.openlocfilehash: fb9528c449d197440590bfc3b1991065cfe13357
ms.sourcegitcommit: 434186988284e0a8268a9de11645912a81226d6b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/29/2019
ms.locfileid: "66376838"
---
# <a name="azure-batch-libraries-for-python"></a>Azure Batch-Bibliotheken für Python

## <a name="overview"></a>Übersicht

Effizientes Ausführen umfangreicher paralleler HPC-Anwendungen in der Cloud mit [Azure Batch](/azure/batch/batch-technical-overview).

Informationen zu den ersten Schritte mit Azure Batch finden Sie unter [Erstellen eines Batch-Kontos mit dem Azure-Portal](/azure/batch/batch-account-create-portal).

## <a name="install-the-libraries"></a>Installieren der Bibliotheken

## <a name="client-library"></a>Clientbibliothek
Mit den Azure Batch-Clientbibliotheken können Sie Computeknoten und -pools konfigurieren, Aufgaben definieren und ihre Ausführung in Aufträgen konfigurieren sowie einen Auftrags-Manager zum Steuern und Überwachen der Auftragsausführung einrichten. [Erfahren Sie mehr](/azure/batch/batch-api-basics) über die Verwendung dieser Objekte zum Ausführen umfangreicher paralleler Computelösungen.

```bash
pip install azure-batch
```
### <a name="example"></a>Beispiel

Einrichten eines Pools mit Linux-Computeknoten in einem Batch-Konto:

```python
# create the batch client for an account using its URI and keys
creds = batchauth.SharedKeyCredentials(account, key)
config = batch.BatchServiceClientConfiguration(creds, base_url = batch_url)
client = batch.BatchServiceClient(config)

# Create the VirtualMachineConfiguration, specifying
# the VM image reference and the Batch node agent to
# be installed on the node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = "batch.node.ubuntu 14.04")

# Assign the virtual machine configuration to the pool
new_pool.virtual_machine_configuration = vmc

# Create pool in the Batch service
client.pool.add(new_pool)
```

## <a name="management-api"></a>Verwaltungs-API
Verwenden Sie die Azure Batch-Verwaltungsbibliotheken zum Erstellen und Löschen von Batch-Konten, zum Lesen und erneuten Generieren von Batch-Kontoschlüsseln sowie zum Verwalten von Batch-Kontospeicher.

```bash
pip install azure-mgmt-batch
```
> [!div class="nextstepaction"]
> [Informationen zu den Client-APIs](/python/api/overview/azure/batch/client)

### <a name="example"></a>Beispiel
Erstellen Sie ein Azure Batch-Konto, und konfigurieren Sie dafür eine neue Anwendung und ein neues Azure-Speicherkonto.

```python
from azure.mgmt.batch import BatchManagementClient
from azure.mgmt.resource import ResourceManagementClient
from azure.mgmt.storage import StorageManagementClient

LOCATION ='eastus'
GROUP_NAME ='batchresourcegroup'
STORAGE_ACCOUNT_NAME ='batchstorageaccount'

# Create Resource group
print('Create Resource Group')
resource_client.resource_groups.create_or_update(GROUP_NAME, {'location': LOCATION})

# Create a storage account
storage_async_operation = storage_client.storage_accounts.create(
    GROUP_NAME,
    STORAGE_ACCOUNT_NAME,
    StorageAccountCreateParameters(
        sku=Sku(SkuName.standard_ragrs),
        kind=Kind.storage,
        location=LOCATION
    )
)
storage_account = storage_async_operation.result()

# Create a Batch Account, specifying the storage account we want to link
storage_resource = storage_account.id
batch_account = azure.mgmt.batch.models.BatchAccountCreateParameters(
    location=LOCATION,
    auto_storage=azure.mgmt.batch.models.AutoStorageBaseProperties(storage_resource)
)
creating = batch_client.account.create('MyBatchAccount', LOCATION, batch_account)
creating.wait()
```

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/batch/management)
