---
title: "Verwaltete Datenträger"
description: "Erstellen, Ändern der Größe und Aktualisieren eines verwalteten Datenträgers"
author: lisawong19
manager: douge
ms.assetid: 
ms.devlang: python
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 6/15/2017
ms.author: liwong
ms.openlocfilehash: 4154367f0449b174790ee3f3c9480ca0bceeea87
ms.sourcegitcommit: c6d9500492131bf782488fcafc7c5c41c2703e92
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/13/2017
---
# <a name="managed-disks"></a>Verwaltete Datenträger

Azure Managed Disks und 1.000 virtuelle Computer in einer Skalierungsgruppe sind jetzt [allgemein verfügbar](https://azure.microsoft.com/en-us/blog/announcing-general-availability-of-managed-disks-and-larger-scale-sets/). Azure Managed Disks bietet mehr Flexibilität, höhere Sicherheit und eine bessere Skalierung. Ein Speicherkonto für Datenträger ist nicht mehr erforderlich, sodass sich Kunden bei der Skalierung keine Gedanken um die mit Speicherkonten einhergehenden Einschränkungen machen müssen. Dieser Artikel enthält eine kurze Einführung und Referenz zur Nutzung des Diensts über Python.



Aus Entwicklerperspektive entspricht die Managed Disks-Umgebung in der Azure CLI der CLI-Umgebung in anderen plattformübergreifenden Tools. Für die Verwaltung von Managed Disks können Sie das [Azure Python](https://azure.microsoft.com/develop/python/) SDK und [azure-mgmt-compute-Paket 0.33.0](https://pypi.python.org/pypi/azure-mgmt-compute) verwenden. Ein Computeclient kann anhand [dieses Tutorials](http://azure-sdk-for-python.readthedocs.io/en/latest/resourcemanagementcomputenetwork.html) erstellt werden.


## <a name="standalone-managed-disks"></a>Eigenständige verwaltete Datenträger

Eigenständige verwaltete Datenträger können auf unterschiedliche Weise erstellt werden.

### <a name="create-an-empty-managed-disk"></a>Erstellen eines leeren verwalteten Datenträgers
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

### <a name="create-a-managed-disk-from-blob-storage"></a>Erstellen eines verwalteten Datenträgers über Blob Storage
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

### <a name="create-a-managed-disk-from-your-own-image"></a>Erstellen eines verwalteten Datenträgers anhand eines eigenen Images
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

## <a name="virtual-machine-with-managed-disks"></a>Virtuelle Computer mit verwalteten Datenträgern

Sie können einen virtuellen Computer mit einem impliziten verwalteten Datenträger für ein spezifisches Datenträgerimage erstellen. Die Erstellung wird durch die implizite Erstellung verwalteter Datenträger ohne Angabe der Datenträgerdetails vereinfacht. Sie müssen sich keine Gedanken um die Erstellung und Verwaltung von Speicherkonten machen.

Ein verwalteter Datenträger wird implizit erstellt, wenn ein virtueller Computer anhand eines Betriebssystemimages in Azure erstellt wird. Im Parameter ``storage_profile`` ist ``os_disk`` jetzt optional, und die Erstellung eines Speicherkontos ist keine Voraussetzung für die Erstellung eines virtuellen Computers.

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
Der Parameter ``storage_profile`` ist jetzt gültig. Ein vollständiges Beispiel zum Erstellen eines virtuellen Computers in Python (einschließlich Netzwerk usw.) finden Sie im vollständigen [Tutorial zu virtuellen Computern in Python](https://github.com/Azure-Samples/virtual-machines-python-manage).

Ein zuvor bereitgestellter verwalteter Datenträger kann ganz einfach angefügt werden.
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

## <a name="virtual-machine-scale-sets-with-managed-disks"></a>Skalierungsgruppen für virtuelle Computer mit Managed Disks

Vor der Einführung von verwalteten Datenträgern mussten Sie manuell ein Speicherkonto für alle virtuellen Computer erstellen, die in der Skalierungsgruppe enthalten sein sollten, und anschließend mit dem Auflistungsparameter ``vhd_containers`` den vollständigen Speicherkontonamen an die REST-API der Skalierungsgruppe übergeben. Das offizielle Handbuch für den Übergang finden Sie in diesem Artikel: `article <https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-convert-template-to-md>`.

Dank verwalteter Datenträger müssen Sie nun keine Speicherkonten mehr verwalten. Wenn Sie mit der Verwendung des VMSS Python SDK vertraut sind, können Sie nun das gleiche Speicherprofil (``storage_profile``) wie bei der Erstellung der virtuellen Computer verwenden:

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

Das vollständige Beispiel lautet wie folgt:

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

## <a name="other-operations-with-managed-disks"></a>Andere Vorgänge mit verwalteten Datenträgern

### <a name="resizing-a-managed-disk"></a>Ändern der Größe eines verwalteten Datenträgers

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

### <a name="update-the-storage-account-type-of-the-managed-disks"></a>Aktualisieren des Speicherkontotyps der verwalteten Datenträger
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

### <a name="create-an-image-from-blob-storage"></a>Erstellen eines Images über Blob Storage
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

### <a name="create-a-snapshot-of-a-managed-disk-that-is-currently-attached-to-a-virtual-machine"></a>Erstellen einer Momentaufnahme eines verwalteten Datenträgers, der derzeit an einen virtuellen Computer angefügt ist
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
