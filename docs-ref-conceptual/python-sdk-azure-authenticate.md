---
title: Authentifizieren bei den Azure-Verwaltungsbibliotheken für Python
description: Authentifizieren mit einem Dienstprinzipal bei den Azure-Verwaltungsbibliotheken für Python
keywords: Azure, Python, SDK, API, Authentifizierung, Active Directory, Dienstprinzipal
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 04/11/2019
ms.topic: article
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 51f26b120cefffd2d7f4af9c2b6b2cb532bc6006
ms.sourcegitcommit: 375a1f9180eb1323fe2af0a7e28fd4676973c68e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2019
ms.locfileid: "59586808"
---
# <a name="authenticate-with-the-azure-management-libraries-for-python"></a>Authentifizieren bei den Azure-Verwaltungsbibliotheken für Python

Wenn Sie mithilfe der Python-Verwaltungsbibliotheken Ressourcen erstellen und verwalten, stehen verschiedene Optionen zum Authentifizieren Ihrer Anwendung bei Azure zur Verfügung.

## <a name="mgmt-auth-token"></a>Authentifizieren mit Tokenanmeldeinformationen

Speichern Sie die Anmeldeinformationen sicher in einer Konfigurationsdatei, der Registrierung oder Azure Key Vault.

Im folgenden Beispiel wird ein [Dienstprinzipal](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) für die Authentifizierung verwendet.

> [!NOTE]
> Verwenden Sie zum Erstellen eines Dienstprinzipals mit der Azure CLI den folgenden Befehl:
>
> ```bash
> az ad sp create-for-rbac --name "MY-PRINCIPAL-NAME" --password "STRONG-SECRET-PASSWORD"
> ```
>
> Weitere Informationen zum Einrichten von Dienstprinzipalen mit der CLI finden Sie unter [Erstellen eines Azure-Dienstprinzipals mit der Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli).

```python
from azure.common.credentials import ServicePrincipalCredentials

# Tenant ID for your Azure subscription
TENANT_ID = '<Your tenant ID>'

# Your service principal App ID
CLIENT = '<Your service principal ID>'

# Your service principal password
KEY = '<Your service principal password>'

credentials = ServicePrincipalCredentials(
    client_id = CLIENT,
    secret = KEY,
    tenant = TENANT_ID
)
```

> [HINWEIS!] Verwenden Sie zum Herstellen einer Verbindung mit einer der unabhängigen Azure-Clouds den `cloud_environment`-Parameter.
>
> ```python
> from azure.common.credentials import ServicePrincipalCredentials
> from msrestazure.azure_cloud import AZURE_CHINA_CLOUD
> 
> # Tenant ID for your Azure Subscription
> TENANT_ID = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
> 
> # Your Service Principal App ID
> CLIENT = 'a2ab11af-01aa-4759-8345-7803287dbd39'
> 
> # Your Service Principal Password
> KEY = 'password'
> 
> credentials = ServicePrincipalCredentials(
>     client_id = CLIENT,
>     secret = KEY,
>     tenant = TENANT_ID,
>     cloud_environment = AZURE_CHINA_CLOUD
> )
> ```

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

> [HINWEIS!] Bei Verwendung einer unabhängigen Azure-Cloud müssen Sie beim Erstellen des Verwaltungsclients auch die entsprechende Basis-URL (über die Konstanten in `msrestazure.azure_cloud`) angeben. Beispiel für Azure-Cloud in China:
> ```python
> client = ComputeManagementClient(credentials, subscription_id,
>     base_url=AZURE_CHINA_CLOUD.endpoints.resource_manager)
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
    "clientId": "<Service principal ID>",
    "clientSecret": "<Service principal secret/password>",
    "subscriptionId": "<Subscription associated with the service principal>",
    "tenantId": "<The service principal's tenant>",
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

## <a name="mgmt-auth-msi"></a>Authentifizieren mit verwalteten Azure-Identitäten
Über verwaltete Azure-Identitäten kann eine Ressource in Azure ganz einfach das SDK oder die CLI nutzen, ohne spezielle Anmeldeinformationen erstellen zu müssen.

> [!IMPORTANT]
>
> Wenn Sie verwaltete Identitäten nutzen möchten, müssen Sie über eine Azure-Ressource (etwa eine Azure-Funktion oder einen in Azure ausgeführten virtuellen Computer) eine Verbindung mit Azure herstellen. Informationen zum Konfigurieren einer verwalteten Identität für eine Ressource finden Sie unter [Konfigurieren von verwalteten Identitäten für Azure-Ressourcen auf einem virtuellen Azure-Computer mithilfe der Azure-Befehlszeilenschnittstelle](/azure/active-directory/managed-identities-azure-resources/qs-configure-cli-windows-vm) und [Verwenden von verwalteten Identitäten für Azure-Ressourcen auf einem virtuellen Azure-Computer für die Anmeldung](/azure/active-directory/managed-identities-azure-resources/how-to-use-vm-sign-in).

```python
from msrestazure.azure_active_directory import MSIAuthentication
from azure.mgmt.resource import ResourceManagementClient, SubscriptionClient

# Create MSI Authentication
credentials = MSIAuthentication()


# Create a Subscription Client
subscription_client = SubscriptionClient(credentials)
subscription = next(subscription_client.subscriptions.list())
subscription_id = subscription.subscription_id

# Create a Resource Management client
resource_client = ResourceManagementClient(credentials, subscription_id)


# List resource groups as an example. The only limit is what role and policy are assigned to this MSI token.
for resource_group in resource_client.resource_groups.list():
    print(resource_group.name)
```

## <a name="mgmt-auth-cli"></a>CLI-basierte Authentifizierung

Das SDK kann mithilfe Ihres aktiven Azure CLI-Abonnements einen Client erstellen.

> [!IMPORTANT]
> Diese Vorgehensweise sollte als Schnellstart für Entwickler verwendet werden. Verwenden Sie zu Produktionszwecken [ADAL](#mgmt-auth-legacy) oder Ihr eigenes System für Anmeldeinformationen.
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
    'my_smart_password'
)
```
