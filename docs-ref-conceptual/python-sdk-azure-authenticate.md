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
ms.openlocfilehash: 5c4cf1dee7d9864e809f2797ad49ce78886a6f66
ms.sourcegitcommit: c57305dad01cad925faf50a64953c408429d4ca9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="authenticate-with-the-azure-management-libraries-for-python"></a><span data-ttu-id="c2c42-104">Authentifizieren bei den Azure-Verwaltungsbibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="c2c42-104">Authenticate with the Azure Management Libraries for Python</span></span>

<span data-ttu-id="c2c42-105">Wenn Sie mithilfe der Python-Verwaltungsbibliotheken Ressourcen erstellen und verwalten, stehen verschiedene Optionen zum Authentifizieren Ihrer Anwendung bei Azure zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="c2c42-105">Several options are available to authenticate your application with Azure when using the Python management libraries to create and manage resources.</span></span>

## <a name="mgmt-auth-token"></a><span data-ttu-id="c2c42-106">Authentifizieren mit Tokenanmeldeinformationen</span><span class="sxs-lookup"><span data-stu-id="c2c42-106">Authenticate with token credentials</span></span>

<span data-ttu-id="c2c42-107">Speichern Sie die Anmeldeinformationen sicher in einer Konfigurationsdatei, der Registrierung oder Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c2c42-107">Store the credentials securely in a configuration file, the registry, or Azure KeyVault.</span></span>

<span data-ttu-id="c2c42-108">Im folgenden Beispiel wird ein [Dienstprinzipal](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) für die Authentifizierung verwendet.</span><span class="sxs-lookup"><span data-stu-id="c2c42-108">The following example uses a [Service Principal](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) for authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="c2c42-109">Ein Dienstprinzipal kann mit der Azure CLI 2.0 erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="c2c42-109">You can create a Service Principal via the Azure CLI 2.0</span></span>
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

> <span data-ttu-id="c2c42-110">[HINWEIS!] Verwenden Sie zum Herstellen einer Verbindung mit einer der unabhängigen Azure-Clouds den `cloud_environment`-Parameter.</span><span class="sxs-lookup"><span data-stu-id="c2c42-110">[NOTE!] To connect to one of the Azure sovereign clouds, use the `cloud_environment` parameter.</span></span>

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

<span data-ttu-id="c2c42-111">Wenn Sie mehr Kontrolle benötigen, wird die Verwendung von [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) und vom SDK-ADAL-Wrapper empfohlen.</span><span class="sxs-lookup"><span data-stu-id="c2c42-111">If you need more control, it is recommended to use [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) and the SDK ADAL wrapper.</span></span> <span data-ttu-id="c2c42-112">Eine Liste aller verfügbaren Szenarien und Beispiele finden Sie auf der ADAL-Website.</span><span class="sxs-lookup"><span data-stu-id="c2c42-112">Please refer to the ADAL website for all the available scenarios list and samples.</span></span> <span data-ttu-id="c2c42-113">Dort finden Sie beispielsweise Informationen zur Dienstprinzipalauthentifizierung:</span><span class="sxs-lookup"><span data-stu-id="c2c42-113">For instance for service principal authentication:</span></span>

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

<span data-ttu-id="c2c42-114">Alle gültigen ADAL-Aufrufe können mit der `AdalAuthentication`-Klasse verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="c2c42-114">All ADAL valid calls can be used with the `AdalAuthentication` class.</span></span>

<span data-ttu-id="c2c42-115">Erstellen Sie als Nächstes ein Clientobjekt, um mit der Verwendung der API zu beginnen:</span><span class="sxs-lookup"><span data-stu-id="c2c42-115">Next, create a client object to start working with the API:</span></span>

```python
from azure.mgmt.compute import ComputeManagementClient

# Your Azure Subscription ID
subscription_id = '33333333-3333-3333-3333-333333333333'

client = ComputeManagementClient(credentials, subscription_id)
```

> <span data-ttu-id="c2c42-116">[HINWEIS!] Bei Verwendung einer unabhängigen Azure-Cloud müssen Sie beim Erstellen des Verwaltungsclients auch die entsprechende Basis-URL (über die Konstanten in `msrestazure.azure_cloud`) angeben.</span><span class="sxs-lookup"><span data-stu-id="c2c42-116">[NOTE!] When using an Azure sovereign cloud you must also specify the appropriate base URL (via the constants in `msrestazure.azure_cloud`) when creating the management client.</span></span> <span data-ttu-id="c2c42-117">Beispiel für Azure-Cloud in China:</span><span class="sxs-lookup"><span data-stu-id="c2c42-117">For example for Azure China Cloud:</span></span>
> ```python
> client = ComputeManagementClient(credentials, subscription_id,
>     base_url=AZURE_CHINA_CLOUD.endpoints.active_directory_resource_id)
> ```


## <a name="mgmt-auth-file"></a><span data-ttu-id="c2c42-118">Dateibasierte Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="c2c42-118">File based authentication</span></span>

<span data-ttu-id="c2c42-119">Die einfachste Authentifizierungsmethode besteht in der Erstellung einer JSON-Datei mit Anmeldeinformationen für einen Azure-Dienstprinzipal.</span><span class="sxs-lookup"><span data-stu-id="c2c42-119">The simplest way to authenticate is to create a JSON file that contains credentials for an Azure Service Principal.</span></span> <span data-ttu-id="c2c42-120">Mit dem folgenden CLI-Befehl können Sie zum gleichen Zeitpunkt einen neuen Dienstprinzipal und diese Datei erstellen:</span><span class="sxs-lookup"><span data-stu-id="c2c42-120">You can use the following CLI command to create a new Service Principal and this file at the same time:</span></span>

