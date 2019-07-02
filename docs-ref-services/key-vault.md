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
# <a name="azure-key-vault-libraries-for-python"></a>Azure Key Vault-Bibliotheken für Python

[Azure Key Vault](/azure/key-vault/) ist das Speicher- und Verwaltungssystem von Azure für kryptografische Schlüssel, Geheimnisse und Zertifikatverwaltung. Die Python SDK-API für Key Vault wird zwischen Clientbibliotheken und Verwaltungsbibliotheken aufgeteilt.

Verwenden Sie die Clientbibliothek für folgende Aktionen:
- Zugreifen auf in Azure Key Vault gespeicherte Elemente sowie Aktualisieren oder Löschen dieser Elemente
- Abrufen von Metadaten für gespeicherte Zertifikate
- Überprüfen von Signaturen für symmetrische Schlüssel in Key Vault

Verwenden Sie die Verwaltungsbibliothek für folgende Aktionen:
- Erstellen, Aktualisieren oder Löschen neuer Key Vault-Speicher
- Steuern von Tresorzugriffsrichtlinien
- Auflisten von Tresoren nach Abonnement oder Ressourcengruppe
- Überprüfen der Verfügbarkeit von Tresornamen

## <a name="install-the-libraries"></a>Installieren der Bibliotheken

### <a name="client-library"></a>Clientbibliothek

```bash
pip install azure-keyvault
```

## <a name="examples"></a>Beispiele

Die folgenden Beispiele verwenden die Dienstprinzipalauthentifizierung. Dabei handelt es sich um die empfohlene Anmeldemethode für Anwendungen, die eine Verbindung mit Azure herstellen. Informationen zur Dienstprinzipalauthentifizierung finden Sie unter [Authentifizieren bei den Azure-Verwaltungsbibliotheken für Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate).

Abrufen des öffentlichen Teils eines asymmetrischen Schlüssels aus einem Tresor:

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

Abrufen eines Geheimnisses aus einem Tresor:

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
> [Informationen zu den Client-APIs](/python/api/overview/azure/keyvault/client)

### <a name="management-library"></a>Verwaltungsbibliothek

```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a>Beispiel

Im folgenden Beispiel wird veranschaulicht, wie Sie eine Azure Key Vault-Instanz erstellen. 

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
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/keyvault/management)

## <a name="samples"></a>Beispiele
* [Verwalten von Azure Key Vault-Instanzen][1] 
* [Azure Key Vault-Wiederherstellung][2]

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

Zeigen Sie die [vollständige Liste](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) von Beispielen für Azure Key Vault an. 
