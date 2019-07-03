---
title: Managed Disks
description: Erstellen, Ändern der Größe und Aktualisieren eines verwalteten Datenträgers
author: lisawong19
manager: douge
ms.assetid: ''
ms.devlang: python
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 6/15/2017
ms.author: routlaw
ms.openlocfilehash: 8618b42a545e2e36ccca8944ef1dc6cf49966b00
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534419"
---
# <a name="managed-disks"></a><span data-ttu-id="54291-103">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="54291-103">Managed Disks</span></span>

<span data-ttu-id="54291-104">Azure Managed Disks bietet eine einfachere Datenträgerverwaltung, mehr Flexibilität, sowie höhere Sicherheit und eine bessere Skalierung.</span><span class="sxs-lookup"><span data-stu-id="54291-104">Azure Managed Disks provide a simplified disk Management, enhanced Scalability, better Security and Scale.</span></span> <span data-ttu-id="54291-105">Ein Speicherkonto für Datenträger ist nicht mehr erforderlich, sodass sich Kunden bei der Skalierung keine Gedanken um die mit Speicherkonten einhergehenden Einschränkungen machen müssen.</span><span class="sxs-lookup"><span data-stu-id="54291-105">It takes away the notion of storage account for disks, enabling customers to scale without worrying about the limitations associated with storage accounts.</span></span> <span data-ttu-id="54291-106">Dieser Artikel enthält eine kurze Einführung und Referenz zur Nutzung des Diensts über Python.</span><span class="sxs-lookup"><span data-stu-id="54291-106">This post provides a quick introduction and reference on consuming the service from Python.</span></span>

