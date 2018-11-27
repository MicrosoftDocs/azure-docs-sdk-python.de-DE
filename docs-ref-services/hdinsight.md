---
title: 'Azure HDInsight Python SDK: Vorschauversion'
description: Referenz zum Azure HDInsight Python SDK Das HDInsight Python SDK bietet Klassen und Methoden, mit denen Sie Ihre HDInsight-Cluster verwalten können.
ms.service: hdinsight
author: tylerfox
ms.author: tyfox
ms.date: 09/18/2018
ms.topic: reference
ms.devlang: python
ms.openlocfilehash: 42e1e36b5854fda93188564be3ed3064b9ba4435
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2018
ms.locfileid: "52277470"
---
# <a name="hdinsight-python-management-sdk-preview"></a><span data-ttu-id="3d685-104">HDInsight Python Management SDK: Vorschauversion</span><span class="sxs-lookup"><span data-stu-id="3d685-104">HDInsight Python Management SDK Preview</span></span>

## <a name="overview"></a><span data-ttu-id="3d685-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="3d685-105">Overview</span></span>

<span data-ttu-id="3d685-106">Das HDInsight Python SDK bietet Klassen und Methoden, mit denen Sie Ihre HDInsight-Cluster verwalten können.</span><span class="sxs-lookup"><span data-stu-id="3d685-106">The HDInsight Python SDK provides classes and methods that allow you to manage your HDInsight clusters.</span></span> <span data-ttu-id="3d685-107">Es enthält Vorgänge zum Erstellen, Löschen, Aktualisieren, Auflisten, Skalieren, Ausführen von Skriptaktionen, Überwachen, Abrufen der Eigenschaften von HDInsight-Clustern und mehr.</span><span class="sxs-lookup"><span data-stu-id="3d685-107">It includes operations to create, delete, update, list, scale, execute script actions, monitor, get properties of HDInsight clusters, and more.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d685-108">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="3d685-108">Prerequisites</span></span>

