---
title: "Azure MySQL-Bibliotheken für Python"
description: 
keywords: Azure, Python, SDK, API, SQL, Datenbank, MySQL
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/12/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: mysql
ms.openlocfilehash: 2ea2ed06d4532f9c9366257e049856dcef73385e
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2017
---
# <a name="azure-mysql-libraries-for-python"></a><span data-ttu-id="4b835-103">Azure MySQL-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="4b835-103">Azure MySQL libraries for Python</span></span> 

## <a name="overview"></a><span data-ttu-id="4b835-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="4b835-104">Overview</span></span>

<span data-ttu-id="4b835-105">Verwenden Sie über Python mit dem MySQL-Manager und pyodbc in [Azure MySQL-Datenbank](/azure/mysql/overview) gespeicherte Ressourcen und Daten.</span><span class="sxs-lookup"><span data-stu-id="4b835-105">Work with resources and data stored in [Azure MySQL Database](/azure/mysql/overview) from python with the MySQL manager and pyodbc.</span></span>

## <a name="client-odbc-driver-and-pyodbc"></a><span data-ttu-id="4b835-106">ODBC-Clienttreiber und pyodbc</span><span class="sxs-lookup"><span data-stu-id="4b835-106">Client ODBC driver and pyodbc</span></span>

<span data-ttu-id="4b835-107">Für den Zugriff auf Azure-Datenbank für MySQL wird als Clientbibliothek der [ODBC-Treiber](/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries) von Microsoft empfohlen.</span><span class="sxs-lookup"><span data-stu-id="4b835-107">The recommended client library for accessing Azure Database for MySQL is the Microsoft [ODBC driver](/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries).</span></span> <span data-ttu-id="4b835-108">Verwenden Sie den ODBC-Treiber zum Herstellen einer Verbindung mit der Datenbank und zum direkten Ausführen von SQL-Anweisungen.</span><span class="sxs-lookup"><span data-stu-id="4b835-108">Use the ODBC driver to connect to the database and execute SQL statements directly.</span></span>

### <a name="example"></a><span data-ttu-id="4b835-109">Beispiel</span><span class="sxs-lookup"><span data-stu-id="4b835-109">Example</span></span>

<span data-ttu-id="4b835-110">Stellen Sie eine Verbindung mit Azure-Datenbank für MySQL her, und wählen Sie alle Datensätze in der Vertriebstabelle aus.</span><span class="sxs-lookup"><span data-stu-id="4b835-110">Connect to a Azure Database for MySQL and select all records in the sales table.</span></span> <span data-ttu-id="4b835-111">Sie können die ODBC-Verbindungszeichenfolge für die Datenbank aus dem Azure-Portal abrufen.</span><span class="sxs-lookup"><span data-stu-id="4b835-111">You can get the ODBC connection string for the database from the Azure Portal.</span></span>

```python
SERVER = 'YOUR_SEVER_NAME' + '.mysql.database.azure.com'
DATABASE = 'YOUR_DATABASE_NAME'
USERNAME = 'YOUR_MYSQL_USERNAME'
PASSWORD = 'YOUR_MYSQL_PASSWORD'

DRIVER = '{MySQL ODBC 5.3 UNICODE Driver}'
cnxn = pyodbc.connect(
    'DRIVER=' + DRIVER + ';PORT=3306;SERVER=' + SERVER + ';PORT=3306;DATABASE=' + DATABASE + ';UID=' + USERNAME + ';PWD=' + PASSWORD)
cursor = cnxn.cursor()
selectsql = "SELECT * FROM SALES"  # SALES is an example table name
cursor.execute(selectsql)
```

## <a name="management-api"></a><span data-ttu-id="4b835-112">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="4b835-112">Management API</span></span>

<span data-ttu-id="4b835-113">Über die Verwaltungs-API können Sie MySQL-Ressourcen in Ihrem Abonnement erstellen und verwalten.</span><span class="sxs-lookup"><span data-stu-id="4b835-113">Create and manage MySQL resources in your subscription with the management API.</span></span>

### <a name="requirements"></a><span data-ttu-id="4b835-114">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="4b835-114">Requirements</span></span>
<span data-ttu-id="4b835-115">Sie müssen die MySQL-Verwaltungsbibliotheken für Python installieren.</span><span class="sxs-lookup"><span data-stu-id="4b835-115">You must install the MySQL management libraries for Python.</span></span>
```bash
pip install azure-mgmt-rdbms
```

<span data-ttu-id="4b835-116">Ausführliche Informationen zum Abrufen von Anmeldeinformationen für die Authentifizierung beim Verwaltungsclient finden Sie unter [Authenticate with the Azure Management Libraries for Python](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) (Authentifizieren bei den Azure-Verwaltungsbibliotheken für Python).</span><span class="sxs-lookup"><span data-stu-id="4b835-116">Please see the [Python SDK authentication](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) page for details on obtaining credentials to authenticate with the management client.</span></span>

### <a name="example"></a><span data-ttu-id="4b835-117">Beispiel</span><span class="sxs-lookup"><span data-stu-id="4b835-117">Example</span></span>

<span data-ttu-id="4b835-118">Erstellen Sie eine MySQL 5.7-Datenbank-Ressource, und schränken Sie den Zugriff mithilfe einer Firewallregel auf einen bestimmten IP-Adressbereich ein.</span><span class="sxs-lookup"><span data-stu-id="4b835-118">Create a MySQL 5.7 Database resource and restrict access to a range of IP addresses using a firewall rule.</span></span>

```python

from azure.mgmt.rdbms.mysql import MySQLManagementClient
from azure.mgmt.rdbms.mysql.models import ServerForCreate, ServerPropertiesForDefaultCreate, ServerVersion

SUBSCRIPTION_ID = "YOUR_AZURE_SUBSCRIPTION_ID"
RESOURCE_GROUP = "YOUR_AZURE_RESOURCE-GROUP_WITH_POSTGRES"
MYSQL_SERVER = "YOUR_DESIRED_MYSQL_SERVER_NAME"
MYSQL_ADMIN_USER = "YOUR_MYSQL_ADMIN_USERNAME"
MYSQL_ADMIN_PASSWORD = "YOUR_MYSQL_ADMIN_PASSOWRD"
LOCATION = "westus"  # example Azure availability zone, should match resource group


client = MySQLManagementClient(credentials=creds,
    subscription_id=SUBSCRIPTION_ID)

server_creation_poller = client.servers.create_or_update(
    resource_group_name=RESOURCE_GROUP,
    server_name=MYSQL_SERVER,
    ServerForCreate(
        ServerPropertiesForDefaultCreate(
            administrator_login=MYSQL_ADMIN_USER,
            administrator_login_password=MYSQL_ADMIN_PASSWORD,
            version=ServerVersion.five_full_stop_seven
        ),
        location=LOCATION
    )
)

server = server_creation_poller.result()

# Open access to this server for IPs
rule_creation_poller = client.firewall_rules.create_or_update(
    RESOURCE_GROUP
    MYSQL_SERVER,
    "some_custom_ip_range_whitelist_rule_name",  # Custom firewall rule name
    "123.123.123.123",  # Start ip range
    "167.220.0.235"  # End ip range
)

firewall_rule = rule_creation_poller.result()
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="4b835-119">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="4b835-119">Explore the Management APIs</span></span>](/python/api/overview/azure/mysql/managementlibrary)