<span data-ttu-id="54291-107">Aus Entwicklerperspektive entspricht die Managed Disks-Umgebung in der Azure CLI der CLI-Umgebung in anderen plattformübergreifenden Tools.</span><span class="sxs-lookup"><span data-stu-id="54291-107">From a developer perspective, the Managed Disks experience in Azure CLI is idomatic to the CLI experience in other cross-platform tools.</span></span> <span data-ttu-id="54291-108">Für die Verwaltung von Managed Disks können Sie das [Azure Python](https://azure.microsoft.com/develop/python/) SDK und [azure-mgmt-compute-Paket 0.33.0](https://pypi.python.org/pypi/azure-mgmt-compute) verwenden.</span><span class="sxs-lookup"><span data-stu-id="54291-108">You can use the [Azure Python](https://azure.microsoft.com/develop/python/) SDK and the [azure-mgmt-compute package 0.33.0](https://pypi.python.org/pypi/azure-mgmt-compute) to administer Managed Disks.</span></span> <span data-ttu-id="54291-109">Ein Computeclient kann anhand [dieses Tutorials](https://docs.microsoft.com/python/api/overview/azure/virtualmachines?view=azure-python) erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="54291-109">You can create a compute client using this [tutorial](https://docs.microsoft.com/python/api/overview/azure/virtualmachines?view=azure-python).</span></span>

## <a name="standalone-managed-disks"></a><span data-ttu-id="54291-110">Eigenständige verwaltete Datenträger</span><span class="sxs-lookup"><span data-stu-id="54291-110">Standalone Managed Disks</span></span>

<span data-ttu-id="54291-111">Eigenständige verwaltete Datenträger können auf unterschiedliche Weise erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="54291-111">You can easily create standalone Managed Disks in a variety of ways.</span></span>

### <a name="create-an-empty-managed-disk"></a><span data-ttu-id="54291-112">Erstellen eines leeren verwalteten Datenträgers</span><span class="sxs-lookup"><span data-stu-id="54291-112">Create an empty Managed Disk</span></span>

```python
from azure.mgmt.compute.models import DiskCreateOption

async_creation = compute_client.disks.create_or_update(
    'my_resource_group',
    'my_disk_name',
    {
        'location': 'eastus',
        'disk_size_gb': 20,
        'creation_data': {
            'create_option': DiskCreateOption.empty
        }
    }
)
disk_resource = async_creation.result()
```

### <a name="create-a-managed-disk-from-blob-storage"></a><span data-ttu-id="54291-113">Erstellen eines verwalteten Datenträgers über den Blobspeicher</span><span class="sxs-lookup"><span data-stu-id="54291-113">Create a Managed Disk from blob storage</span></span>

```python
from azure.mgmt.compute.models import DiskCreateOption

async_creation = compute_client.disks.create_or_update(
    'my_resource_group',
    'my_disk_name',
    {
        'location': 'eastus',
        'creation_data': {
            'create_option': DiskCreateOption.import_enum,
            'source_uri': 'https://bg09.blob.core.windows.net/vm-images/non-existent.vhd'
        }
    }
)
disk_resource = async_creation.result()
```

### <a name="create-an-image-from-blob-storage"></a><span data-ttu-id="54291-114">Erstellen eines Images über den Blobspeicher</span><span class="sxs-lookup"><span data-stu-id="54291-114">Create an image from blob storage</span></span>

```python
from azure.mgmt.compute.models import DiskCreateOption

async_creation = compute_client.images.create_or_update(
    'my_resource_group',
    'my_image_name',
    {
        'location': 'eastus',
        'storage_profile': {
           'os_disk': {
              'os_type': 'Linux',
              'os_state': "Generalized",
              'blob_uri': 'https://bg09.blob.core.windows.net/vm-images/non-existent.vhd',
              'caching': "ReadWrite",
           }
        }        
    }
)
image_resource = async_creation.result()
```

### <a name="create-a-managed-disk-from-your-own-image"></a><span data-ttu-id="54291-115">Erstellen eines verwalteten Datenträgers anhand eines eigenen Images</span><span class="sxs-lookup"><span data-stu-id="54291-115">Create a Managed Disk from your own image</span></span>

```python
from azure.mgmt.compute.models import DiskCreateOption

# If you don't know the id, do a 'get' like this to obtain it
managed_disk = compute_client.disks.get(self.group_name, 'myImageDisk')
async_creation = compute_client.disks.create_or_update(
    'my_resource_group',
    'my_disk_name',
    {
        'location': 'eastus',
        'creation_data': {
            'create_option': DiskCreateOption.copy,
            'source_resource_id': managed_disk.id
        }
    }
)

disk_resource = async_creation.result()
```

## <a name="virtual-machine-with-managed-disks"></a><span data-ttu-id="54291-116">Virtuelle Computer mit verwalteten Datenträgern</span><span class="sxs-lookup"><span data-stu-id="54291-116">Virtual machine with Managed Disks</span></span>

<span data-ttu-id="54291-117">Sie können einen virtuellen Computer mit einem impliziten verwalteten Datenträger für ein spezifisches Datenträgerimage erstellen.</span><span class="sxs-lookup"><span data-stu-id="54291-117">You can create a Virtual Machine with an implicit Managed Disk for a specific disk image.</span></span> <span data-ttu-id="54291-118">Die Erstellung wird durch die implizite Erstellung verwalteter Datenträger ohne Angabe der Datenträgerdetails vereinfacht.</span><span class="sxs-lookup"><span data-stu-id="54291-118">Creation is simplified with implicit creation of managed disks without specifying all the disk details.</span></span> <span data-ttu-id="54291-119">Sie müssen sich keine Gedanken um die Erstellung und Verwaltung von Speicherkonten machen.</span><span class="sxs-lookup"><span data-stu-id="54291-119">You do not have to worry about creating and managing Storage Accounts.</span></span>

<span data-ttu-id="54291-120">Ein verwalteter Datenträger wird implizit erstellt, wenn ein virtueller Computer anhand eines Betriebssystemimages in Azure erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="54291-120">A Managed Disk is created implicitly when creating VM from an OS image in Azure.</span></span> <span data-ttu-id="54291-121">Im Parameter ``storage_profile`` ist ``os_disk`` jetzt optional, und die Erstellung eines Speicherkontos ist keine Voraussetzung für die Erstellung eines virtuellen Computers.</span><span class="sxs-lookup"><span data-stu-id="54291-121">In the ``storage_profile`` parameter, ``os_disk`` is now optional and you don't have to create a storage account as required precondition to create a Virtual Machine.</span></span>

```python
storage_profile = azure.mgmt.compute.models.StorageProfile(
    image_reference = azure.mgmt.compute.models.ImageReference(
        publisher='Canonical',
        offer='UbuntuServer',
        sku='16.04-LTS',
        version='latest'
    )
)
```

<span data-ttu-id="54291-122">Der Parameter ``storage_profile`` ist jetzt gültig.</span><span class="sxs-lookup"><span data-stu-id="54291-122">This ``storage_profile`` parameter is now valid.</span></span> <span data-ttu-id="54291-123">Ein vollständiges Beispiel zum Erstellen eines virtuellen Computers in Python (einschließlich Netzwerk usw.) finden Sie im vollständigen [Tutorial zu virtuellen Computern in Python](https://github.com/Azure-Samples/virtual-machines-python-manage).</span><span class="sxs-lookup"><span data-stu-id="54291-123">To get a complete example on how to create a VM in Python (including network, etc), check the full [VM tutorial in Python](https://github.com/Azure-Samples/virtual-machines-python-manage).</span></span>

<span data-ttu-id="54291-124">Sie können ``storage_profile`` auch mithilfe eines eigenen Images erstellen:</span><span class="sxs-lookup"><span data-stu-id="54291-124">You can also create a ``storage_profile`` from your own image:</span></span>

```python
# If you don't know the id, do a 'get' like this to obtain it
image = compute_client.images.get(self.group_name, 'myImageDisk')
storage_profile = azure.mgmt.compute.models.StorageProfile(
    image_reference = azure.mgmt.compute.models.ImageReference(
        id = image.id
    )
)
```

<span data-ttu-id="54291-125">Ein zuvor bereitgestellter verwalteter Datenträger kann ganz einfach angefügt werden.</span><span class="sxs-lookup"><span data-stu-id="54291-125">You can easily attach a previously provisioned Managed Disk.</span></span>

```python
vm = compute.virtual_machines.get(
    'my_resource_group',
    'my_vm'
)
managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
vm.storage_profile.data_disks.append({
    'lun': 12, # You choose the value, depending of what is available for you
    'name': managed_disk.name,
    'create_option': DiskCreateOptionTypes.attach,
    'managed_disk': {
        'id': managed_disk.id
    }
})
async_update = compute_client.virtual_machines.create_or_update(
    'my_resource_group',
    vm.name,
    vm,
)
async_update.wait()
```

## <a name="virtual-machine-scale-sets-with-managed-disks"></a><span data-ttu-id="54291-126">VM-Skalierungsgruppen mit Managed Disks</span><span class="sxs-lookup"><span data-stu-id="54291-126">Virtual machine Scale Sets with Managed Disks</span></span>

<span data-ttu-id="54291-127">Vor der Einführung von verwalteten Datenträgern mussten Sie manuell ein Speicherkonto für alle virtuellen Computer erstellen, die in der Skalierungsgruppe enthalten sein sollten, und anschließend mit dem Auflistungsparameter ``vhd_containers`` den vollständigen Speicherkontonamen an die REST-API der Skalierungsgruppe übergeben.</span><span class="sxs-lookup"><span data-stu-id="54291-127">Before Managed Disks, you needed to create a storage account manually for all the VMs you wanted inside your Scale Set, and then use the list parameter ``vhd_containers`` to provide all the storage account name to the Scale Set RestAPI.</span></span> <span data-ttu-id="54291-128">Das offizielle Handbuch für den Übergang finden Sie in diesem Artikel: `<https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-convert-template-to-md>`.</span><span class="sxs-lookup"><span data-stu-id="54291-128">The official transition guide is available in this article `<https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-convert-template-to-md>`.</span></span>

<span data-ttu-id="54291-129">Dank verwalteter Datenträger müssen Sie nun keine Speicherkonten mehr verwalten.</span><span class="sxs-lookup"><span data-stu-id="54291-129">Now with Managed Disk, you don't have to manage any storage account at all.</span></span> <span data-ttu-id="54291-130">Wenn Sie mit der Verwendung des VMSS Python SDK vertraut sind, können Sie nun das gleiche Speicherprofil (``storage_profile``) wie bei der Erstellung der virtuellen Computer verwenden:</span><span class="sxs-lookup"><span data-stu-id="54291-130">If you're are used to the VMSS Python SDK, your ``storage_profile`` can now be exactly the same as the one used in VM creation:</span></span>

```python
'storage_profile': {
    'image_reference': {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "16.04-LTS",
        "version": "latest"
    }
},
```

<span data-ttu-id="54291-131">Das vollständige Beispiel lautet wie folgt:</span><span class="sxs-lookup"><span data-stu-id="54291-131">The full sample being:</span></span>

```python
naming_infix = "PyTestInfix"
vmss_parameters = {
    'location': self.region,
    "overprovision": True,
    "upgrade_policy": {
        "mode": "Manual"
    },
    'sku': {
        'name': 'Standard_A1',
        'tier': 'Standard',
        'capacity': 5
    },
    'virtual_machine_profile': {
        'storage_profile': {
            'image_reference': {
                "publisher": "Canonical",
                "offer": "UbuntuServer",
                "sku": "16.04-LTS",
                "version": "latest"
            }
        },
        'os_profile': {
            'computer_name_prefix': naming_infix,
            'admin_username': 'Foo12',
            'admin_password': 'BaR@123!!!!',
        },
        'network_profile': {
            'network_interface_configurations' : [{
                'name': naming_infix + 'nic',
                "primary": True,
                'ip_configurations': [{
                    'name': naming_infix + 'ipconfig',
                    'subnet': {
                        'id': subnet.id
                    } 
                }]
            }]
        }
    }
}

# Create VMSS test
result_create = compute_client.virtual_machine_scale_sets.create_or_update(
    'my_resource_group',
    'my_scale_set',
    vmss_parameters,
)
vmss_result = result_create.result()
```

## <a name="other-operations-with-managed-disks"></a><span data-ttu-id="54291-132">Andere Vorgänge mit Managed Disks</span><span class="sxs-lookup"><span data-stu-id="54291-132">Other operations with Managed Disks</span></span>

### <a name="resizing-a-managed-disk"></a><span data-ttu-id="54291-133">Ändern der Größe eines verwalteten Datenträgers</span><span class="sxs-lookup"><span data-stu-id="54291-133">Resizing a Managed Disk</span></span>

```python
managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
managed_disk.disk_size_gb = 25
async_update = self.compute_client.disks.create_or_update(
    'my_resource_group',
    'myDisk',
    managed_disk
)
async_update.wait()
```

### <a name="update-the-storage-account-type-of-the-managed-disks"></a><span data-ttu-id="54291-134">Aktualisieren des Speicherkontotyps der verwalteten Datenträger</span><span class="sxs-lookup"><span data-stu-id="54291-134">Update the storage account type of the Managed Disks</span></span>

```python
from azure.mgmt.compute.models import StorageAccountTypes

managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
managed_disk.account_type = StorageAccountTypes.standard_lrs
async_update = self.compute_client.disks.create_or_update(
    'my_resource_group',
    'myDisk',
    managed_disk
)
async_update.wait()
```

### <a name="create-an-image-from-nlob-storage"></a><span data-ttu-id="54291-135">Erstellen eines Images über den Blobspeicher</span><span class="sxs-lookup"><span data-stu-id="54291-135">Create an image from nlob storage</span></span>

```python
async_create_image = compute_client.images.create_or_update(
    'my_resource_group',
    'myImage',
    {
        'location': 'westus',
        'storage_profile': {
            'os_disk': {
                'os_type': 'Linux',
                'os_state': "Generalized",
                'blob_uri': 'https://bg09.blob.core.windows.net/vm-images/non-existent.vhd',
                'caching': "ReadWrite",
            }
        }
    }
)
image = async_create_image.result()
```

### <a name="create-a-snapshot-of-a-managed-disk-that-is-currently-attached-to-a-virtual-machine"></a><span data-ttu-id="54291-136">Erstellen einer Momentaufnahme eines verwalteten Datenträgers, der derzeit an einen virtuellen Computer angefügt ist</span><span class="sxs-lookup"><span data-stu-id="54291-136">Create a snapshot of a Managed Disk that is currently attached to a virtual machine</span></span>

```python
managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
async_snapshot_creation = self.compute_client.snapshots.create_or_update(
        'my_resource_group',
        'mySnapshot',
        {
            'location': 'westus',
            'creation_data': {
                'create_option': 'Copy',
                'source_uri': managed_disk.id
            }
        }
    )
snapshot = async_snapshot_creation.result()
```
