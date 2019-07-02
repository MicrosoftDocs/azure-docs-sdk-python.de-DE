---
title: Azure Key Vault-Bibliotheken für Python
description: Referenzdokumentation für die Python-Clientbibliotheken für Azure Key Vault
author: sptramer
manager: carmonm
ms.author: sttramer
ms.date: 06/10/2019
ms.topic: conceptual
ms.devlang: python
ms.service: keyvault
ms.openlocfilehash: f4661ee389c13ce8546e7b5cc8866ab7b216d3b0
ms.sourcegitcommit: 92fa5dbcfd9a20f4a49da5f4bdc03045783d3495
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "67149327"
---
# <a name="azure-key-vault-libraries-for-python"></a><span data-ttu-id="25ac4-103">Azure Key Vault-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="25ac4-103">Azure Key Vault libraries for Python</span></span>

<span data-ttu-id="25ac4-104">[Azure Key Vault](/azure/key-vault/) ist das Speicher- und Verwaltungssystem von Azure für kryptografische Schlüssel, Geheimnisse und Zertifikatverwaltung.</span><span class="sxs-lookup"><span data-stu-id="25ac4-104">[Azure Key Vault](/azure/key-vault/) is Azure's storage and management system for cryptographic keys, secrets, and certificate management.</span></span> <span data-ttu-id="25ac4-105">Die Python SDK-API für Key Vault wird zwischen Clientbibliotheken und Verwaltungsbibliotheken aufgeteilt.</span><span class="sxs-lookup"><span data-stu-id="25ac4-105">The Python SDK API for Key Vault is split between client libraries and management libraries.</span></span>

<span data-ttu-id="25ac4-106">Verwenden Sie die Clientbibliothek für folgende Aktionen:</span><span class="sxs-lookup"><span data-stu-id="25ac4-106">Use the client library to:</span></span>
- <span data-ttu-id="25ac4-107">Zugreifen auf in Azure Key Vault gespeicherte Elemente sowie Aktualisieren oder Löschen dieser Elemente</span><span class="sxs-lookup"><span data-stu-id="25ac4-107">Access, update, or delete items stored in an Azure Key Vault</span></span>
- <span data-ttu-id="25ac4-108">Abrufen von Metadaten für gespeicherte Zertifikate</span><span class="sxs-lookup"><span data-stu-id="25ac4-108">Get metadata for stored certificates</span></span>
- <span data-ttu-id="25ac4-109">Überprüfen von Signaturen für symmetrische Schlüssel in Key Vault</span><span class="sxs-lookup"><span data-stu-id="25ac4-109">Verify signatures against symmetric keys in Key Vault</span></span>

<span data-ttu-id="25ac4-110">Verwenden Sie die Verwaltungsbibliothek für folgende Aktionen:</span><span class="sxs-lookup"><span data-stu-id="25ac4-110">Use the management library to:</span></span>
- <span data-ttu-id="25ac4-111">Erstellen, Aktualisieren oder Löschen neuer Key Vault-Speicher</span><span class="sxs-lookup"><span data-stu-id="25ac4-111">Create, update, or delete new Key Vault stores</span></span>
- <span data-ttu-id="25ac4-112">Steuern von Tresorzugriffsrichtlinien</span><span class="sxs-lookup"><span data-stu-id="25ac4-112">Control vault access policies</span></span>
- <span data-ttu-id="25ac4-113">Auflisten von Tresoren nach Abonnement oder Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="25ac4-113">List vaults by subscription or resource group</span></span>
- <span data-ttu-id="25ac4-114">Überprüfen der Verfügbarkeit von Tresornamen</span><span class="sxs-lookup"><span data-stu-id="25ac4-114">Check for vault name availability</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="25ac4-115">Installieren der Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="25ac4-115">Install the libraries</span></span>

### <a name="client-library"></a><span data-ttu-id="25ac4-116">Clientbibliothek</span><span class="sxs-lookup"><span data-stu-id="25ac4-116">Client library</span></span>

```bash
pip install azure-keyvault
```

## <a name="examples"></a><span data-ttu-id="25ac4-117">Beispiele</span><span class="sxs-lookup"><span data-stu-id="25ac4-117">Examples</span></span>

