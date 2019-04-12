---
title: Azure HDInsight SDK für Python
description: Referenz zum Azure HDInsight SDK für Python Das HDInsight SDK für Python bietet Klassen und Methoden, mit denen Sie Ihre HDInsight-Cluster verwalten können.
ms.service: hdinsight
author: tylerfox
ms.author: tyfox
ms.date: 04/10/2019
ms.topic: reference
ms.devlang: python
ms.openlocfilehash: f16e5da474e1c506c800b860b451754a6bdc75bc
ms.sourcegitcommit: 3c6087cbc1fee5a2c88c40fe96d351375c6c6377
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/11/2019
ms.locfileid: "59504547"
---
# <a name="hdinsight-sdk-for-python"></a>HDInsight SDK für Python

## <a name="overview"></a>Übersicht

Das HDInsight SDK für Python bietet Klassen und Methoden, mit denen Sie Ihre HDInsight-Cluster verwalten können. Es enthält Vorgänge zum Erstellen, Löschen, Aktualisieren, Auflisten, Ändern der Größe, Ausführen von Skriptaktionen, Überwachen, Abrufen der Eigenschaften von HDInsight-Clustern und mehr.

## <a name="prerequisites"></a>Voraussetzungen

* Ein Azure-Konto. Falls Sie noch kein Konto haben, können Sie eine [kostenlose Testversion](https://azure.microsoft.com/free/) verwenden.
* [Python](https://www.python.org/downloads/)
* [pip](https://pypi.org/project/pip/#description)

## <a name="sdk-installation"></a>SDK-Installation

Sie finden das HDInsight SDK für Python unter [Python Package Index](https://pypi.org/project/azure-mgmt-hdinsight/) und können es mit folgendem Befehl installieren: 

`pip install azure-mgmt-hdinsight`

## <a name="authentication"></a>Authentication

Das SDK muss zunächst für Ihr Azure-Abonnement authentifiziert werden.  Erstellen Sie anhand des Beispiels unten einen Dienstprinzipal, und verwenden Sie ihn für die Authentifizierung. Nachdem dies erfolgt ist, verfügen Sie über eine Instanz von `HDInsightManagementClient` mit vielen Methoden (in den Abschnitten unten beschrieben), die zum Durchführen von Verwaltungsvorgängen verwendet werden können.

> [!NOTE]
> Neben dem Beispiel unten gibt es noch andere Möglichkeiten der Authentifizierung, die für Ihre Anforderungen unter Umständen besser geeignet sind. Hier werden alle Methoden beschrieben: [Authentifizieren bei den Azure-Verwaltungsbibliotheken für Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate?view=azure-python)

### <a name="authentication-example-using-a-service-principal"></a>Beispiel für die Authentifizierung mit einem Dienstprinzipal

Melden Sie sich zuerst bei [Azure Cloud Shell](https://shell.azure.com/bash) an. Vergewissern Sie sich, dass Sie derzeit das Abonnement verwenden, in dem der Dienstprinzipal erstellt werden soll. 

```azurecli-interactive
az account show
```

Die Informationen zu Ihrem Abonnement werden im JSON-Format angezeigt.

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

Wenn Sie nicht am richtigen Abonnement angemeldet sind, können Sie das richtige auswählen, indem Sie Folgendes ausführen: 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> Falls Sie den HDInsight-Ressourcenanbieter nicht bereits mit einer anderen Methode registriert haben (z.B. durch das Erstellen eines HDInsight-Clusters über das Azure-Portal), müssen Sie dies vor dem Authentifizieren durchführen. Dies ist über [Azure Cloud Shell](https://shell.azure.com/bash) möglich, indem Sie den folgenden Befehl ausführen:
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

Wählen Sie als Nächstes einen Namen für Ihren Dienstprinzipal aus, und erstellen Sie ihn mit dem folgenden Befehl:

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

Die Dienstprinzipalinformationen werden im JSON-Format angezeigt.

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
Kopieren Sie den unten angegebenen Python-Codeausschnitt, und geben Sie für `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` und `SUBSCRIPTION_ID` die Zeichenfolgen aus dem JSON-Code ein, der nach dem Ausführen des Befehls zum Erstellen des Dienstprinzipals zurückgegeben wurde.

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


## <a name="cluster-management"></a>Clusterverwaltung

> [!NOTE]
> In diesem Abschnitt wird davon ausgegangen, dass Sie bereits eine `HDInsightManagementClient`-Instanz authentifiziert und in einer Variablen mit dem Namen `client` gespeichert haben. Eine Anleitung zum Authentifizieren und Abrufen eines `HDInsightManagementClient`-Elements finden Sie oben im Abschnitt „Authentifizierung“.

### <a name="create-a-cluster"></a>Erstellen eines Clusters

Sie können einen neuen Cluster erstellen, indem Sie `client.clusters.create()` aufrufen. 

#### <a name="example"></a>Beispiel

In diesem Beispiel wird gezeigt, wie Sie einen Spark-Cluster mit zwei Hauptknoten und einem Workerknoten erstellen.

> [!NOTE]
> Sie müssen zuerst wie unten beschrieben eine Ressourcengruppe und ein Speicherkonto erstellen. Wenn Sie diese Komponenten bereits erstellt haben, können Sie diese Schritte überspringen.

##### <a name="creating-a-resource-group"></a>Erstellen einer Ressourcengruppe

Sie können eine Ressourcengruppe erstellen, indem Sie mit [Azure Cloud Shell](https://shell.azure.com/bash) Folgendes ausführen:
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a>Erstellen eines Speicherkontos

Sie können ein Speicherkonto erstellen, indem Sie mit [Azure Cloud Shell](https://shell.azure.com/bash) Folgendes ausführen:
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
Führen Sie jetzt den folgenden Befehl aus, um den Schlüssel für Ihr Speicherkonto abzurufen (Sie benötigen ihn, um einen Cluster zu erstellen):
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
Mit dem unten angegebenen Python-Codeausschnitt wird ein Spark-Cluster mit zwei Hauptknoten und einem Workerknoten erstellt. Geben Sie gemäß den Anweisungen in den Kommentaren Werte in die leeren Variablen ein, und ändern Sie ggf. auch andere Parameter, um diese an Ihre Anforderungen anzupassen.

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

#### <a name="samples"></a>Beispiele

Darüber hinaus stehen Codebeispiele zum Erstellen verschiedener allgemeiner HDInsight-Clustertypen zur Verfügung: [HDInsight-Python-Beispiele](https://github.com/Azure-Samples/hdinsight-python-sdk-samples).

### <a name="get-cluster-details"></a>Abrufen von Clusterdetails

Rufen Sie die Eigenschaften für einen Cluster wie folgt ab:

```python
client.clusters.get("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a>Beispiel

Sie können `get` verwenden, um zu bestätigen, dass die Erstellung des Clusters erfolgreich war.

```python
my_cluster = client.clusters.get("<Resource Group Name>", "<Cluster Name>")
print(my_cluster)
```

Die Ausgabe sollte wie folgt aussehen:

```
{'additional_properties': {}, 'id': '/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>', 'name': '<Cluster Name>', 'type': 'Microsoft.HDInsight/clusters', 'location': '<Location>', 'tags': {}, 'etag': 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX', 'properties': <azure.mgmt.hdinsight.models.cluster_get_properties_py3.ClusterGetProperties object at 0x0000013766D68048>}
```

### <a name="list-clusters"></a>Auflisten von Clustern

#### <a name="list-clusters-under-the-subscription"></a>Auflisten von Clustern unter dem Abonnement

```python
client.clusters.list()
```
#### <a name="list-clusters-by-resource-group"></a>Auflisten von Clustern nach Ressourcengruppe

```python
client.clusters.list_by_resource_group("<Resource Group Name>")
```
> [!NOTE]
> Sowohl `list()` als auch `list_by_resource_group()` geben ein `ClusterPaged`-Objekt zurück. Wenn Sie `advance_page()` aufrufen, wird eine Liste der Cluster auf dieser Seite zurückgegeben und das `ClusterPaged`-Objekt auf der nächsten Seite fortgesetzt. Dies kann wiederholt werden, bis eine Ausnahme vom Typ `StopIteration` zurückgegeben wird, die darauf hinweist, dass keine Seiten mehr vorhanden sind.

#### <a name="example"></a>Beispiel

Im folgenden Beispiel werden die Eigenschaften aller Cluster für das aktuelle Abonnement ausgegeben:

```python
clusters_paged = client.clusters.list()
while True:
  try:
    for cluster in clusters_paged.advance_page():
      print(cluster)
  except StopIteration: 
    break
```

### <a name="delete-a-cluster"></a>Löschen eines Clusters

Löschen Sie einen Cluster wie folgt:

```python
client.clusters.delete("<Resource Group Name>", "<Cluster Name>")
```

### <a name="update-cluster-tags"></a>Aktualisieren von Clustermarkierungen

Sie können die Markierungen eines Clusters wie folgt aktualisieren:

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={<Dictionary of Tags>})
```

#### <a name="example"></a>Beispiel

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={"tag1Name" : "tag1Value", "tag2Name" : "tag2Value"})
```

### <a name="resize-cluster"></a>Ändern der Clustergröße

Sie können die Anzahl von Workerknoten für einen Cluster ändern, indem Sie wie folgt eine neue Größe angeben:

```python
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", target_instance_count=<Num of Worker Nodes>)
```

## <a name="cluster-monitoring"></a>Clusterüberwachung

Das HDInsight Management SDK kann auch verwendet werden, um die Überwachung Ihrer Cluster per Operations Management Suite (OMS) zu verwalten.

### <a name="enable-oms-monitoring"></a>Aktivieren der OMS-Überwachung

> [!NOTE]
> Sie müssen über einen vorhandenen Log Analytics-Arbeitsbereich verfügen, um die OMS-Überwachung zu ermöglichen. Wenn Sie noch keinen erstellt haben, erfahren Sie an dieser Stelle, wie Sie dazu vorgehen: [Erstellen eines Log Analytics-Arbeitsbereichs im Azure-Portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace)

Aktivieren Sie die OMS-Überwachung in Ihrem Cluster wie folgt:

```python
client.extension.enable_monitoring("<Resource Group Name>", "<Cluster Name>", workspace_id="<Workspace Id>")
```

### <a name="view-status-of-oms-monitoring"></a>Anzeigen des Status der OMS-Überwachung

Rufen Sie den Status von OMS in Ihrem Cluster wie folgt ab:

```python
client.extension.get_monitoring_status("<Resource Group Name", "Cluster Name")
```

### <a name="disable-oms-monitoring"></a>Deaktivieren der OMS-Überwachung

Deaktivieren Sie OMS in Ihrem Cluster wie folgt:

```python
client.extension.disable_monitoring("<Resource Group Name>", "<Cluster Name>")
```

## <a name="script-actions"></a>Skriptaktionen

HDInsight verfügt über eine Konfigurationsmethode mit der Bezeichnung „Skriptaktionen“, mit der benutzerdefinierte Skripts zum Anpassen des Clusters aufgerufen werden.
> [!NOTE]
> Weitere Informationen zum Verwenden von Skriptaktionen finden Sie hier: [Anpassen Linux-basierter HDInsight-Cluster mithilfe von Skriptaktionen](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)

### <a name="execute-script-actions"></a>Ausführen von Skriptaktionen
So führen Sie Skriptaktionen für einen bestimmten Cluster aus:

```python
script_action1 = RuntimeScriptAction(name="<Script Name>", uri="<URL To Script>", roles=[<List of Roles>]) #valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.clusters.execute_script_actions("<Resource Group Name>", "<Cluster Name>", <persist_on_success (bool)>, script_actions=[script_action1]) #add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a>Löschen der Skriptaktion

Löschen Sie eine angegebene permanente Skriptaktion für einen Cluster wie folgt:

```python
client.script_actions.delete("<Resource Group Name>", "<Cluster Name", "<Script Name>")
```

### <a name="list-persisted-script-actions"></a>Auflisten von permanenten Skriptaktionen

> [!NOTE]
> `list()` und `list_persisted_scripts()` geben ein `RuntimeScriptActionDetailPaged`-Objekt zurück. Wenn Sie `advance_page()` aufrufen, wird die Liste für `RuntimeScriptActionDetail` auf dieser Seite zurückgegeben und das `RuntimeScriptActionDetailPaged`-Objekt auf der nächsten Seite fortgesetzt. Dies kann wiederholt werden, bis eine Ausnahme vom Typ `StopIteration` zurückgegeben wird, die darauf hinweist, dass keine Seiten mehr vorhanden sind. Betrachten Sie das folgende Beispiel.

Listen Sie alle permanenten Skriptaktionen für den angegebenen Cluster wie folgt auf:
```python
client.script_actions.list_persisted_scripts("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a>Beispiel

```python
scripts_paged = client.script_actions.list_persisted_scripts(resource_group_name, cluster_name)
while True:
  try:
    for script in scripts_paged.advance_page():
      print(script)
  except StopIteration:
    break
```

### <a name="list-all-scripts-execution-history"></a>Auflisten des Ausführungsverlaufs aller Skripts

Listen Sie den Ausführungsverlauf aller Skripts für den angegebenen Cluster wie folgt auf:

```python
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a>Beispiel

In diesem Beispiel werden alle Details zu allen erfolgten Skriptausführungen ausgegeben.

```python
script_executions_paged = client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
while True:
  try:
    for script in script_executions_paged.advance_page():            
      print(script)
    except StopIteration:       
      break
```