* <span data-ttu-id="3d685-109">Ein Azure-Konto.</span><span class="sxs-lookup"><span data-stu-id="3d685-109">An Azure account.</span></span> <span data-ttu-id="3d685-110">Falls Sie noch kein Konto haben, können Sie eine [kostenlose Testversion](https://azure.microsoft.com/free/) verwenden.</span><span class="sxs-lookup"><span data-stu-id="3d685-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* [<span data-ttu-id="3d685-111">Python</span><span class="sxs-lookup"><span data-stu-id="3d685-111">Python</span></span>](https://www.python.org/downloads/)
* [<span data-ttu-id="3d685-112">pip</span><span class="sxs-lookup"><span data-stu-id="3d685-112">pip</span></span>](https://pypi.org/project/pip/#description)

## <a name="sdk-installation"></a><span data-ttu-id="3d685-113">SDK-Installation</span><span class="sxs-lookup"><span data-stu-id="3d685-113">SDK Installation</span></span>

<span data-ttu-id="3d685-114">Sie finden das HDInsight Python SDK unter [Python Package Index](https://pypi.org/project/azure-mgmt-hdinsight/) und können es mit folgendem Befehl installieren:</span><span class="sxs-lookup"><span data-stu-id="3d685-114">The HDInsight Python SDK can be found in the [Python Package Index](https://pypi.org/project/azure-mgmt-hdinsight/) and can be installed by running:</span></span> 

`pip install azure-mgmt-hdinsight`

## <a name="authentication"></a><span data-ttu-id="3d685-115">Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="3d685-115">Authentication</span></span>

<span data-ttu-id="3d685-116">Das SDK muss zunächst für Ihr Azure-Abonnement authentifiziert werden.</span><span class="sxs-lookup"><span data-stu-id="3d685-116">The SDK first needs to be authenticated with your Azure subscription.</span></span>  <span data-ttu-id="3d685-117">Erstellen Sie anhand des Beispiels unten einen Dienstprinzipal, und verwenden Sie ihn für die Authentifizierung.</span><span class="sxs-lookup"><span data-stu-id="3d685-117">Follow the example below to create a service principal and use it to authenticate.</span></span> <span data-ttu-id="3d685-118">Nachdem dies erfolgt ist, verfügen Sie über eine Instanz von `HDInsightManagementClient` mit vielen Methoden (in den Abschnitten unten beschrieben), die zum Durchführen von Verwaltungsvorgängen verwendet werden können.</span><span class="sxs-lookup"><span data-stu-id="3d685-118">After this is done, you will have an instance of an `HDInsightManagementClient`, which contains many methods (outlined in below sections) that can be used to perform management operations.</span></span>

> [!NOTE]
> <span data-ttu-id="3d685-119">Neben dem Beispiel unten gibt es noch andere Möglichkeiten der Authentifizierung, die für Ihre Anforderungen unter Umständen besser geeignet sind.</span><span class="sxs-lookup"><span data-stu-id="3d685-119">There are other ways to authenticate besides the below example that could potentially be better suited for your needs.</span></span> <span data-ttu-id="3d685-120">Eine Beschreibung aller Methoden finden Sie unter [Authentifizieren bei den Azure-Verwaltungsbibliotheken für Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate?view=azure-python).</span><span class="sxs-lookup"><span data-stu-id="3d685-120">All methods are outlined here: [Authenticate with the Azure Management Libraries for Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate?view=azure-python)</span></span>

### <a name="authentication-example-using-a-service-principal"></a><span data-ttu-id="3d685-121">Beispiel für die Authentifizierung mit einem Dienstprinzipal</span><span class="sxs-lookup"><span data-stu-id="3d685-121">Authentication Example Using a Service Principal</span></span>

<span data-ttu-id="3d685-122">Melden Sie sich zuerst bei [Azure Cloud Shell](https://shell.azure.com/bash) an.</span><span class="sxs-lookup"><span data-stu-id="3d685-122">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="3d685-123">Vergewissern Sie sich, dass Sie derzeit das Abonnement verwenden, in dem der Dienstprinzipal erstellt werden soll.</span><span class="sxs-lookup"><span data-stu-id="3d685-123">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="3d685-124">Die Informationen zu Ihrem Abonnement werden im JSON-Format angezeigt.</span><span class="sxs-lookup"><span data-stu-id="3d685-124">Your subscription information is displayed as JSON.</span></span>

```json
{
  "environmentName": "AzureCloud",
  "id": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "isDefault": true,
  "name": "XXXXXXX",
  "state": "Enabled",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "user": {
    "cloudShellID": true,
    "name": "XXX@XXX.XXX",
    "type": "user"
  }
}
```

<span data-ttu-id="3d685-125">Wenn Sie nicht am richtigen Abonnement angemeldet sind, können Sie das richtige auswählen, indem Sie Folgendes ausführen:</span><span class="sxs-lookup"><span data-stu-id="3d685-125">If you're not logged into the correct subscription, select the correct one by running:</span></span> 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> <span data-ttu-id="3d685-126">Falls Sie den HDInsight-Ressourcenanbieter nicht bereits mit einer anderen Methode registriert haben (z.B. durch das Erstellen eines HDInsight-Clusters über das Azure-Portal), müssen Sie dies vor dem Authentifizieren durchführen.</span><span class="sxs-lookup"><span data-stu-id="3d685-126">If you have not already registered the HDInsight Resource Provider by another method (such as by creating an HDInsight Cluster through the Azure Portal), you need to do this once before you can authenticate.</span></span> <span data-ttu-id="3d685-127">Dies ist über [Azure Cloud Shell](https://shell.azure.com/bash) möglich, indem Sie den folgenden Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="3d685-127">This can be done from the [Azure Cloud Shell](https://shell.azure.com/bash) by running the following command:</span></span>
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

<span data-ttu-id="3d685-128">Wählen Sie als Nächstes einen Namen für Ihren Dienstprinzipal aus, und erstellen Sie ihn mit dem folgenden Befehl:</span><span class="sxs-lookup"><span data-stu-id="3d685-128">Next, choose a name for your service principal and create it with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

<span data-ttu-id="3d685-129">Die Dienstprinzipalinformationen werden im JSON-Format angezeigt.</span><span class="sxs-lookup"><span data-stu-id="3d685-129">The service principal information is displayed as JSON.</span></span>

```json
{
  "clientId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "clientSecret": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "subscriptionId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```
<span data-ttu-id="3d685-130">Kopieren Sie den unten angegebenen Python-Codeausschnitt, und geben Sie für `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` und `SUBSCRIPTION_ID` die Zeichenfolgen aus dem JSON-Code ein, der nach dem Ausführen des Befehls zum Erstellen des Dienstprinzipals zurückgegeben wurde.</span><span class="sxs-lookup"><span data-stu-id="3d685-130">Copy the below Python snippet and fill in `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET`, and `SUBSCRIPTION_ID` with the strings from the JSON that was returned after running the command to create the service principal.</span></span>

```python
from azure.mgmt.hdinsight import HDInsightManagementClient
from azure.common.credentials import ServicePrincipalCredentials
from azure.mgmt.hdinsight.models import *

# Tenant ID for your Azure Subscription
TENANT_ID = ''
# Your Service Principal App Client ID
CLIENT_ID = ''
# Your Service Principal Client Secret
CLIENT_SECRET = ''
# Your Azure Subscription ID
SUBSCRIPTION_ID = ''

credentials = ServicePrincipalCredentials(
    client_id = CLIENT_ID,
    secret = CLIENT_SECRET,
    tenant = TENANT_ID
)

client = HDInsightManagementClient(credentials, SUBSCRIPTION_ID)
```


## <a name="cluster-management"></a><span data-ttu-id="3d685-131">Clusterverwaltung</span><span class="sxs-lookup"><span data-stu-id="3d685-131">Cluster Management</span></span>

> [!NOTE]
> <span data-ttu-id="3d685-132">In diesem Abschnitt wird davon ausgegangen, dass Sie bereits eine `HDInsightManagementClient`-Instanz authentifiziert und in einer Variablen mit dem Namen `client` gespeichert haben.</span><span class="sxs-lookup"><span data-stu-id="3d685-132">This section assumes you have already authenticated and constructed an `HDInsightManagementClient` instance and store it in a variable called `client`.</span></span> <span data-ttu-id="3d685-133">Eine Anleitung zum Authentifizieren und Abrufen eines `HDInsightManagementClient`-Elements finden Sie oben im Abschnitt „Authentifizierung“.</span><span class="sxs-lookup"><span data-stu-id="3d685-133">Instructions for authenticating and obtaining an `HDInsightManagementClient` can be found in the Authentication section above.</span></span>

### <a name="create-a-cluster"></a><span data-ttu-id="3d685-134">Erstellen eines Clusters</span><span class="sxs-lookup"><span data-stu-id="3d685-134">Create a Cluster</span></span>

<span data-ttu-id="3d685-135">Sie können einen neuen Cluster erstellen, indem Sie `client.clusters.create()` aufrufen.</span><span class="sxs-lookup"><span data-stu-id="3d685-135">A new cluster can be created by calling `client.clusters.create()`.</span></span> 

#### <a name="example"></a><span data-ttu-id="3d685-136">Beispiel</span><span class="sxs-lookup"><span data-stu-id="3d685-136">Example</span></span>

<span data-ttu-id="3d685-137">In diesem Beispiel wird gezeigt, wie Sie einen Spark-Cluster mit zwei Hauptknoten und einem Workerknoten erstellen.</span><span class="sxs-lookup"><span data-stu-id="3d685-137">This example demonstrates how to create a Spark cluster with 2 head nodes and 1 worker node.</span></span>

> [!NOTE]
> <span data-ttu-id="3d685-138">Sie müssen zuerst wie unten beschrieben eine Ressourcengruppe und ein Speicherkonto erstellen.</span><span class="sxs-lookup"><span data-stu-id="3d685-138">You first need to create a Resource Group and Storage Account, as explained below.</span></span> <span data-ttu-id="3d685-139">Wenn Sie diese Komponenten bereits erstellt haben, können Sie diese Schritte überspringen.</span><span class="sxs-lookup"><span data-stu-id="3d685-139">If you have already created these, you can skip these steps.</span></span>

##### <a name="creating-a-resource-group"></a><span data-ttu-id="3d685-140">Erstellen einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="3d685-140">Creating a Resource Group</span></span>

<span data-ttu-id="3d685-141">Sie können eine Ressourcengruppe erstellen, indem Sie mit [Azure Cloud Shell](https://shell.azure.com/bash) Folgendes ausführen:</span><span class="sxs-lookup"><span data-stu-id="3d685-141">You can create a resource group using the [Azure Cloud Shell](https://shell.azure.com/bash) by running</span></span>
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a><span data-ttu-id="3d685-142">Erstellen eines Speicherkontos</span><span class="sxs-lookup"><span data-stu-id="3d685-142">Creating a Storage Account</span></span>

<span data-ttu-id="3d685-143">Sie können ein Speicherkonto erstellen, indem Sie mit [Azure Cloud Shell](https://shell.azure.com/bash) Folgendes ausführen:</span><span class="sxs-lookup"><span data-stu-id="3d685-143">You can create a storage account using the [Azure Cloud Shell](https://shell.azure.com/bash) by running:</span></span>
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
<span data-ttu-id="3d685-144">Führen Sie jetzt den folgenden Befehl aus, um den Schlüssel für Ihr Speicherkonto abzurufen (Sie benötigen ihn, um einen Cluster zu erstellen):</span><span class="sxs-lookup"><span data-stu-id="3d685-144">Now run the following command to get the key for your storage account (you will need this to create a cluster):</span></span>
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
<span data-ttu-id="3d685-145">Mit dem unten angegebenen Python-Codeausschnitt wird ein Spark-Cluster mit zwei Hauptknoten und einem Workerknoten erstellt.</span><span class="sxs-lookup"><span data-stu-id="3d685-145">The below Python snippet creates a Spark cluster with 2 head nodes and 1 worker node.</span></span> <span data-ttu-id="3d685-146">Geben Sie gemäß den Anweisungen in den Kommentaren Werte in die leeren Variablen ein, und ändern Sie ggf. auch andere Parameter, um diese an Ihre Anforderungen anzupassen.</span><span class="sxs-lookup"><span data-stu-id="3d685-146">Fill in the blank variables as explained in the comments and feel free to change other parameters to suit your specific needs.</span></span>

```python
# The name for the cluster you are creating
cluster_name = ""
# The name of your existing Resource Group
resource_group_name = ""
# Choose a username
username = ""
# Choose a password
password = ""
# Replace <> with the name of your storage account
storage_account = "<>.blob.core.windows.net"
# Storage account key you obtained above
storage_account_key = ""
# Choose a region
location = ""
container = "default"

params = ClusterCreateProperties(
    cluster_version="3.6",
    os_type=OSType.linux,
    tier=Tier.standard,
    cluster_definition=ClusterDefinition(
        kind="spark",
        configurations={
            "gateway": {
                "restAuthCredential.enabled_credential": "True",
                "restAuthCredential.username": username,
                "restAuthCredential.password": password
            }
        }
    ),
    compute_profile=ComputeProfile(
        roles=[
            Role(
                name="headnode",
                target_instance_count=2,
                hardware_profile=HardwareProfile(vm_size="Large"),
                os_profile=OsProfile(
                    linux_operating_system_profile=LinuxOperatingSystemProfile(
                        username=username,
                        password=password
                    )
                )
            ),
            Role(
                name="workernode",
                target_instance_count=1,
                hardware_profile=HardwareProfile(vm_size="Large"),
                os_profile=OsProfile(
                    linux_operating_system_profile=LinuxOperatingSystemProfile(
                        username=username,
                        password=password
                    )
                )
            )
        ]
    ),
    storage_profile=StorageProfile(
        storageaccounts=[StorageAccount(
            name=storage_account,
            key=storage_account_key,
            container=container,
            is_default=True
        )]
    )
)

client.clusters.create(
    cluster_name=cluster_name,
    resource_group_name=resource_group_name,
    parameters=ClusterCreateParametersExtended(
        location=location,
        tags={},
        properties=params
    ))
```

### <a name="get-cluster-details"></a><span data-ttu-id="3d685-147">Abrufen von Clusterdetails</span><span class="sxs-lookup"><span data-stu-id="3d685-147">Get Cluster Details</span></span>

<span data-ttu-id="3d685-148">Rufen Sie die Eigenschaften für einen Cluster wie folgt ab:</span><span class="sxs-lookup"><span data-stu-id="3d685-148">To get properties for a given cluster:</span></span>

```python
client.clusters.get("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="3d685-149">Beispiel</span><span class="sxs-lookup"><span data-stu-id="3d685-149">Example</span></span>

<span data-ttu-id="3d685-150">Sie können `get` verwenden, um zu bestätigen, dass die Erstellung des Clusters erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="3d685-150">You can use `get` to confirm that you have successfully created your cluster.</span></span>

```python
my_cluster = client.clusters.get("<Resource Group Name>", "<Cluster Name>")
print(my_cluster)
```

<span data-ttu-id="3d685-151">Die Ausgabe sollte wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="3d685-151">The output should look like:</span></span>

```
{'additional_properties': {}, 'id': '/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>', 'name': '<Cluster Name>', 'type': 'Microsoft.HDInsight/clusters', 'location': '<Location>', 'tags': {}, 'etag': 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX', 'properties': <azure.mgmt.hdinsight.models.cluster_get_properties_py3.ClusterGetProperties object at 0x0000013766D68048>}
```

### <a name="list-clusters"></a><span data-ttu-id="3d685-152">Auflisten von Clustern</span><span class="sxs-lookup"><span data-stu-id="3d685-152">List Clusters</span></span>

#### <a name="list-clusters-under-the-subscription"></a><span data-ttu-id="3d685-153">Auflisten von Clustern unter dem Abonnement</span><span class="sxs-lookup"><span data-stu-id="3d685-153">List Clusters Under The Subscription</span></span>

```python
client.clusters.list()
```
#### <a name="list-clusters-by-resource-group"></a><span data-ttu-id="3d685-154">Auflisten von Clustern nach Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="3d685-154">List Clusters By Resource Group</span></span>

```python
client.clusters.list_by_resource_group("<Resource Group Name>")
```
> [!NOTE]
> <span data-ttu-id="3d685-155">Sowohl für `list()` als auch für `list_by_resource_group()` wird ein `ClusterPaged`-Objekt zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="3d685-155">Both `list()` and `list_by_resource_group()` return an `ClusterPaged` object.</span></span> <span data-ttu-id="3d685-156">Wenn Sie `advance_page()` aufrufen, wird die Liste der Cluster auf dieser Seite zurückgegeben und das `ClusterPaged`-Objekt auf der nächsten Seite fortgesetzt.</span><span class="sxs-lookup"><span data-stu-id="3d685-156">Calling `advance_page()` returns the a list of clusters on that page and advances the `ClusterPaged` object to the next page.</span></span> <span data-ttu-id="3d685-157">Dies kann wiederholt werden, bis eine Ausnahme vom Typ `StopIteration` zurückgegeben wird, die darauf hinweist, dass keine Seiten mehr vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="3d685-157">This can be repeated until a `StopIteration` exception is raised, indicating that there are no more pages.</span></span>

#### <a name="example"></a><span data-ttu-id="3d685-158">Beispiel</span><span class="sxs-lookup"><span data-stu-id="3d685-158">Example</span></span>

<span data-ttu-id="3d685-159">Im folgenden Beispiel werden die Eigenschaften aller Cluster für das aktuelle Abonnement ausgegeben:</span><span class="sxs-lookup"><span data-stu-id="3d685-159">The following example prints the properties of all clusters for the current subscription:</span></span>

```python
clusters_paged = client.clusters.list()
while True:
  try:
    for cluster in clusters_paged.advance_page():
      print(cluster)
  except StopIteration: 
    break
```

### <a name="delete-a-cluster"></a><span data-ttu-id="3d685-160">Löschen eines Clusters</span><span class="sxs-lookup"><span data-stu-id="3d685-160">Delete a Cluster</span></span>

<span data-ttu-id="3d685-161">Löschen Sie einen Cluster wie folgt:</span><span class="sxs-lookup"><span data-stu-id="3d685-161">To delete a cluster:</span></span>

```python
client.clusters.delete("<Resource Group Name>", "<Cluster Name>")
```

### <a name="update-cluster-tags"></a><span data-ttu-id="3d685-162">Aktualisieren von Clustermarkierungen</span><span class="sxs-lookup"><span data-stu-id="3d685-162">Update Cluster Tags</span></span>

<span data-ttu-id="3d685-163">Sie können die Markierungen eines Clusters wie folgt aktualisieren:</span><span class="sxs-lookup"><span data-stu-id="3d685-163">You can update the tags of a given cluster like so:</span></span>

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={<Dictionary of Tags>})
```

#### <a name="example"></a><span data-ttu-id="3d685-164">Beispiel</span><span class="sxs-lookup"><span data-stu-id="3d685-164">Example</span></span>

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={"tag1Name" : "tag1Value", "tag2Name" : "tag2Value"})
```

### <a name="scale-cluster"></a><span data-ttu-id="3d685-165">Skalieren von Clustern</span><span class="sxs-lookup"><span data-stu-id="3d685-165">Scale Cluster</span></span>

<span data-ttu-id="3d685-166">Sie können die Anzahl von Workerknoten für einen Cluster skalieren, indem Sie wie folgt eine neue Größe angeben:</span><span class="sxs-lookup"><span data-stu-id="3d685-166">You can scale a given cluster's number of worker nodes by specifying a new size like so:</span></span>

```python
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", target_instance_count=<Num of Worker Nodes>)
```

## <a name="cluster-monitoring"></a><span data-ttu-id="3d685-167">Clusterüberwachung</span><span class="sxs-lookup"><span data-stu-id="3d685-167">Cluster Monitoring</span></span>

<span data-ttu-id="3d685-168">Das HDInsight Management SDK kann auch verwendet werden, um die Überwachung Ihrer Cluster per Operations Management Suite (OMS) zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="3d685-168">The HDInsight Management SDK can also be used to manage monitoring on your clusters via the Operations Management Suite (OMS).</span></span>

### <a name="enable-oms-monitoring"></a><span data-ttu-id="3d685-169">Aktivieren der OMS-Überwachung</span><span class="sxs-lookup"><span data-stu-id="3d685-169">Enable OMS Monitoring</span></span>

> [!NOTE]
> <span data-ttu-id="3d685-170">Sie müssen über einen vorhandenen Log Analytics-Arbeitsbereich verfügen, um die OMS-Überwachung zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="3d685-170">To enable OMS Monitoring, you must have an existing Log Analytics workspace.</span></span> <span data-ttu-id="3d685-171">Falls Sie diesen noch nicht erstellt haben, helfen Ihnen die Informationen im folgenden Artikel weiter: [Erstellen eines Log Analytics-Arbeitsbereichs im Azure-Portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span><span class="sxs-lookup"><span data-stu-id="3d685-171">If you have not already created one, you can learn how to do that here: [Create a Log Analytics workspace in the Azure portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span></span>

<span data-ttu-id="3d685-172">Aktivieren Sie die OMS-Überwachung in Ihrem Cluster wie folgt:</span><span class="sxs-lookup"><span data-stu-id="3d685-172">To enable OMS Monitoring on your cluster:</span></span>

```python
client.extension.enable_monitoring("<Resource Group Name>", "<Cluster Name>", workspace_id="<Workspace Id>")
```

### <a name="view-status-of-oms-monitoring"></a><span data-ttu-id="3d685-173">Anzeigen des Status der OMS-Überwachung</span><span class="sxs-lookup"><span data-stu-id="3d685-173">View Status Of OMS Monitoring</span></span>

<span data-ttu-id="3d685-174">Rufen Sie den Status von OMS in Ihrem Cluster wie folgt ab:</span><span class="sxs-lookup"><span data-stu-id="3d685-174">To get the status of OMS on your cluster:</span></span>

```python
client.extension.get_monitoring_status("<Resource Group Name", "Cluster Name")
```

### <a name="disable-oms-monitoring"></a><span data-ttu-id="3d685-175">Deaktivieren der OMS-Überwachung</span><span class="sxs-lookup"><span data-stu-id="3d685-175">Disable OMS Monitoring</span></span>

<span data-ttu-id="3d685-176">Deaktivieren Sie OMS in Ihrem Cluster wie folgt:</span><span class="sxs-lookup"><span data-stu-id="3d685-176">To disable OMS on your cluster:</span></span>

```python
client.extension.disable_monitoring("<Resource Group Name>", "<Cluster Name>")
```

## <a name="script-actions"></a><span data-ttu-id="3d685-177">Skriptaktionen</span><span class="sxs-lookup"><span data-stu-id="3d685-177">Script Actions</span></span>

<span data-ttu-id="3d685-178">HDInsight verfügt über eine Konfigurationsmethode mit der Bezeichnung „Skriptaktionen“, mit der benutzerdefinierte Skripts zum Anpassen des Clusters aufgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="3d685-178">HDInsight provides a configuration method called script actions that invokes custom scripts to customize the cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="3d685-179">Weitere Informationen zur Verwendung von Skriptaktionen finden Sie unter [Anpassen Linux-basierter HDInsight-Cluster mithilfe von Skriptaktionen](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="3d685-179">More information on how to use script actions can be found here: [Customize Linux-based HDInsight clusters using script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span></span>

### <a name="execute-script-actions"></a><span data-ttu-id="3d685-180">Ausführen von Skriptaktionen</span><span class="sxs-lookup"><span data-stu-id="3d685-180">Execute Script Actions</span></span>
<span data-ttu-id="3d685-181">So führen Sie Skriptaktionen für einen bestimmten Cluster aus:</span><span class="sxs-lookup"><span data-stu-id="3d685-181">To execute script actions on a given cluster:</span></span>

```python
script_action1 = RuntimeScriptAction(name="<Script Name>", uri="<URL To Script>", roles=[<List of Roles>]) #valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.clusters.execute_script_actions("<Resource Group Name>", "<Cluster Name>", <persist_on_success (bool)>, script_actions=[script_action1]) #add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a><span data-ttu-id="3d685-182">Löschen der Skriptaktion</span><span class="sxs-lookup"><span data-stu-id="3d685-182">Delete Script Action</span></span>

<span data-ttu-id="3d685-183">Löschen Sie eine angegebene permanente Skriptaktion für einen Cluster wie folgt:</span><span class="sxs-lookup"><span data-stu-id="3d685-183">To delete a specified persisted script action on a given cluster:</span></span>

```python
client.script_actions.delete("<Resource Group Name>", "<Cluster Name", "<Script Name>")
```

### <a name="list-persisted-script-actions"></a><span data-ttu-id="3d685-184">Auflisten von permanenten Skriptaktionen</span><span class="sxs-lookup"><span data-stu-id="3d685-184">List Persisted Script Actions</span></span>

> [!NOTE]
> <span data-ttu-id="3d685-185">`list()` und `list_persisted_scripts()` geben ein `RuntimeScriptActionDetailPaged`-Objekt zurück.</span><span class="sxs-lookup"><span data-stu-id="3d685-185">`list()` and `list_persisted_scripts()` return a `RuntimeScriptActionDetailPaged` object.</span></span> <span data-ttu-id="3d685-186">Wenn Sie `advance_page()` aufrufen, wird die Liste für `RuntimeScriptActionDetail` auf dieser Seite zurückgegeben und das `RuntimeScriptActionDetailPaged`-Objekt auf der nächsten Seite fortgesetzt.</span><span class="sxs-lookup"><span data-stu-id="3d685-186">Calling `advance_page()` returns the a list of `RuntimeScriptActionDetail` on that page and advances the `RuntimeScriptActionDetailPaged` object to the next page.</span></span> <span data-ttu-id="3d685-187">Dies kann wiederholt werden, bis eine Ausnahme vom Typ `StopIteration` zurückgegeben wird, die darauf hinweist, dass keine Seiten mehr vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="3d685-187">This can be repeated until a `StopIteration` exception is raised, indicating that there are no more pages.</span></span> <span data-ttu-id="3d685-188">Betrachten Sie das folgende Beispiel.</span><span class="sxs-lookup"><span data-stu-id="3d685-188">See the example below.</span></span>

<span data-ttu-id="3d685-189">Listen Sie alle permanenten Skriptaktionen für den angegebenen Cluster wie folgt auf:</span><span class="sxs-lookup"><span data-stu-id="3d685-189">To list all persisted script actions for the specified cluster:</span></span>
```python
client.script_actions.list_persisted_scripts("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="3d685-190">Beispiel</span><span class="sxs-lookup"><span data-stu-id="3d685-190">Example</span></span>

```python
scripts_paged = client.script_actions.list_persisted_scripts(resource_group_name, cluster_name)
while True:
  try:
    for script in scripts_paged.advance_page():
      print(script)
  except StopIteration:
    break
```

### <a name="list-all-scripts-execution-history"></a><span data-ttu-id="3d685-191">Auflisten des Ausführungsverlaufs aller Skripts</span><span class="sxs-lookup"><span data-stu-id="3d685-191">List All Scripts' Execution History</span></span>

<span data-ttu-id="3d685-192">Listen Sie den Ausführungsverlauf aller Skripts für den angegebenen Cluster wie folgt auf:</span><span class="sxs-lookup"><span data-stu-id="3d685-192">To list all scripts' execution history for the specified cluster:</span></span>

```python
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="3d685-193">Beispiel</span><span class="sxs-lookup"><span data-stu-id="3d685-193">Example</span></span>

<span data-ttu-id="3d685-194">In diesem Beispiel werden alle Details zu allen erfolgten Skriptausführungen ausgegeben.</span><span class="sxs-lookup"><span data-stu-id="3d685-194">This example prints all the details for all past script executions.</span></span>

```python
script_executions_paged = client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
while True:
  try:
    for script in script_executions_paged.advance_page():            
      print(script)
    except StopIteration:       
      break
```