<span data-ttu-id="25ac4-118">Die folgenden Beispiele verwenden die Dienstprinzipalauthentifizierung. Dabei handelt es sich um die empfohlene Anmeldemethode für Anwendungen, die eine Verbindung mit Azure herstellen.</span><span class="sxs-lookup"><span data-stu-id="25ac4-118">The following examples use service principal authentication, which is the recommended sign in method for applications that connect to Azure.</span></span> <span data-ttu-id="25ac4-119">Informationen zur Dienstprinzipalauthentifizierung finden Sie unter [Authentifizieren bei den Azure-Verwaltungsbibliotheken für Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="25ac4-119">To learn about service principal authentication, see [Authenticate with the Azure SDK for Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate)</span></span>

<span data-ttu-id="25ac4-120">Abrufen des öffentlichen Teils eines asymmetrischen Schlüssels aus einem Tresor:</span><span class="sxs-lookup"><span data-stu-id="25ac4-120">Retrieve the public portion of an asymmetric key from a vault:</span></span>

```python
from azure.keyvault import KeyVaultClient
from azure.common.credentials import ServicePrincipalCredentials

credentials = ServicePrincipalCredentials(
    client_id = '...',
    secret = '...',
    tenant = '...'
)

client = KeyVaultClient(credentials)

# VAULT_URL must be in the format 'https://<vaultname>.vault.azure.net'
# KEY_VERSION is required, and can be obtained with the KeyVaultClient.get_key_versions(self, vault_url, key_name) API
key_bundle = client.get_key(VAULT_URL, KEY_NAME, KEY_VERSION)
key = key_bundle.key
```

<span data-ttu-id="25ac4-121">Abrufen eines Geheimnisses aus einem Tresor:</span><span class="sxs-lookup"><span data-stu-id="25ac4-121">Retrieve a secret from a vault:</span></span>

```python
from azure.keyvault import KeyVaultClient
from azure.common.credentials import ServicePrincipalCredentials

credentials = ServicePrincipalCredentials(
    client_id = '...',
    secret = '...',
    tenant = '...'
)

client = KeyVaultClient(credentials)

# VAULT_URL must be in the format 'https://<vaultname>.vault.azure.net'
# SECRET_VERSION is required, and can be obtained with the KeyVaultClient.get_secret_versions(self, vault_url, secret_id) API
secret_bundle = client.get_secret(VAULT_URL, SECRET_ID, SECRET_VERSION)
secret = secret_bundle.value
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="25ac4-122">Informationen zu den Client-APIs</span><span class="sxs-lookup"><span data-stu-id="25ac4-122">Explore the Client APIs</span></span>](/python/api/overview/azure/keyvault/client)

### <a name="management-library"></a><span data-ttu-id="25ac4-123">Verwaltungsbibliothek</span><span class="sxs-lookup"><span data-stu-id="25ac4-123">Management library</span></span>

```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a><span data-ttu-id="25ac4-124">Beispiel</span><span class="sxs-lookup"><span data-stu-id="25ac4-124">Example</span></span>

<span data-ttu-id="25ac4-125">Im folgenden Beispiel wird veranschaulicht, wie Sie eine Azure Key Vault-Instanz erstellen.</span><span class="sxs-lookup"><span data-stu-id="25ac4-125">The following example shows how to create an Azure Key Vault.</span></span> 

```python
from azure.mgmt.keyvault import KeyVaultManagementClient
from azure.common.credentials import ServicePrincipalCredentials


credentials = ServicePrincipalCredentials(
    client_id = '...',
    secret = '...',
    tenant = '...'
)

# Even when using service principal credentials, a subscription ID is required. For service principals,
# this should be the subscription used to create the service principal. Storing a token like a valid
# subscription ID in code is not recommended and only shown here for example purposes.
SUBSCRIPTION_ID = '...'
client = KeyVaultManagementClient(credentials, SUBSCRIPTION_ID)

# The object ID and organization ID (tenant) of the user, application, or service principal for access policies.
# These values can be found through the Azure CLI or the Portal.
ALLOW_OBJECT_ID = '...'
ALLOW_TENANT_ID = '...'

RESOURCE_GROUP = '...'
VAULT_NAME = '...'

# Vault properties may also be created by using the azure.mgmt.keyvault.models.VaultCreateOrUpdateParameters
# class, rather than a map. 
operation = client.vaults.create_or_update(
    RESOURCE_GROUP,
    VAULT_NAME,
    {
        'location': 'eastus',
        'properties': {
            'sku': {
                'name': 'standard'
            },
            'tenant_id': TENANT_ID,
            'access_policies': [{
                'object_id': OBJECT_ID,
                'tenant_id': ALLOW_TENANT_ID,
                'permissions': {
                    'keys': ['all'],
                    'secrets': ['all']
                }
            }]
        }
    }
)

vault = operation.result()
print(f'New vault URI: {vault.properties.vault_uri}')
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="25ac4-126">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="25ac4-126">Explore the Management APIs</span></span>](/python/api/overview/azure/keyvault/management)

## <a name="samples"></a><span data-ttu-id="25ac4-127">Beispiele</span><span class="sxs-lookup"><span data-stu-id="25ac4-127">Samples</span></span>
* <span data-ttu-id="25ac4-128">[Verwalten von Azure Key Vault-Instanzen][1]</span><span class="sxs-lookup"><span data-stu-id="25ac4-128">[Manage Azure Key Vaults][1]</span></span> 
* <span data-ttu-id="25ac4-129">[Azure Key Vault-Wiederherstellung][2]</span><span class="sxs-lookup"><span data-stu-id="25ac4-129">[Azure Key Vault recovery][2]</span></span>

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

<span data-ttu-id="25ac4-130">Zeigen Sie die [vollständige Liste](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) von Beispielen für Azure Key Vault an.</span><span class="sxs-lookup"><span data-stu-id="25ac4-130">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) of Azure Key Vault samples.</span></span> 
