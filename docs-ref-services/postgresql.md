---
title: Azure PostgreSQL-Bibliotheken für Python
description: ''
keywords: Azure, Python, SDK, API, SQL, Datenbank, Postgres, PostgreSQL
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/11/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: postgresql
ms.openlocfilehash: cad5995072d5040764986765d9a900f46f5141ec
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
ms.locfileid: "29478933"
---
#<a name="azure-postgresql-libraries-for-python"></a><span data-ttu-id="81d4d-103">Azure PostgreSQL-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="81d4d-103">Azure PostgreSQL libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="81d4d-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="81d4d-104">Overview</span></span>
<span data-ttu-id="81d4d-105">Verwenden Sie den ODBC-Treiber und pyodbc zum Herstellen einer Verbindung mit der Datenbank und zum direkten Ausführen von SQL-Anweisungen.</span><span class="sxs-lookup"><span data-stu-id="81d4d-105">Use the ODBC driver and pyodbc to connect to the database and execute SQL statements directly.</span></span>

<span data-ttu-id="81d4d-106">Weitere Informationen zu [Azure-Datenbank für PostgreSQL](https://docs.microsoft.com/azure/postgresql/)</span><span class="sxs-lookup"><span data-stu-id="81d4d-106">Learn more about [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span></span>

## <a name="client-odbc-driver-and-pyodbc"></a><span data-ttu-id="81d4d-107">ODBC-Clienttreiber und pyodbc</span><span class="sxs-lookup"><span data-stu-id="81d4d-107">Client ODBC driver and pyodbc</span></span>
<span data-ttu-id="81d4d-108">Für den Zugriff auf Azure-Datenbank für PostgreSQL werden als Clientbibliothek der [ODBC-Treiber von Microsoft und pyodbc](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries) empfohlen.</span><span class="sxs-lookup"><span data-stu-id="81d4d-108">The recommended client library for accessing Azure Database for PostgreSQL is the Microsoft [ODBC driver and pyodbc](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries)</span></span>

### <a name="example"></a><span data-ttu-id="81d4d-109">Beispiel</span><span class="sxs-lookup"><span data-stu-id="81d4d-109">Example</span></span> 

<span data-ttu-id="81d4d-110">Stellen Sie eine Verbindung mit Azure-Datenbank für PostgreSQL her, und wählen Sie alle Datensätze in der Tabelle `SALES` aus.</span><span class="sxs-lookup"><span data-stu-id="81d4d-110">Connect to a Azure Database for PostgreSQL and select all records in the `SALES` table.</span></span> <span data-ttu-id="81d4d-111">Sie können die ODBC-Verbindungszeichenfolge für die Datenbank aus dem Azure-Portal abrufen.</span><span class="sxs-lookup"><span data-stu-id="81d4d-111">You can get the ODBC connection string for the database from the Azure Portal.</span></span>

```python
import pyodbc

SERVER = 'YOUR_SERVER_NAME.postgres.database.azure.com'
DATABASE = 'YOUR_DB_NAME'
USERNAME = 'YOUR_USERNAME'
PASSWORD = 'YOUR_PASSWORD'

DRIVER = '{PostgreSQL ODBC Driver}'
cnxn = pyodbc.connect(
    'DRIVER=' + DRIVER + ';PORT=5432;SERVER=' + SERVER +
    ';PORT=5432;DATABASE=' + DATABASE + ';UID=' + USERNAME +
    ';PWD=' + PASSWORD)
cursor = cnxn.cursor()
selectsql = "SELECT * FROM SALES" # SALES is an example table name
cursor.execute(selectsql)
```

## <a name="management-api"></a><span data-ttu-id="81d4d-112">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="81d4d-112">Management API</span></span>
### <a name="requirements"></a><span data-ttu-id="81d4d-113">Requirements (Anforderungen)</span><span class="sxs-lookup"><span data-stu-id="81d4d-113">Requirements</span></span>
<span data-ttu-id="81d4d-114">Sie müssen die PostgreSQL-Verwaltungsbibliotheken für Python installieren.</span><span class="sxs-lookup"><span data-stu-id="81d4d-114">You must install the PostgreSQL management libraries for Python.</span></span>
```bash
pip install azure-mgmt-rdbms
```

<span data-ttu-id="81d4d-115">Ausführliche Informationen zum Abrufen von Anmeldeinformationen für die Authentifizierung beim Verwaltungsclient finden Sie unter [Authenticate with the Azure Management Libraries for Python](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) (Authentifizieren bei den Azure-Verwaltungsbibliotheken für Python).</span><span class="sxs-lookup"><span data-stu-id="81d4d-115">Please see the [Python SDK authentication](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) page for details on obtaining credentials to authenticate with the management client.</span></span>

### <a name="example"></a><span data-ttu-id="81d4d-116">Beispiel</span><span class="sxs-lookup"><span data-stu-id="81d4d-116">Example</span></span>
<span data-ttu-id="81d4d-117">In diesem Beispiel wird eine neue Postgres-Datenbank auf unserem vorhandenen Postgres-Server erstellt:</span><span class="sxs-lookup"><span data-stu-id="81d4d-117">In this example we will create a new Postgres database on our existing Postgres server.</span></span>
```python
from azure.mgtm.rdbms.postgresql import PostgreSQLManagementClient

SUBSCRIPTION_ID = "YOUR_AZURE_SUBSCRIPTION_ID"
RESOURCE_GROUP = "YOUR_AZURE_RESOURCE_GROUP_WITH_POSTGRES"
POSTGRES_SERVER = "YOUR_POSTGRES_SERVER_NAME"
DB_NAME = "YOUR_DESIRED_DATABASE_NAME"

client = PostgreSQLManagementClient(credentials, SUBSCRIPTION_ID)

db_creation_poller = client.databases.create_or_update(
    resource_group_name=RESOURCE_GROUP,
    server_name=POSTGRES_SERVER, database_name=DB_NAME)
db = db_creation_poller.result()
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="81d4d-118">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="81d4d-118">Explore the Management APIs</span></span>](/python/api/overview/azure/postgresql/management)

