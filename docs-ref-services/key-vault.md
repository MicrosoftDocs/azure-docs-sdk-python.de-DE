---
title: Azure Key Vault-Bibliotheken für Python
description: Referenzdokumentation für die Python-Clientbibliotheken für Azure Key Vault
author: lisawong19
keywords: Azure, Python, SDK, API, Schlüssel, Key Vault, Authentifizierung, Geheimnis, Schlüssel, Sicherheit
manager: douge
ms.author: liwong
ms.date: 07/18/2017
ms.topic: article
ms.devlang: python
ms.service: keyvault
ms.openlocfilehash: e9ad2630a9004edfb3521f818307c134aa885315
ms.sourcegitcommit: fc9f0188879abc4afab8cc7d8aae8b2899133529
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2019
ms.locfileid: "55065069"
---
# <a name="azure-key-vault-libraries-for-python"></a>Azure Key Vault-Bibliotheken für Python

## <a name="overview"></a>Übersicht

Erstellen, aktualisieren und löschen Sie Schlüssel und Geheimnisse in Azure Key Vault mit den Clientbibliotheken.

Verwenden Sie die Azure Key Vault-Verwaltungsbibliotheken, um Schlüsseltresore zu erstellen, Anwendungen zu autorisieren und Berechtigungen zu verwalten. 

Weitere Informationen zu [Azure Key Vault](/azure/key-vault/key-vault-whatis)

## <a name="install-the-libraries"></a>Installieren der Bibliotheken

### <a name="client-library"></a>Clientbibliothek

```bash
pip install azure-keyvault
```

## <a name="examples"></a>Beispiele

Abrufen eines [JSON-Webschlüssels](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) aus einem Schlüsseltresor.

```python
from azure.keyvault import KeyVaultClient, KeyVaultAuthentication
from azure.common.credentials import ServicePrincipalCredentials

def auth_callback(server, resource, scope):
    credentials = ServicePrincipalCredentials(
        client_id = '',
        secret = '',
        tenant = '',
        resource = "https://vault.azure.net"
    )
    token = credentials.token
    return token['token_type'], token['access_token']

client = KeyVaultClient(KeyVaultAuthentication(auth_callback))

key_bundle = client.get_key(VAULT_URL, KEY_NAME, KEY_VERSION)
json_key = key_bundle.key
```

Analog dazu können Sie mit dem folgenden Codeausschnitt ein Geheimnis aus dem Tresor abrufen:

```python
from azure.keyvault import KeyVaultClient, KeyVaultAuthentication
from azure.common.credentials import ServicePrincipalCredentials

def auth_callback(server, resource, scope):
    credentials = ServicePrincipalCredentials(
        client_id = '',
        secret = '',
        tenant = '',
        resource = "https://vault.azure.net"
    )
    token = credentials.token
    return token['token_type'], token['access_token']

client = KeyVaultClient(KeyVaultAuthentication(auth_callback))

secret_bundle = client.get_secret(VAULT_URL, SECRET_ID, SECRET_VERSION)

print(secret_bundle.value)
```

> [!div class="nextstepaction"]
> [Informationen zu den Client-APIs](/python/api/overview/azure/keyvault/client)

### <a name="management-api"></a>Verwaltungs-API

```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a>Beispiel
Im folgenden Beispiel wird veranschaulicht, wie Sie eine Azure Key Vault-Instanz erstellen. 

```python
from azure.mgmt.keyvault import KeyVaultManagementClient

GROUP_NAME = 'your_resource_group_name'
KV_NAME = 'your_key_vault_name'
#The object ID of the User or Application for access policies. Find this number in the portal
OBJECT_ID = '00000000-0000-0000-0000-000000000000'
TENANT_ID = os.environ['AZURE_TENANT_ID']

kv_client = KeyVaultManagementClient(credentials, subscription_id)

operation = kv_client.vaults.create_or_update(
    GROUP_NAME,
    KV_NAME,
    {
        'location': 'eastus',
        'properties': {
            'sku': {
                'name': 'standard'
            },
            'tenant_id': TENANT_ID,
            'access_policies': [{
                'tenant_id': TENANT_ID,
                'object_id': OBJECT_ID,
                'permissions': {
                    'keys': ['all'],
                    'secrets': ['all']
                }
            }]
        }
    }
)

vault = operation.result()

VAULT_URI = vault.properties.vault_uri
```
> [!div class="nextstepaction"]
> [Informationen zu den Client-APIs](/python/api/overview/azure/keyvault/client)

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/keyvault/management)

## <a name="samples"></a>Beispiele
* [Verwalten von Schlüsseltresoren][1] 
* [Key Vault-Wiederherstellung][2]

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

Zeigen Sie die [vollständige Liste](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) von Beispielen für Azure Key Vault an. 
