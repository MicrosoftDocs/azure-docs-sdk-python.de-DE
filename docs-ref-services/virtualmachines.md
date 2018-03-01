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
ms.openlocfilehash: adea3dfd1e38fb8c880009d5a02ab2b8be2a67e1
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
---
# <a name="azure-virtual-machine-libraries"></a><span data-ttu-id="7bc43-103">Azure Virtual Machines-Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="7bc43-103">Azure virtual machine libraries</span></span>

## <a name="overview"></a><span data-ttu-id="7bc43-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="7bc43-104">Overview</span></span>

<span data-ttu-id="7bc43-105">Bedarfsgesteuerte, skalierbare Computeressourcen unter Linux oder Windows</span><span class="sxs-lookup"><span data-stu-id="7bc43-105">On-demand, scalable computing resources running Linux or Windows.</span></span>

<span data-ttu-id="7bc43-106">Informationen zu den ersten Schritten mit Azure Virtual Machines finden Sie unter [Erstellen einer Linux-VM mit dem Azure-Portal](/azure/virtual-machines/linux/quick-create-portal).</span><span class="sxs-lookup"><span data-stu-id="7bc43-106">To get started with Azure Virtual Machines, see [Create a Linux virtual machine with the Azure portal](/azure/virtual-machines/linux/quick-create-portal).</span></span>

## <a name="management-api"></a><span data-ttu-id="7bc43-107">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="7bc43-107">Management API</span></span>

<span data-ttu-id="7bc43-108">Mit der Verwaltungs-API können Sie virtuelle Windows- und Linux-Computer in Azure über Ihren Code erstellen, konfigurieren, verwalten und skalieren.</span><span class="sxs-lookup"><span data-stu-id="7bc43-108">Create, configure, manage and scale Windows and Linux virtual machines in Azure from your code with the management API.</span></span>

<span data-ttu-id="7bc43-109">Installieren Sie die Bibliothek über pip:</span><span class="sxs-lookup"><span data-stu-id="7bc43-109">Install the library via pip.</span></span>

```bash
pip install azure-mgmt-compute 
```   

### <a name="example"></a><span data-ttu-id="7bc43-110">Beispiel</span><span class="sxs-lookup"><span data-stu-id="7bc43-110">Example</span></span>

<span data-ttu-id="7bc43-111">Erstellen Sie einen neuen virtuellen Linux-Computer in einer vorhandenen Azure-Ressourcengruppe mit Authentifizierung über die verwaltete Dienstidentität (Managed Service Identity, MSI).</span><span class="sxs-lookup"><span data-stu-id="7bc43-111">Create a new Linux virtual machine in an existing Azure resource group with Managed Service Identity(MSI) authentication.</span></span>

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
> [<span data-ttu-id="7bc43-112">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="7bc43-112">Explore the Management APIs</span></span>](/python/api/overview/azure/virtualmachines/management)

## <a name="samples"></a><span data-ttu-id="7bc43-113">Beispiele</span><span class="sxs-lookup"><span data-stu-id="7bc43-113">Samples</span></span>

* <span data-ttu-id="7bc43-114">[Verwalten virtueller Computer][1]</span><span class="sxs-lookup"><span data-stu-id="7bc43-114">[Manage virtual machines][1]</span></span>
* <span data-ttu-id="7bc43-115">[Authentifizieren mit der verwalteten Dienstidentität][2]</span><span class="sxs-lookup"><span data-stu-id="7bc43-115">[Authenticate with Managed Service Identity][2]</span></span>
* <span data-ttu-id="7bc43-116">[Erstellen eines virtuellen Computers mit der Erweiterung für die verwaltete Dienstidentität][3]</span><span class="sxs-lookup"><span data-stu-id="7bc43-116">[Create a virtual machine with Managed Service Identity Extension][3]</span></span>
* <span data-ttu-id="7bc43-117">[Verwalten eines Lastenausgleichs][4]</span><span class="sxs-lookup"><span data-stu-id="7bc43-117">[Manage a load balancer][4]</span></span>
* <span data-ttu-id="7bc43-118">[Erstellen und Konfigurieren von verwalteten Datenträgern][5]</span><span class="sxs-lookup"><span data-stu-id="7bc43-118">[Create and configure managed disks][5]</span></span>
* <span data-ttu-id="7bc43-119">[Auflisten von Images][6]</span><span class="sxs-lookup"><span data-stu-id="7bc43-119">[List images][6]</span></span> 
* <span data-ttu-id="7bc43-120">[Überwachen virtueller Computer][7]</span><span class="sxs-lookup"><span data-stu-id="7bc43-120">[Monitor virtual machines][7]</span></span>

<span data-ttu-id="7bc43-121">Zeigen Sie die [vollständige](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines) Liste von VM-Beispielen an.</span><span class="sxs-lookup"><span data-stu-id="7bc43-121">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines) of virtual machine samples.</span></span>

[1]: https://azure.microsoft.com/resources/samples/virtual-machines-python-manage/
[2]: https://github.com/Azure-Samples/resource-manager-python-manage-resources-with-msi
[3]: https://github.com/Azure-Samples/compute-python-msi-vm
[4]: https://azure.microsoft.com/resources/samples/network-python-manage-loadbalancer
[5]: ../docs-ref-conceptual/python-sdk-azure-samples-managed-disks.md
[6]: ../docs-ref-conceptual/python-sdk-azure-samples-list-images.md
[7]: ../docs-ref-conceptual/python-sdk-azure-samples-monitor-vms.md