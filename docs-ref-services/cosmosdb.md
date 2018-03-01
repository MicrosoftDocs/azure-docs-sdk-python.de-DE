---
title: "Azure Cosmos DB-Bibliotheken für Python"
description: "Referenzdokumentation für die Python-Clientbibliotheken für Cosmos DB"
keywords: Azure, Python, SDK, API, SQL, Datenbank, PostGres, CosmosDB, NoSQL
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 08/11/2017
ms.topic: article
ms.devlang: python
ms.service: cosmosdb
ms.openlocfilehash: d56dd69f4fc4513034046f9f721608ad94ff5cfe
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
---
# <a name="azure-cosmosdb-libraries-for-python"></a>Azure Cosmos DB-Bibliotheken für Python

## <a name="overview"></a>Übersicht

Verwenden Sie Cosmos DB in Ihren Python-Anwendungen, um JSON-Dokumente in einem NoSQL-Datenspeicher zu speichern und abzufragen.

Weitere Informationen zu [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction)

## <a name="client-library"></a>Clientbibliothek
 ```bash
pip install pydocumentdb
 ```

## <a name="management-library"></a>Verwaltungsbibliothek
```bash
pip install azure-mgmt-cosmosdb
```

### <a name="example"></a>Beispiel

Suchen Sie entsprechende Dokumente in Cosmos DB über eine SQL-ähnliche Abfrageschnittstelle:

```python
import pydocumentdb
import pydocumentdb.document_client as document_client

# Initialize the Python DocumentDB client
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

[Entwickeln einer Python-App mit der DocumentDB-API von Azure Cosmos DB](https://azure.microsoft.com/resources/samples/azure-cosmos-db-documentdb-python-getting-started/)


