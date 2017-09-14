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

## <a name="example"></a>Beispiel
Abrufen eines [JSON-Webschlüssels](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) aus einem Schlüsseltresor.

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
[Informationen zu den Client-APIs](/python/api/overview/azure/keyvault/clientlibrary)

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
> [Informationen zu den Verwaltungs-APIs](/python/api/azure.mgmt.keyvault)

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/keyvault/managementlibrary)

## <a name="samples"></a>Beispiele
* [Verwalten von Schlüsseltresoren][1] 
* [Key Vault-Wiederherstellung][2]

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

Zeigen Sie die [vollständige Liste](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) von Beispielen für Azure Key Vault an. 