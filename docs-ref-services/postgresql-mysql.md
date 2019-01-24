---
title: Azure MySQL-/PostgreSQL-Bibliotheken für Python
description: ''
keywords: Azure, Python, SDK, API, SQL, Datenbank, MySQL, PostgreSQL
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/19/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.openlocfilehash: 402e87ae81e6df64b040293992244902313e5b1b
ms.sourcegitcommit: fba77bdf8eb9f49621be94544d9fef88aff98c14
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/23/2019
ms.locfileid: "54747720"
---
# <a name="azure-mysqlpostgresql-libraries-for-python"></a>Azure MySQL-/PostgreSQL-Bibliotheken für Python

## <a name="mysql"></a>MySQL

Verwenden Sie über Python mit dem MySQL-Manager und pyodbc in [Azure MySQL-Datenbank](/azure/mysql/overview) gespeicherte Ressourcen und Daten.

### <a name="client-odbc-driver-and-pyodbc"></a>ODBC-Clienttreiber und pyodbc

Für den Zugriff auf Azure-Datenbank für MySQL wird als Clientbibliothek der [ODBC-Treiber](/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries) von Microsoft empfohlen. Verwenden Sie den ODBC-Treiber zum Herstellen einer Verbindung mit der Datenbank und zum direkten Ausführen von SQL-Anweisungen.

#### <a name="example"></a>Beispiel

Stellen Sie eine Verbindung mit Azure-Datenbank für MySQL her, und wählen Sie alle Datensätze in der Vertriebstabelle aus. Sie können die ODBC-Verbindungszeichenfolge für die Datenbank aus dem Azure-Portal abrufen.

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

### <a name="management-api"></a>Verwaltungs-API

Über die Verwaltungs-API können Sie MySQL-Ressourcen in Ihrem Abonnement erstellen und verwalten.

#### <a name="requirements"></a>Requirements (Anforderungen)
Sie müssen die MySQL-Verwaltungsbibliotheken für Python installieren.
```bash
pip install azure-mgmt-rdbms
```

Ausführliche Informationen zum Abrufen von Anmeldeinformationen für die Authentifizierung beim Verwaltungsclient finden Sie unter [Authenticate with the Azure Management Libraries for Python](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) (Authentifizieren bei den Azure-Verwaltungsbibliotheken für Python).

#### <a name="example"></a>Beispiel

Erstellen Sie eine MySQL 5.7-Datenbank-Ressource, und schränken Sie den Zugriff mithilfe einer Firewallregel auf einen bestimmten IP-Adressbereich ein.

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
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/postgresql/mysql/management)

## <a name="postgresql"></a>PostgreSQL
Verwenden Sie den ODBC-Treiber und pyodbc zum Herstellen einer Verbindung mit der Datenbank und zum direkten Ausführen von SQL-Anweisungen.

Weitere Informationen zu [Azure-Datenbank für PostgreSQL](https://docs.microsoft.com/azure/postgresql/)

### <a name="client-odbc-driver-and-pyodbc"></a>ODBC-Clienttreiber und pyodbc
Für den Zugriff auf Azure-Datenbank für PostgreSQL werden als Clientbibliothek der [ODBC-Treiber von Microsoft und pyodbc](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries) empfohlen.

#### <a name="example"></a>Beispiel 

Stellen Sie eine Verbindung mit Azure-Datenbank für PostgreSQL her, und wählen Sie alle Datensätze in der Tabelle `SALES` aus. Sie können die ODBC-Verbindungszeichenfolge für die Datenbank aus dem Azure-Portal abrufen.

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

### <a name="management-api"></a>Verwaltungs-API
#### <a name="requirements"></a>Requirements (Anforderungen)
Sie müssen die PostgreSQL-Verwaltungsbibliotheken für Python installieren.
```bash
pip install azure-mgmt-rdbms
```

Ausführliche Informationen zum Abrufen von Anmeldeinformationen für die Authentifizierung beim Verwaltungsclient finden Sie unter [Authenticate with the Azure Management Libraries for Python](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) (Authentifizieren bei den Azure-Verwaltungsbibliotheken für Python).

#### <a name="example"></a>Beispiel
In diesem Beispiel wird eine neue Postgres-Datenbank auf unserem vorhandenen Postgres-Server erstellt:
```python
from azure.mgmt.rdbms.postgresql import PostgreSQLManagementClient

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
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/postgresql/mysql/management)
