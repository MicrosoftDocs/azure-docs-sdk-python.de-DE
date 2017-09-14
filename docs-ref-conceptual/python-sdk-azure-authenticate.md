---
title: "Authentifizieren bei den Azure-Verwaltungsbibliotheken für Python"
description: "Authentifizieren mit einem Dienstprinzipal bei den Azure-Verwaltungsbibliotheken für Python"
keywords: Azure, Python, SDK, API, Authentifizierung, Active Directory, Dienstprinzipal
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/24/2017
ms.topic: article
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.assetid: 
ms.openlocfilehash: 1dba0bdd9b543c11b31f3001737038e7e99daf08
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2017
---
# <a name="authenticate-with-the-azure-management-libraries-for-python"></a>Authentifizieren bei den Azure-Verwaltungsbibliotheken für Python

Wenn Sie mithilfe der Python-Verwaltungsbibliotheken Ressourcen erstellen und verwalten, stehen verschiedene Optionen zum Authentifizieren Ihrer Anwendung bei Azure zur Verfügung.

## <a name="mgmt-auth-token"></a>Authentifizieren mit Tokenanmeldeinformationen

Speichern Sie die Anmeldeinformationen sicher in einer Konfigurationsdatei, der Registrierung oder Azure Key Vault.

Im folgenden Beispiel wird ein [Dienstprinzipal](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) für die Authentifizierung verwendet.

> [!NOTE]
> Ein Dienstprinzipal kann mit der Azure CLI 2.0 erstellt werden.
> ```bash
> az ad sp create-for-rbac --name "MY-PRINCIPAL-NAME" --password "STRONG-SECRET-PASSWORD"
> ```

```python
    from azure.common.credentials import ServicePrincipalCredentials

    # Tenant ID for your Azure Subscription
    TENANT_ID = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'

    # Your Service Principal App ID
    CLIENT = 'a2ab11af-01aa-4759-8345-7803287dbd39'

    # Your Service Principal Password
    KEY = 'password'

    credentials = ServicePrincipalCredentials(
        client_id = CLIENT,
        secret = KEY,
        tenant = TENANT_ID
    )
```

> [Hinweis!] Verwenden Sie zum Herstellen einer Verbindung mit einer der unabhängigen Azure-Clouds den `cloud_environment`-Parameter.

```python
    from azure.common.credentials import ServicePrincipalCredentials
    from msrestazure.azure_cloud import AZURE_CHINA_CLOUD

    # Tenant ID for your Azure Subscription
    TENANT_ID = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'

    # Your Service Principal App ID
    CLIENT = 'a2ab11af-01aa-4759-8345-7803287dbd39'

    # Your Service Principal Password
    KEY = 'password'

    credentials = ServicePrincipalCredentials(
        client_id = CLIENT,
        secret = KEY,
        tenant = TENANT_ID,
        cloud_environment = AZURE_CHINA_CLOUD
    )
```

Wenn Sie mehr Kontrolle benötigen, wird die Verwendung von [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) und vom SDK-ADAL-Wrapper empfohlen. Eine Liste aller verfügbaren Szenarien und Beispiele finden Sie auf der ADAL-Website. Dort finden Sie beispielsweise Informationen zur Dienstprinzipalauthentifizierung:

```python
    import adal
    from msrestazure.azure_active_directory import AdalAuthentication
    from msrestazure.azure_cloud import AZURE_PUBLIC_CLOUD

    # Tenant ID for your Azure Subscription
    TENANT_ID = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'

    # Your Service Principal App ID
    CLIENT = 'a2ab11af-01aa-4759-8345-7803287dbd39'

    # Your Service Principal Password
    KEY = 'password'

    LOGIN_ENDPOINT = AZURE_PUBLIC_CLOUD.endpoints.active_directory
    RESOURCE = AZURE_PUBLIC_CLOUD.endpoints.active_directory_resource_id

    context = adal.AuthenticationContext(LOGIN_ENDPOINT + '/' + TENANT_ID)
    credentials = AdalAuthentication(
        context.acquire_token_with_client_credentials,
        RESOURCE,
        CLIENT,
        KEY
    )
```

Alle gültigen ADAL-Aufrufe können mit der `AdalAuthentication`-Klasse verwendet werden.

