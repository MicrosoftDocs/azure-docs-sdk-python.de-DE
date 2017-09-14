---
title: "Erste Schritte mit den Azure-Bibliotheken für Python"
description: "Erste Schritte mit Azure-Bibliotheken für Python"
keywords: Azure, Python, SDK, API
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/05/2017
ms.topic: get-started
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.assetid: 
ms.openlocfilehash: 848ca9dc40000e68e5e3cea3af8b8a0d22747881
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-the-azure-libraries-for-python"></a>Erste Schritte mit den Azure-Bibliotheken für Python

Dieses Handbuch veranschaulicht die Verwendung verschiedener Azure-Bibliotheken für Python.  Sie richten die Authentifizierung ein und erstellen und verwenden ein Azure Storage-Konto sowie eine Azure SQL-Datenbank. Außerdem stellen Sie einige virtuelle Computer und eine Azure App Service-Web-App über GitHub bereit.

## <a name="prerequisites"></a>Voraussetzungen

- Ein Azure-Konto. Falls Sie noch kein Konto haben, können Sie eine [kostenlose Testversion](https://azure.microsoft.com/free/) verwenden.
- [Python](https://www.python.org/downloads/)
- [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) oder [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).

[!INCLUDE [azure-cloud-shell](../docs-ref-conceptual/includes/cloud-shell-try-it.md)]

## <a name="set-up-authentication"></a>Einrichten der Authentifizierung
> [!IMPORTANT]
> Diese Vorgehensweise sollte als Schnellstart für Entwickler verwendet werden. Verwenden Sie zu Produktionszwecken [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) oder Ihr eigenes System für Anmeldeinformationen.
> Alle Änderungen an der CLI-Konfiguration wirken sich auf die SDK-Ausführung aus.

Das SDK kann mithilfe Ihres aktiven CLI-Abonnements einen Client erstellen.

Verwenden Sie zum Definieren der aktiven Anmeldeinformationen [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).
Bei der standardmäßigen Abonnement-ID handelt es sich um die ID, die Sie bereits besitzen. Alternativ können Sie die ID mit [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli) festlegen.

```python
from azure.common.client_factory import get_client_from_cli_profile
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_cli_profile(ComputeManagementClient)
```
## <a name="create-a-virtual-environment"></a>Erstellen einer virtuellen Umgebung

> [!IMPORTANT]
> Die Erstellung einer virtuellen Umgebung ist optional, wird jedoch dringend empfohlen.

Erstellen einer virtuellen Umgebung in Bash (Linux oder [Bash für Windows](https://msdn.microsoft.com/commandline/wsl/about)):
```bash
pip install virtualenv
virtualenv mytestenv
cd mytestenv
source ./bin/activate
```

Erstellen einer virtuellen Umgebung in PowerShell:
```powershell
pip install virtualenv
virtualenv mytestenv
cd mytestenv
.\Scripts\activate
```

> [!IMPORTANT]
> Hinweis: Wenn Sie [VSCode](https://code.visualstudio.com/) und die [Python-Erweiterung](https://marketplace.visualstudio.com/items?itemName=donjayamanne.python) verwenden, können Sie die Nutzung mit `code .` starten und die Umgebung konfigurieren.

## <a name="create-a-linux-virtual-machine"></a>Erstellen einer virtuellen Linux-Maschine
Dieser Code erstellt einen neuen virtuellen Linux-Computer namens `testLinuxVM` in der Ressourcengruppe `sampleVmResourceGroup` in der Azure-Region „USA, Osten“.

Authentifizieren:
```azcli
az login
```
Erstellen Sie eine Ressourcengruppe:
```azurecli-interactive
az group create -l eastus --n sampleVmResourceGroup
```

Erstellen eines virtuellen Netzwerks und des Subnetzes:
```azurecli-interactive
az network vnet create -g sampleVmResourceGroup -n azure-sample-vnet --address-prefix 10.0.0.0/16 --subnet-name azure-sample-subnet --subnet-prefix 10.0.0.0/24
```

Erstellen einer öffentlichen IP-Adresse:
```azurecli-interactive
az network public-ip create -g sampleVmResourceGroup -n azure-sample-ip --allocation-method Dynamic --version IPv6
```
Erstellen eines Netzwerkschnittstellenclients:
```azurecli-interactive
az network nic create -g sampleVmResourceGroup --vnet-name azure-sample-vnet --subnet azure-sample-subnet -n azure-sample-nic --public-ip-address azure-sample-ip
```

```python
from azure.mgmt.network import NetworkManagementClient
from azure.mgmt.compute import ComputeManagementClient
from azure.common.client_factory import get_client_from_cli_profile

# Azure Datacenter
LOCATION = 'eastus'

# Resource Group
GROUP_NAME = 'sampleVmResourceGroup'

# Network
VNET_NAME = 'azure-sample-vnet'
SUBNET_NAME = 'azure-sample-subnet'

# VM
NIC_NAME = 'azure-sample-nic'
VM_NAME = 'testLinuxVM'

USERNAME = 'userlogin'
PASSWORD = 'Pa$$w0rd91'

IP_ADDRESS_NAME='azure-sample-ip'

VM_REFERENCE = {
    'linux': {
        'publisher': 'Canonical',
        'offer': 'UbuntuServer',
        'sku': '16.04.0-LTS',
        'version': 'latest'
    },
    'windows': {
        'publisher': 'MicrosoftWindowsServerEssentials',
        'offer': 'WindowsServerEssentials',
        'sku': 'WindowsServerEssentials',
        'version': 'latest'
    }
}


def run_example():

    compute_client = get_client_from_cli_profile(ComputeManagementClient)
    network_client = get_client_from_cli_profile(NetworkManagementClient)

    # get nic id
    nic = network_client.network_interfaces.get(GROUP_NAME, NIC_NAME)

    # Create Linux VM
    print('\nCreating Linux Virtual Machine')
    vm_parameters = create_vm_parameters(nic.id, VM_REFERENCE['linux'])
    print(vm_parameters)
    async_vm_creation = compute_client.virtual_machines.create_or_update(
        GROUP_NAME, VM_NAME, vm_parameters)
    async_vm_creation.wait()


def create_vm_parameters(nic_id, vm_reference):
    """Create the VM parameters structure.
    """
    return {
        'location': LOCATION,
        'os_profile': {
            'computer_name': VM_NAME,
            'admin_username': USERNAME,
            'admin_password': PASSWORD
        },
        'hardware_profile': {
            'vm_size': 'Standard_DS1_v2'
        },
        'storage_profile': {
            'image_reference': {
                'publisher': vm_reference['publisher'],
                'offer': vm_reference['offer'],
                'sku': vm_reference['sku'],
                'version': vm_reference['version']
            },
        },
        'network_profile': {
            'network_interfaces': [{
                'id': nic_id,
            }]
        },
    }


if __name__ == "__main__":
    run_example()
```

Überprüfen Sie den virtuellen Computer in Ihrem Abonnement nach Abschluss des Programms mithilfe der Azure CLI 2.0:

```azurecli-interactive
az vm list --resource-group sampleVmResourceGroup
```

Nachdem Sie sich vergewissert haben, dass der Code erfolgreich ausgeführt wurde, löschen Sie den virtuellen Computer und dessen Ressourcen über die Befehlszeile.

```azurecli-interactive
az group delete --name sampleVmResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a>Bereitstellen einer Web-App aus einem GitHub-Repository
Dieser Code stellt eine Flask-Webanwendung aus der Verzweigung `master` in einem öffentlichen GitHub-Repository für eine neue [Azure App Service-Web-App](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) bereit, die unter dem Tarif „Free“ ausgeführt wird. 

Voraussetzungen: Forken Sie https://github.com/Azure-Samples/python-docs-hello-world.

Authentifizieren:
```azcli
az login
```
Erstellen Sie eine Ressourcengruppe:
```azurecli-interactive
az group create -l eastus -n sampleWebResourceGroup
```

Erstellen eines App Service-Tarifs vom Typ „Free“:
```azurecli-interactive
az appservice plan create -g sampleWebResourceGroup -n sampleFreePlan  --sku Free
```

```python
from azure.mgmt.web import WebSiteManagementClient
from azure.mgmt.web.models import Site, SiteSourceControl, SiteConfig
from azure.common.client_factory import get_client_from_cli_profile

RESOURCE_GROUP_NAME = 'sampleWebResourceGroup'
SERVICE_PLAN_NAME = 'sampleFreePlanName'
WEB_APP_NAME = 'sampleflaskapp123'
REPO_URL = 'GitHub_Repository_URL'

#log in
web_client = get_client_from_cli_profile(WebSiteManagementClient)

# get service plan id
service_plan = web_client.app_service_plans.get(RESOURCE_GROUP_NAME, SERVICE_PLAN_NAME)

# create a web app
siteConfiguration = SiteConfig(
    python_version='3.4',
)
site_async_operation = web_client.web_apps.create_or_update(
    RESOURCE_GROUP_NAME,
    WEB_APP_NAME,
    Site(
        location='eastus',
        server_farm_id=service_plan.id,
        site_config=siteConfiguration
    ),
)

site = site_async_operation.result()
print('created webapp: ' + site.default_host_name)

# continuous deployment with GitHub
source_control_async_operation = web_client.web_apps.create_or_update_source_control(
    RESOURCE_GROUP_NAME,
    WEB_APP_NAME,
    SiteSourceControl(
        location='GitHub',
        repo_url= REPO_URL,
        branch='master'
    )
)

source_control = source_control_async_operation.result()
print("added source control to: " + source_control.name + "azurewebsites.net")
```

Öffnen Sie die Anwendung über die Befehlszeilenschnittstelle in einem Browser:
```azurecli-interactive
az appservice web browse --resource-group sampleWebResourceGroup --name YOUR_APP_NAME
```

Entfernen Sie die Web-App und den Plan aus Ihrem Abonnement, nachdem Sie die Bereitstellung überprüft haben. 
```azurecli-interactive
az group delete --name sampleWebResourceGroup
```


## <a name="connect-to-a-sql-database"></a>Herstellen einer Verbindung mit einer SQL-Datenbank
Dieser Code erstellt eine neue SQL­-Datenbank mit einer Firewallregel, die Remotezugriffe zulässt, und stellt anschließend unter Verwendung des Microsoft-ODBC-Treibers eine Verbindung mit der Datenbank her. pyodbc verwendet den Microsoft ODBC-Treiber unter Linux zum Herstellen von Verbindungen mit SQL-Datenbank-Instanzen. 

Authentifizieren:
```azcli
az login
```
Erstellen Sie eine Ressourcengruppe:
```azurecli-interactive
az group create -l eastus -n azure-sample-group
```

Erstellen einer SQL Server-Instanz:
```azurecli-interactive
az sql server create --admin-password HusH_Sec4et --admin-user mysecretname -l eastus -n samplesqlserver123 -g azure-sample-group
```

Hinzufügen einer Firewallregel:
```azurecli-interactive
az sql server firewall-rule create --end-ip-address 167.220.0.235 --name firewall_rule_name_123.123.123.123 --resource-group azure-sample-group --server samplesqlserver123 --start-ip-address 123.123.123.123
```

Erstellen einer SQL-Datenbank:
```azurecli-interactive
az sql db create --name sample-db --resource-group azure-sample-group --server samplesqlserver123
```


```python
from azure.mgmt.sql import SqlManagementClient
from azure.common.client_factory import get_client_from_cli_profile
import pyodbc

LOCATION = 'eastus'
GROUP_NAME = 'azure-sample-group'
SERVER_NAME = 'samplesqlserver123'
DATABASE_NAME = 'sample-db'
USER_NAME ='mysecretname'
PASSWORD='HusH_Sec4et'

# authenticate
sql_client = get_client_from_cli_profile(SqlManagementClient)


def run_example():
    # Get SQL database
    print('Get SQL database')
    database = sql_client.databases.get(
        GROUP_NAME,
        SERVER_NAME,
        DATABASE_NAME
    )
    print(database)
    print("\n\n")


def create_and_insert():
    server = SERVER_NAME+'.database.windows.net'
    database = DATABASE_NAME
    username = USER_NAME
    password = PASSWORD
    driver = '{ODBC Driver 13 for SQL Server}'
    cnxn = pyodbc.connect(
        'DRIVER=' + driver + ';PORT=1433;SERVER=' + server + ';PORT=1443;DATABASE=' + database + ';UID=' + username + ';PWD=' + password)
    cursor = cnxn.cursor()
    tsql = "CREATE TABLE CLOUD (name varchar(255), code int);"
    tsqlInsert = "INSERT INTO CLOUD (name, code) VALUES ('Azure', 1); "
    selectValues = "SELECT * FROM CLOUD"
    with cursor.execute(tsql):
        print('Successfully created table!')
    with cursor.execute(tsqlInsert):
        print('Successfully inserted data into table')
    cursor.execute(selectValues)
    row = cursor.fetchone()
    while row:
        print(str(row[0]) + " " + str(row[1]))
        row = cursor.fetchone()
    cnxn.commit()

if __name__ == "__main__":
    run_example()
    create_and_insert()
```

Nachdem Sie sich vergewissert haben, dass der Code erfolgreich ausgeführt wurde, löschen Sie die SQL-Datenbank und ihre Ressourcen mit der CLI.

```azurecli-interactive
az group delete --name azure-sample-group
```

## <a name="write-a-blob-into-a-new-storage-account"></a>Schreiben eines Blobs in ein neues Speicherkonto

Authentifizieren:
```azcli
az login
```
Erstellen Sie eine Ressourcengruppe:
```azurecli-interactive
az group create -l eastus -n sampleStorageResourceGroup
```

Erstellen eines Speicherkontos:
```azurecli-interactive
az storage account create -n samplestorageaccountname -g sampleStorageResourceGroup -l eastus --sku Standard_RAGRS
```

Dieser Code erstellt ein [Azure-Speicherkonto](https://docs.microsoft.com/azure/storage/storage-introduction) und anschließend unter Verwendung von Azure Storage-Bibliotheken für Python eine neue HTML-Datei in der Cloud. 
```python
from azure.storage import CloudStorageAccount
from azure.storage.blob import PublicAccess
from azure.storage.blob.models import ContentSettings
from azure.common.client_factory import get_client_from_cli_profile
from azure.mgmt.storage import StorageManagementClient

RESOURCE_GROUP = 'sampleStorageResourceGroup'
STORAGE_ACCOUNT_NAME = 'samplestorageaccountname'
CONTAINER_NAME = 'samplecontainername'

# log in
storage_client = get_client_from_cli_profile(StorageManagementClient)

# create a public storage container to hold the file
storage_keys = storage_client.storage_accounts.list_keys(RESOURCE_GROUP, STORAGE_ACCOUNT_NAME)
storage_keys = {v.key_name: v.value for v in storage_keys.keys}

storage_client = CloudStorageAccount(STORAGE_ACCOUNT_NAME, storage_keys['key1'])
blob_service = storage_client.create_block_blob_service()

blob_service.create_container(CONTAINER_NAME, public_access=PublicAccess.Container)

blob_service.create_blob_from_bytes(
    CONTAINER_NAME,
    'helloworld.html',
    b'<center><h1>Hello World!</h1></center>',
    content_settings=ContentSettings('text/html')
)

print(blob_service.make_blob_url(CONTAINER_NAME, 'helloworld.html'))
```
Navigieren Sie zur ausgegebenen URL, um den erfolgreichen Upload der Inhalte zu überprüfen. 

Bereinigen Sie das Speicherkonto über die Befehlszeilenschnittstelle:
```azurecli-interactive
az group delete --name sampleStorageResourceGroup
```

## <a name="explore-more-samples"></a>Erkunden weiterer Beispiele

Weitere Informationen zur Ressourcenverwaltung und Aufgabenautomatisierung mit den Azure-Verwaltungsbibliotheken für Python finden Sie in unserem Beispielcode für [virtuelle Computer](python-sdk-azure-web-apps-samples.md), [Web-Apps](python-sdk-azure-web-apps-samples.md) und [SQL-Datenbank](python-sdk-azure-sql-database-samples.md).


## <a name="reference"></a>Referenz

Für alle Pakete steht eine [Referenz](/python/api/overview/azure/?view=azure-python) zur Verfügung.
