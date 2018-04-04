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
ms.openlocfilehash: 391b556ece7d818406fa501763814eb7f0d50d22
ms.sourcegitcommit: 41e6e6b5469271f4ec497a322b460e2a2af2c73d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="azure-cosmos-db-libraries-for-python"></a><span data-ttu-id="f31ef-104">Azure DB Cosmos-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="f31ef-104">Azure Cosmos DB libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="f31ef-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="f31ef-105">Overview</span></span>

<span data-ttu-id="f31ef-106">Verwenden Sie Azure Cosmos DB in Ihren Python-Anwendungen, um JSON-Dokumente in einem NoSQL-Datenspeicher zu speichern und abzufragen.</span><span class="sxs-lookup"><span data-stu-id="f31ef-106">Use Azure Cosmos DB in your Python applications to store and query JSON documents in a NoSQL data store.</span></span>

<span data-ttu-id="f31ef-107">Erfahren Sie mehr über [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="f31ef-107">Learn more about [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

## <a name="client-library"></a><span data-ttu-id="f31ef-108">Clientbibliothek</span><span class="sxs-lookup"><span data-stu-id="f31ef-108">Client library</span></span>
 ```bash
pip install pydocumentdb
 ```

## <a name="management-library"></a><span data-ttu-id="f31ef-109">Verwaltungsbibliothek</span><span class="sxs-lookup"><span data-stu-id="f31ef-109">Management library</span></span>
```bash
pip install azure-mgmt-cosmosdb
```

### <a name="example"></a><span data-ttu-id="f31ef-110">Beispiel</span><span class="sxs-lookup"><span data-stu-id="f31ef-110">Example</span></span>

<span data-ttu-id="f31ef-111">Suchen Sie entsprechende Dokumente in Azure Cosmos DB über eine SQL-ähnliche Abfrageschnittstelle:</span><span class="sxs-lookup"><span data-stu-id="f31ef-111">Find matching documents in Azure CosmosDB using a SQL-like query interface:</span></span>

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
> [<span data-ttu-id="f31ef-112">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="f31ef-112">Explore the Management APIs</span></span>](/python/api/overview/azure/cosmosdb/management)

## <a name="samples"></a><span data-ttu-id="f31ef-113">Beispiele</span><span class="sxs-lookup"><span data-stu-id="f31ef-113">Samples</span></span>

[<span data-ttu-id="f31ef-114">Entwickeln einer Python-App mit Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f31ef-114">Develop a Python app using Azure Cosmos DB</span></span>](https://azure.microsoft.com/resources/samples/azure-cosmos-db-documentdb-python-getting-started/)


