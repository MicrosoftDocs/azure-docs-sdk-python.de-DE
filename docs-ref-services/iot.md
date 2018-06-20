---
title: Azure IoT Hub-Bibliotheken für Python
description: Referenz zu Azure IoT Hub-Bibliotheken für Python
keywords: Azure, Python, SDK, API, Azure IoT Hub
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 07/10/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 0a1a5efa299f66ff8c31e8224e29dd7bcdc41783
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
ms.locfileid: "29478773"
---
# <a name="azure-iot-hub-libraries-for-python"></a><span data-ttu-id="3815e-104">Azure IoT Hub-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="3815e-104">Azure IoT Hub libraries for python</span></span>

## <a name="management-apipythonapioverviewazureiotmanagement"></a>[<span data-ttu-id="3815e-105">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="3815e-105">Management API</span></span>](/python/api/overview/azure/iot/management)

```bash
pip install azure-mgmt-iothub
```

## <a name="create-the-management-client"></a><span data-ttu-id="3815e-106">Erstellen des Verwaltungsclients</span><span class="sxs-lookup"><span data-stu-id="3815e-106">Create the management client</span></span>

<span data-ttu-id="3815e-107">Der folgende Code erstellt eine Instanz des Verwaltungsclients.</span><span class="sxs-lookup"><span data-stu-id="3815e-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="3815e-108">Sie müssen Ihre ``subscription_id`` angeben. Diese ID kann aus der [Abonnementliste](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping) abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="3815e-108">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="3815e-109">Informationen zur Azure Active Directory-Authentifizierung mit dem Python SDK sowie zum Erstellen einer ``Credentials``-Instanz finden Sie im Artikel zur [Authentifizierung bei der Ressourcenverwaltung](/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="3815e-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.iothub import IotHubClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

iothub_client = IotHubClient(
    credentials,
    subscription_id
)
```

## <a name="create-an-iothub"></a><span data-ttu-id="3815e-110">Erstellen eines IoT Hubs</span><span class="sxs-lookup"><span data-stu-id="3815e-110">Create an IoTHub</span></span>
```python
async_iot_hub = iothub_client.iot_hub_resource.create_or_update(
    'MyResourceGroup',
    'MyIoTHubAccount',
    {
        'location': 'westus',
        'subscriptionid': subscription_id,
        'resourcegroup': 'MyResourceGroup',
        'sku': {
            'name': 'S1',
            'capacity': 2
        },
        'properties': {
            'enable_file_upload_notifications': False,
            'operations_monitoring_properties': {
            'events': {
                "C2DCommands": "Error",
                "DeviceTelemetry": "Error",
                "DeviceIdentityOperations": "Error",
                "Connections": "Information"
            }
            },
            "features": "None",
        }
    }
)
iothub = async_iot_hub.result() # Blocking wait for creation
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="3815e-111">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="3815e-111">Explore the Management APIs</span></span>](/python/api/overview/azure/iot/management)