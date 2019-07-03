---
title: Azure SQL-Datenbank-Bibliotheken für Python
description: Stellen Sie über den ODBC-Treiber und pyodbc eine Verbindung mit Azure SQL-Datenbank her, oder verwalten Sie Azure SQL-Instanzen über die Verwaltungs-API.
author: lisawong19
ms.author: routlaw
manager: routlaw
ms.date: 01/09/2018
ms.topic: reference
ms.devlang: python
ms.service: sql-database
ms.openlocfilehash: 9b8a5b120425fc600f34c1e4c4456b0888814fe8
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534201"
---
# <a name="azure-sql-database-libraries-for-python"></a>Azure SQL-Datenbank-Bibliotheken für Python

## <a name="overview"></a>Übersicht

Arbeiten Sie mit dem [ODBC-Datenbanktreiber](https://github.com/mkleehammer/pyodbc/wiki/Drivers-and-Driver-Managers) von pyodbc über Python mit in [Azure SQL-Datenbank](/azure/sql-database/sql-database-technical-overview) gespeicherten Daten. Sehen Sie sich unsere [Schnellstartanleitung](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) zum Herstellen einer Verbindung mit einer Azure SQL-Datenbank und zum Abrufen von Daten mithilfe von Transact-SQL-Anweisungen an. Sie enthält außerdem ein [Beispiel](https://github.com/mkleehammer/pyodbc/wiki/Getting-started) für die ersten Schritte mit pyodbc.

## <a name="install-odbc-driver-and-pyodbc"></a>Installieren des ODBC-Treibers und von pyodbc

```bash
pip install pyodbc
```
Weitere [Einzelheiten](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#prerequisites) zum Installieren der Python- und Datenbankkommunikationsbibliotheken

## <a name="connect-and-execute-a-sql-query"></a>Herstellen einer Verbindung und Ausführen einer SQL-Abfrage

### <a name="connect-to-a-sql-database"></a>Herstellen einer Verbindung mit einer SQL-Datenbank-Instanz

```python
import pyodbc

server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
driver= '{ODBC Driver 13 for SQL Server}'

cnxn = pyodbc.connect('DRIVER='+driver+';PORT=1433;SERVER='+server+';PORT=1443;DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
```

### <a name="execute-a-sql-query"></a>Ausführen einer SQL-Abfrage

```python
cursor.execute("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid")
row = cursor.fetchone()
while row:
    print (str(row[0]) + " " + str(row[1]))
    row = cursor.fetchone()
```

> [!div class="nextstepaction"]
> [pyodbc-Beispiel](https://github.com/mkleehammer/pyodbc/wiki/Getting-started)

## <a name="connecting-to-orms"></a>Herstellen einer Verbindung mit ORMs

pyodbc kann mit anderen ORMs wie [SQLAlchemy](https://docs.sqlalchemy.org/en/latest/dialects/mssql.html?highlight=pyodbc#module-sqlalchemy.dialects.mssql.pyodbc) und [Django](https://github.com/lionheart/django-pyodbc/) verwendet werden. 

## <a name="management-apipythonapioverviewazuresqlmanagement"></a>[Verwaltungs-API](/python/api/overview/azure/sql/management)

Über die Verwaltungs-API können Sie Azure SQL-Datenbank-Ressourcen in Ihrem Abonnement erstellen und verwalten. 

```bash
pip install azure-common
pip install azure-mgmt-sql
pip install azure-mgmt-resource
```

## <a name="example"></a>Beispiel

Erstellen Sie eine SQL-Datenbank-Ressource, und schränken Sie den Zugriff mithilfe einer Firewallregel auf einen bestimmten IP-Adressbereich ein.

```python
from azure.common.client_factory import get_client_from_cli_profile
from azure.mgmt.resource import ResourceManagementClient
from azure.mgmt.sql import SqlManagementClient

RESOURCE_GROUP = 'YOUR_RESOURCE_GROUP_NAME'
LOCATION = 'eastus'  # example Azure availability zone, should match resource group
SQL_SERVER = 'yourvirtualsqlserver'
SQL_DB = 'YOUR_SQLDB_NAME'
USERNAME = 'YOUR_USERNAME'
PASSWORD = 'YOUR_PASSWORD'

# create resource client
resource_client = get_client_from_cli_profile(ResourceManagementClient)
# create resource group
resource_client.resource_groups.create_or_update(RESOURCE_GROUP, {'location': LOCATION})

sql_client = get_client_from_cli_profile(SqlManagementClient)

# Create a SQL server
server = sql_client.servers.create_or_update(
    RESOURCE_GROUP,
    SQL_SERVER,
    {
        'location': LOCATION,
        'version': '12.0', # Required for create
        'administrator_login': USERNAME, # Required for create
        'administrator_login_password': PASSWORD # Required for create
    }
)

# Create a SQL database in the Basic tier
database = sql_client.databases.create_or_update(
    RESOURCE_GROUP,
    SQL_SERVER,
    SQL_DB,
    {
        'location': LOCATION,
        'collation': 'SQL_Latin1_General_CP1_CI_AS',
        'create_mode': 'default',
        'requested_service_objective_name': 'Basic'
    }
)

# Open access to this server for IPs
firewall_rule = sql_client.firewall_rules.create_or_update(
    RESOURCE_GROUP,
    SQL_DB,
    "firewall_rule_name_123.123.123.123",
    "123.123.123.123", # Start ip range
    "167.220.0.235"  # End ip range
)
```
> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/sql/management)