Erstellen Sie als Nächstes ein Clientobjekt, um mit der Verwendung der API zu beginnen:

```python
from azure.mgmt.compute import ComputeManagementClient

# Your Azure Subscription ID
subscription_id = '33333333-3333-3333-3333-333333333333'

client = ComputeManagementClient(credentials, subscription_id)
```

> [Hinweis!] Bei Verwendung einer unabhängigen Azure-Cloud müssen Sie beim Erstellen des Verwaltungsclients auch die entsprechende Basis-URL (über die Konstanten in `msrestazure.azure_cloud`) angeben. Beispiel für Azure-Cloud in China:
> ```python
> client = ComputeManagementClient(credentials, subscription_id,
>     base_url=AZURE_CHINA_CLOUD.endpoints.active_directory_resource_id)
> ```

## <a name="mgmt-auth-file"></a>Dateibasierte Authentifizierung

Die einfachste Authentifizierungsmethode besteht in der Erstellung einer JSON-Datei mit Anmeldeinformationen für einen Azure-Dienstprinzipal. Mit dem folgenden CLI-Befehl können Sie zum gleichen Zeitpunkt einen neuen Dienstprinzipal und diese Datei erstellen:

```bash
az ad sp create-for-rbac --sdk-auth > mycredentials.json
```

Speichern Sie diese Datei an einem sicheren Ort in Ihrem System, an dem sie vom Code gelesen werden kann. Legen Sie eine Umgebungsvariable mit dem vollständigen Pfad zur Datei in der Shell fest:

```bash
export AZURE_AUTH_LOCATION=~/.azure/azure_credentials.json
```

Wenn Sie die Datei selbst erstellen möchten, halten Sie sich an das folgende Format:

```json
{
    "clientId": "ad735158-65ca-11e7-ba4d-ecb1d756380e",
    "clientSecret": "b70bb224-65ca-11e7-810c-ecb1d756380e",
    "subscriptionId": "bfc42d3a-65ca-11e7-95cf-ecb1d756380e",
    "tenantId": "c81da1d8-65ca-11e7-b1d1-ecb1d756380e",
    "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
    "resourceManagerEndpointUrl": "https://management.azure.com/",
    "activeDirectoryGraphResourceId": "https://graph.windows.net/",
    "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
    "galleryEndpointUrl": "https://gallery.azure.com/",
    "managementEndpointUrl": "https://management.core.windows.net/"
}
```

Sie können dann einen beliebigen Client mit der Clientfactory erstellen:
```python
from azure.common.client_factory import get_client_from_auth_file
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_auth_file(ComputeManagementClient)
```


## <a name="mgmt-auth-cli"></a>CLI-basierte Authentifizierung

Das SDK kann mithilfe Ihres aktiven CLI-Abonnements einen Client erstellen.

> [!IMPORTANT]
> Diese Vorgehensweise sollte als Schnellstart für Entwickler verwendet werden. Verwenden Sie zu Produktionszwecken [ADAL](#authenticate-with-token-credentials) oder Ihr eigenes System für Anmeldeinformationen.
> Alle Änderungen an der CLI-Konfiguration wirken sich auf die SDK-Ausführung aus.

Verwenden Sie zum Definieren der aktiven Anmeldeinformationen [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).
Bei der standardmäßigen Abonnement-ID handelt es sich um die ID, die Sie bereits besitzen. Alternativ können Sie die ID mit [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli) festlegen.

```python
from azure.common.client_factory import get_client_from_cli_profile
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_cli_profile(ComputeManagementClient)
```

## <a name="mgmt-auth-legacy"></a>Authentifizieren mit Tokenanmeldeinformationen (Legacy)

In der vorherigen Version des SDK war ADAL noch nicht verfügbar, und es wurde eine `UserPassCredentials`-Klasse bereitgestellt. Diese wird als veraltet betrachtet und sollte nicht mehr verwendet werden.

In diesem Beispiel wird das Szenario mit Benutzername und Kennwort gezeigt. 2FA wird dabei nicht unterstützt.

```python
    from azure.common.credentials import UserPassCredentials

    credentials = UserPassCredentials(
        'user@domain.com',
        'my_smart_password',
    )
```
