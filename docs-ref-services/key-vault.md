---
title: "Azure Key Vault-Bibliotheken für Python"
description: "Referenzdokumentation für die Python-Clientbibliotheken für Azure Key Vault"
author: lisawong19
keywords: "Azure, Python, SDK, API, Schlüssel, Key Vault, Authentifizierung, Geheimnis, Schlüssel, Sicherheit"
manager: douge
ms.author: liwong
ms.date: 07/18/2017
ms.topic: article
ms.devlang: python
ms.service: keyvault
ms.openlocfilehash: 3eac46eb4d5d19273ead9f19b739f6fb6d72e5cc
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2017
---
# <a name="azure-key-vault-libraries-for-python"></a><span data-ttu-id="a029e-104">Azure Key Vault-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="a029e-104">Azure Key Vault libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="a029e-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="a029e-105">Overview</span></span>

<span data-ttu-id="a029e-106">Erstellen, aktualisieren und löschen Sie Schlüssel und Geheimnisse in Azure Key Vault mit den Clientbibliotheken.</span><span class="sxs-lookup"><span data-stu-id="a029e-106">Create, update, and delete keys and secrets in Azure Key Vault with the client libraries.</span></span>

<span data-ttu-id="a029e-107">Verwenden Sie die Azure Key Vault-Verwaltungsbibliotheken, um Schlüsseltresore zu erstellen, Anwendungen zu autorisieren und Berechtigungen zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="a029e-107">Use the Azure Key Vault management libraries to create key vaults, authorize applications, and manage permissions.</span></span> 

<span data-ttu-id="a029e-108">Weitere Informationen zu [Azure Key Vault](/azure/key-vault/key-vault-whatis)</span><span class="sxs-lookup"><span data-stu-id="a029e-108">Learn more about [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="a029e-109">Installieren der Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="a029e-109">Install the libraries</span></span>

### <a name="client-library"></a><span data-ttu-id="a029e-110">Clientbibliothek</span><span class="sxs-lookup"><span data-stu-id="a029e-110">Client library</span></span>
```bash
pip install azure-keyvault
```

## <a name="example"></a><span data-ttu-id="a029e-111">Beispiel</span><span class="sxs-lookup"><span data-stu-id="a029e-111">Example</span></span>
<span data-ttu-id="a029e-112">Abrufen eines [JSON-Webschlüssels](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) aus einem Schlüsseltresor.</span><span class="sxs-lookup"><span data-stu-id="a029e-112">Retrieve a [JSON web key](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) from a Key Vault.</span></span>

```python
from azure.keyvault import KeyVaultClient, KeyVaultAuthentication
from azure.common.credentials import ServicePrincipalCredentials

credentials = None

def auth_callack(server, resource, scope):
    credentials = credentials or ServicePrincipalCredentials(
        client_id = '', #client id
        secret = '',
        tenant = '',
        resource = resource
    )
    token = credentials.token
    return token['token_type'], token['access_token']

client = KeyVaultClient(KeyVaultAuthentication(auth_callack))

key_bundle = client.get_key(vault_url, key_name, key_version)
json_key = key_bundle.key
```
[!div class="nextstepaction"]
[<span data-ttu-id="a029e-113">Informationen zu den Client-APIs</span><span class="sxs-lookup"><span data-stu-id="a029e-113">Explore the Client APIs</span></span>](/python/api/overview/azure/keyvault/clientlibrary)

### <a name="management-api"></a><span data-ttu-id="a029e-114">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="a029e-114">Management API</span></span>
```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a><span data-ttu-id="a029e-115">Beispiel</span><span class="sxs-lookup"><span data-stu-id="a029e-115">Example</span></span>
<span data-ttu-id="a029e-116">Im folgenden Beispiel wird veranschaulicht, wie Sie eine Azure Key Vault-Instanz erstellen.</span><span class="sxs-lookup"><span data-stu-id="a029e-116">The following example shows how to create an Azure Key Vault.</span></span> 

```python
from azure.mgmt.keyvault import KeyVaultManagementClient

GROUP_NAME = 'your_resource_group_name'
KV_NAME = 'your_key_vault_name'
#The object ID of the User or Application for access policies. Find this number in the portal
OBJECT_ID = '00000000-0000-0000-0000-000000000000'

kv_client = KeyVaultManagementClient(credentials, subscription_id)

vault = kv_client.vaults.create_or_update(
    GROUP_NAME,
    KV_NAME,
    {
        'location': 'eastus',
        'properties': {
            'sku': {
                'name': 'standard'
            },
            'tenant_id': os.environ['AZURE_TENANT_ID'],
            'access_policies': [{
                'tenant_id': os.environ['AZURE_TENANT_ID'],
                'object_id': OBJECT_ID,
                'permissions': {
                    'keys': ['all'],
                    'secrets': ['all']
                }
            }]
        }
    }
)
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="a029e-117">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="a029e-117">Explore the Management APIs</span></span>](/python/api/azure.mgmt.keyvault)

> [!div class="nextstepaction"]
> [<span data-ttu-id="a029e-118">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="a029e-118">Explore the Management APIs</span></span>](/python/api/overview/azure/keyvault/managementlibrary)

## <a name="samples"></a><span data-ttu-id="a029e-119">Beispiele</span><span class="sxs-lookup"><span data-stu-id="a029e-119">Samples</span></span>
* <span data-ttu-id="a029e-120">[Verwalten von Schlüsseltresoren][1]</span><span class="sxs-lookup"><span data-stu-id="a029e-120">[Manage Key Vaults][1]</span></span> 
* <span data-ttu-id="a029e-121">[Key Vault-Wiederherstellung][2]</span><span class="sxs-lookup"><span data-stu-id="a029e-121">[Key Vault recovery][2]</span></span>

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

<span data-ttu-id="a029e-122">Zeigen Sie die [vollständige Liste](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) von Beispielen für Azure Key Vault an.</span><span class="sxs-lookup"><span data-stu-id="a029e-122">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) of Azure Key Vault samples.</span></span> 