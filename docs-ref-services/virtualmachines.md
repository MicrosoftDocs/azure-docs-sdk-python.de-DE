---
title: "Azure Virtual Machines-Bibliotheken für Python"
description: 
keywords: Azure, Python, SDK, API, Compute, Virtual Machines
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/09/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: compute
ms.openlocfilehash: e2f2ad4e42bd847c9286333bacd583c3cd3f1b8c
ms.sourcegitcommit: 79afc8a1b427e26ecea7bdc0b7b3c898f143360f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2017
---
# <a name="azure-virtual-machine-libraries"></a>Azure Virtual Machines-Bibliotheken

## <a name="overview"></a>Übersicht

Bedarfsgesteuerte, skalierbare Computeressourcen unter Linux oder Windows

Informationen zu den ersten Schritten mit Azure Virtual Machines finden Sie unter [Erstellen einer Linux-VM mit dem Azure-Portal](/azure/virtual-machines/linux/quick-create-portal).

## <a name="management-api"></a>Verwaltungs-API

Mit der Verwaltungs-API können Sie virtuelle Windows- und Linux-Computer in Azure über Ihren Code erstellen, konfigurieren, verwalten und skalieren.

Installieren Sie die Bibliothek über pip:

```bash
pip install azure-mgmt-compute 
```   

### <a name="example"></a>Beispiel

Erstellen Sie einen neuen virtuellen Linux-Computer in einer vorhandenen Azure-Ressourcengruppe mit Authentifizierung über die verwaltete Dienstidentität (Managed Service Identity, MSI).

```python
VM_PARAMETERS={
        'location': 'LOCATION',
        'os_profile': {
            'computer_name': 'VM_NAME',
            'admin_username': 'USERNAME',
            'admin_password': 'PASSWORD'
        },
        'hardware_profile': {
            'vm_size': 'Standard_DS1_v2'
        },
        'storage_profile': {
            'image_reference': {
                'publisher': 'Canonical',
                'offer': 'UbuntuServer',
                'sku': '16.04.0-LTS',
                'version': 'latest'
            },
        },
        'network_profile': {
            'network_interfaces': [{
                'id': 'NIC_ID',
            }]
        },
    }

def create_vm()
    compute_client.virtual_machines.create_or_update(
        'RESOURCE_GROUP_NAME', 'VM_NAME', VM_PARAMETERS)
```

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/virtualmachines/managementlibrary)

## <a name="samples"></a>Beispiele

* [Verwalten virtueller Computer][1]
* [Authentifizieren mit der verwalteten Dienstidentität][2]
* [Verwalten eines Lastenausgleichs][3]
* [Erstellen und Konfigurieren von verwalteten Datenträgern][4]
* [Auflisten von Images][5] 
* [Überwachen virtueller Computer][6]

Zeigen Sie die [vollständige](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines) Liste von VM-Beispielen an.

[1]: https://azure.microsoft.com/resources/samples/virtual-machines-python-manage/
[2]: https://github.com/Azure-Samples/resource-manager-python-manage-resources-with-msi
[3]: https://azure.microsoft.com/resources/samples/network-python-manage-loadbalancer
[4]: ../docs-ref-conceptual/python-sdk-azure-samples-managed-disks.md
[5]: ../docs-ref-conceptual/python-sdk-azure-samples-list-images.md
[6]: ../docs-ref-conceptual/python-sdk-azure-samples-monitor-vms.md