```bash
az ad sp create-for-rbac --sdk-auth > mycredentials.json
```

<span data-ttu-id="c2c42-121">Speichern Sie diese Datei an einem sicheren Ort in Ihrem System, an dem sie vom Code gelesen werden kann.</span><span class="sxs-lookup"><span data-stu-id="c2c42-121">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="c2c42-122">Legen Sie eine Umgebungsvariable mit dem vollständigen Pfad zur Datei in der Shell fest:</span><span class="sxs-lookup"><span data-stu-id="c2c42-122">Set an environment variable with the full path to the file in your shell:</span></span>

```bash
export AZURE_AUTH_LOCATION=~/.azure/azure_credentials.json
```

<span data-ttu-id="c2c42-123">Wenn Sie die Datei selbst erstellen möchten, halten Sie sich an das folgende Format:</span><span class="sxs-lookup"><span data-stu-id="c2c42-123">If you want to create the file yourself, please follow this format:</span></span>

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

<span data-ttu-id="c2c42-124">Sie können dann einen beliebigen Client mit der Clientfactory erstellen:</span><span class="sxs-lookup"><span data-stu-id="c2c42-124">You can then create any client using the client factory:</span></span>
```python
from azure.common.client_factory import get_client_from_auth_file
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_auth_file(ComputeManagementClient)
```

## <a name="mgmt-auth-msi"></a><span data-ttu-id="c2c42-125">Authentifizieren mit der verwalteten Dienstidentität (Managed Service Identity, MSI)</span><span class="sxs-lookup"><span data-stu-id="c2c42-125">Authenticate with Managed Service Identity(MSI)</span></span> 
<span data-ttu-id="c2c42-126">Über MSI kann eine Ressource in Azure ganz einfach das SDK oder die CLI nutzen, ohne spezielle Anmeldeinformationen erstellen zu müssen.</span><span class="sxs-lookup"><span data-stu-id="c2c42-126">MSI is a simple way for a resource in Azure to use SDK/CLI without the need to create specific credentials.</span></span>

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

## <a name="mgmt-auth-cli"></a><span data-ttu-id="c2c42-127">CLI-basierte Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="c2c42-127">CLI-based authentication</span></span>

<span data-ttu-id="c2c42-128">Das SDK kann mithilfe Ihres aktiven CLI-Abonnements einen Client erstellen.</span><span class="sxs-lookup"><span data-stu-id="c2c42-128">The SDK is able to create a client using your CLI active subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c2c42-129">Diese Vorgehensweise sollte als Schnellstart für Entwickler verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="c2c42-129">This should be used as quick start developer experience.</span></span> <span data-ttu-id="c2c42-130">Verwenden Sie zu Produktionszwecken [ADAL](#authenticate-with-token-credentials) oder Ihr eigenes System für Anmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="c2c42-130">For production purposes, use [ADAL](#authenticate-with-token-credentials) or your own credentials system.</span></span>
> <span data-ttu-id="c2c42-131">Alle Änderungen an der CLI-Konfiguration wirken sich auf die SDK-Ausführung aus.</span><span class="sxs-lookup"><span data-stu-id="c2c42-131">Any change to your CLI configuration will impact the SDK execution.</span></span>

<span data-ttu-id="c2c42-132">Verwenden Sie zum Definieren der aktiven Anmeldeinformationen [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c2c42-132">To define active credentials, use [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).</span></span>
<span data-ttu-id="c2c42-133">Bei der standardmäßigen Abonnement-ID handelt es sich um die ID, die Sie bereits besitzen. Alternativ können Sie die ID mit [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli) festlegen.</span><span class="sxs-lookup"><span data-stu-id="c2c42-133">Default subscription ID is either the only one you have, or you can define it using [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli)</span></span>

```python
from azure.common.client_factory import get_client_from_cli_profile
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_cli_profile(ComputeManagementClient)
```

## <a name="mgmt-auth-legacy"></a><span data-ttu-id="c2c42-134">Authentifizieren mit Tokenanmeldeinformationen (Legacy)</span><span class="sxs-lookup"><span data-stu-id="c2c42-134">Authenticate with token credentials (legacy)</span></span>

<span data-ttu-id="c2c42-135">In der vorherigen Version des SDK war ADAL noch nicht verfügbar, und es wurde eine `UserPassCredentials`-Klasse bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="c2c42-135">In previous version of the SDK, ADAL was not yet available and we provided a `UserPassCredentials` class.</span></span> <span data-ttu-id="c2c42-136">Diese wird als veraltet betrachtet und sollte nicht mehr verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="c2c42-136">This is considered deprecated and should not be used anymore.</span></span>

<span data-ttu-id="c2c42-137">In diesem Beispiel wird das Szenario mit Benutzername und Kennwort gezeigt.</span><span class="sxs-lookup"><span data-stu-id="c2c42-137">This sample shows user/password scenario.</span></span> <span data-ttu-id="c2c42-138">2FA wird dabei nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="c2c42-138">This does not support 2FA.</span></span>

```python
    from azure.common.credentials import UserPassCredentials

    credentials = UserPassCredentials(
        'user@domain.com',
        'my_smart_password',
    )
```
