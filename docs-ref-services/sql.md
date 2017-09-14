---
title: "Azure SQL-Datenbank-Bibliotheken für Python"
description: 
keywords: Azure, Python, SDK, API, SQL, Datenbank, pyodbc
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/11/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: sql-database
ms.openlocfilehash: b580c5011412bc77fd8fd55b709a305be07e2316
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2017
---
# <a name="azure-sql-database-libraries-for-python"></a>Azure SQL-Datenbank-Bibliotheken für Python

## <a name="overview"></a>Übersicht

Arbeiten Sie mit dem Microsoft ODBC-Treiber und pyodbc über Python mit in [Azure SQL-Datenbank](/azure/sql-database/sql-database-technical-overview) gespeicherten Daten. 

## <a name="client-odbc-driver-and-pyodbc"></a>ODBC-Clienttreiber und pyodbc

```bash
pip install pyodbc
```
Weitere Informationen zum Installieren der Python- und Datenbankkommunikationsbibliotheken finden Sie [hier](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries).

### <a name="example"></a>Beispiel

Stellen Sie eine Verbindung mit einer SQL-Datenbank her, und wählen Sie alle Datensätze in einer Tabelle aus.

```python
import pyodbc 

SERVER = 'YOUR_SERVER_NAME.database.windows.net'
DATABASE = 'YOUR_DATABASE_NAME'
USERNAME = 'YOUR_DB_USERNAME'
PASSWORD = 'YOUR_DB_PASSWORD'

DRIVER= '{ODBC Driver 13 for SQL Server}'
cnxn = pyodbc.connect('DRIVER=' + DRIVER + ';PORT=1433;SERVER=' + SERVER +
    ';PORT=1443;DATABASE=' + DATABASE + ';UID=' + USERNAME + ';PWD=' + PASSWORD)
cursor = cnxn.cursor()
selectsql = "SELECT * FROM SALES"  # SALES is an example table name
cursor.execute(selectsql)
```

## <a name="management-api"></a>Verwaltungs-API

Über die Verwaltungs-API können Sie Azure SQL-Datenbank-Ressourcen in Ihrem Abonnement erstellen und verwalten. 

```bash
pip install azure-mgmt-sql
```

### <a name="example"></a>Beispiel

Erstellen Sie eine SQL-Datenbank-Ressource, und schränken Sie den Zugriff mithilfe einer Firewallregel auf einen bestimmten IP-Adressbereich ein.

```python
RESOURCE_GROUP = 'YOUR_RESOURCE_GROUP_NAME'
LOCATION = 'eastus'  # example Azure availability zone, should match resource group
SQL_DB = 'YOUR_SQLDB_NAME'

# Create a SQL server
server = sql_client.servers.create_or_update(
    RESOURCE_GROUP,
    SQL_DB,
    {
        'location': LOCATION,
        'version': '12.0', # Required for create
        'administrator_login': USERNAME, # Required for create
        'administrator_login_password': PASSWORD # Required for create
    }
)

# Open access to this server for IPs
firewall_rule = sql_client.firewall_rules.create_or_update(
    RESOURCE_GROUP
    SQL_DB,
    "firewall_rule_name_123.123.123.123",
    "123.123.123.123", # Start ip range
    "167.220.0.235"  # End ip range
)
```
> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/sql/managementlibrary)

## <a name="samples"></a>Beispiele

* [Erstellen und Verwalten von SQL-Datenbanken][1]    
* [Verwenden von Python zum Herstellen einer Verbindung und Abfragen von Daten][2]   

[1]: https://github.com/Azure-Samples/sql-database-python-manage
[2]: https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python

Zeigen Sie die [vollständige Liste](https://azure.microsoft.com/resources/samples/?platform=python&term=SQL) von Beispielen für Azure SQL-Datenbank an. 