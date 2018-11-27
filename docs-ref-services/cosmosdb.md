---
title: Azure DB Cosmos-Bibliotheken für Python
description: Referenzdokumentation für die Python-Clientbibliotheken für Azure Cosmos DB
keywords: Azure, Python, SDK, API, SQL, Datenbank, PostGres,Cosmos DB, NoSQL
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 03/20/2018
ms.topic: article
ms.devlang: python
ms.service: cosmosdb
ms.openlocfilehash: c2f3ea017a8864d4d2fb74a439c420f1f0313082
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2018
ms.locfileid: "52276794"
---
# <a name="azure-cosmos-db-libraries-for-python"></a>Azure DB Cosmos-Bibliotheken für Python

## <a name="overview"></a>Übersicht

Verwenden Sie Azure Cosmos DB in Ihren Python-Anwendungen, um JSON-Dokumente in einem NoSQL-Datenspeicher zu speichern und abzufragen.

Erfahren Sie mehr über [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).

## <a name="client-library"></a>Clientbibliothek
 ```bash
pip install pydocumentdb
 ```

## <a name="management-library"></a>Verwaltungsbibliothek
```bash
pip install azure-mgmt-cosmosdb
```

### <a name="example"></a>Beispiel

Suchen Sie entsprechende Dokumente in Azure Cosmos DB über eine SQL-ähnliche Abfrageschnittstelle:

```python
import pydocumentdb
import pydocumentdb.document_client as document_client

# Initialize the Python Azure Cosmos DB client
client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
# Create a database
db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })

# Create collection options
options = {
    'offerEnableRUPerMinuteThroughput': True,
    'offerVersion': "V2",
    'offerThroughput': 400
}

# Create a collection
collection = client.CreateCollection(db['_self'], { 'id': config['DOCUMENTDB_COLLECTION'] }, options)

# Create some documents
document1 = client.CreateDocument(collection['_self'],
    { 
        'id': 'server1',
        'Web Site': 0,
        'Cloud Service': 0,
        'Virtual Machine': 0,
        'name': 'some' 
    })

# Query them in SQL
query = { 'query': 'SELECT * FROM server s' }    

options = {} 
options['enableCrossPartitionQuery'] = True
options['maxItemCount'] = 2

result_iterable = client.QueryDocuments(collection['_self'], query, options)
results = list(result_iterable)

print(results)
```
> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/cosmosdb/management)

## <a name="samples"></a>Beispiele

* [Entwickeln einer Python-App zum Zugreifen auf und Verwalten von Daten, die in einem Azure Cosmos DB-SQL-API-Konto gespeichert sind](https://github.com/Azure-Samples/azure-cosmos-db-python-getting-started.git)

* [Entwickeln einer Python-App zum Zugreifen auf und Verwalten von Daten, die in einem Azure Cosmos DB-MongoDB-API-Konto gespeichert sind](https://github.com/Azure-Samples/CosmosDB-Flask-Mongo-Sample.git)

* [Entwickeln einer Python-App zum Zugreifen auf und Verwalten von Daten, die in einem Azure Cosmos DB-Gremlin-API-Konto gespeichert sind](https://github.com/Azure-Samples/azure-cosmos-db-graph-python-getting-started.git)

* [Entwickeln einer Python-App zum Zugreifen auf und Verwalten von Daten, die in einem Azure Cosmos DB-Cassandra-API-Konto gespeichert sind](https://github.com/Azure-Samples/azure-cosmos-db-cassandra-python-getting-started.git)

* [Entwickeln einer Python-App zum Zugreifen auf und Verwalten von Daten, die in einem Azure Cosmos DB-Tabellen-API-Konto gespeichert sind](https://github.com/Azure-Samples/storage-python-getting-started.git)


