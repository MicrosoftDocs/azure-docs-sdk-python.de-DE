---
title: "Azure Storage-Bibliotheken für Python"
description: 
keywords: Azure, Python, SDK, API, Storage
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/12/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: storage
ms.openlocfilehash: 64465964d32934a6a45dec44cb92a0a8a84b9c37
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2017
---
# <a name="azure-storage-libraries-for-python"></a><span data-ttu-id="202c1-103">Azure Storage-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="202c1-103">Azure Storage libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="202c1-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="202c1-104">Overview</span></span>
- <span data-ttu-id="202c1-105">Mit [Azure Blob Storage](https://docs.microsoft.com/en-us/azure/storage/storage-python-how-to-use-blob-storage) können Sie Objekte und Dateien lesen und schreiben.</span><span class="sxs-lookup"><span data-stu-id="202c1-105">Read and write objects and files from [Azure Blob storage](https://docs.microsoft.com/en-us/azure/storage/storage-python-how-to-use-blob-storage)</span></span>
- <span data-ttu-id="202c1-106">Senden und Empfangen von Nachrichten zwischen Anwendungen mit Cloudverbindung per [Azure Queue Storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage)</span><span class="sxs-lookup"><span data-stu-id="202c1-106">Send and receive messages between cloud-connected applications with [Azure Queue storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage)</span></span>
- <span data-ttu-id="202c1-107">Lesen und Schreiben von großen strukturierten Datenmengen per [Azure Table Storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage)</span><span class="sxs-lookup"><span data-stu-id="202c1-107">Read and write large structured data with [Azure Table storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage)</span></span> 
- <span data-ttu-id="202c1-108">Freigeben von Speicher zwischen Apps mit [Azure-Dateispeicher](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage)</span><span class="sxs-lookup"><span data-stu-id="202c1-108">Share storage between apps with [Azure File storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage)</span></span>

<span data-ttu-id="202c1-109">Mit den Verwaltungsbibliotheken können Sie Azure Storage-Konten erstellen, aktualisieren und verwalten und Zugriffsschlüssel über Ihren Python-Code abfragen und neu generieren.</span><span class="sxs-lookup"><span data-stu-id="202c1-109">Create, update, and manage Azure Storage accounts and query and regenerate access keys from your Python code with the management libraries.</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="202c1-110">Installieren der Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="202c1-110">Install the libraries</span></span>

### <a name="client"></a><span data-ttu-id="202c1-111">Client-</span><span class="sxs-lookup"><span data-stu-id="202c1-111">Client</span></span>

```bash
pip install azure-storage
```

### <a name="management"></a><span data-ttu-id="202c1-112">Verwaltung</span><span class="sxs-lookup"><span data-stu-id="202c1-112">Management</span></span>

```bash
pip install azure-mgmt-storage
```

## <a name="example"></a><span data-ttu-id="202c1-113">Beispiel</span><span class="sxs-lookup"><span data-stu-id="202c1-113">Example</span></span>
```python
storage_client = CloudStorageAccount(storage_account_name, storage_key)
blob_service = storage_client.create_block_blob_service()

blob_service.create_container(
    'mycontainername',
    public_access=PublicAccess.Blob
)

blob_service.create_blob_from_bytes(
    'mycontainername',
    'myblobname',
    b'<center><h1>Hello World!</h1></center>',
    content_settings=ContentSettings('text/html')
)

print(blob_service.make_blob_url('mycontainername', 'myblobname'))
```

## <a name="samples"></a><span data-ttu-id="202c1-114">Beispiele</span><span class="sxs-lookup"><span data-stu-id="202c1-114">Samples</span></span>

| | |
|--|--|
| [<span data-ttu-id="202c1-115">Erste Schritte mit Azure Blob Storage in Python</span><span class="sxs-lookup"><span data-stu-id="202c1-115">Get started with Azure Blob Storage in Python</span></span>](https://azure.microsoft.com/resources/samples/storage-blob-python-getting-started/) | <span data-ttu-id="202c1-116">Erstellen, Lesen, Aktualisieren, Beschränken des Zugriffs und Löschen von Dateien und Objekten in Azure Storage</span><span class="sxs-lookup"><span data-stu-id="202c1-116">Create, read, update, restrict access, and delete files and objects in Azure Storage.</span></span> |
| [<span data-ttu-id="202c1-117">Erste Schritte mit Azure Queue Storage in Python</span><span class="sxs-lookup"><span data-stu-id="202c1-117">Get started with Azure Queue Storage in Python</span></span>](https://azure.microsoft.com/resources/samples/storage-queue-python-getting-started/) | <span data-ttu-id="202c1-118">Einfügen, Einsehen, Abrufen und Löschen von Nachrichten aus Azure Storage-Warteschlangen</span><span class="sxs-lookup"><span data-stu-id="202c1-118">Insert, peek, retrieve and delete messages from Azure Storage queues.</span></span> | 
| [<span data-ttu-id="202c1-119">Verwalten von Azure Storage-Konten</span><span class="sxs-lookup"><span data-stu-id="202c1-119">Manage Azure Storage accounts</span></span>](https://azure.microsoft.com/resources/samples/storage-python-manage) | <span data-ttu-id="202c1-120">Erstellen, Aktualisieren und Löschen von Speicherkonten</span><span class="sxs-lookup"><span data-stu-id="202c1-120">Create, update , and delete storage accounts.</span></span> <span data-ttu-id="202c1-121">Abrufen und erneutes Generieren von Speicherzugriffsschlüsseln</span><span class="sxs-lookup"><span data-stu-id="202c1-121">Retrieve and regenerate storage account access keys.</span></span>

<span data-ttu-id="202c1-122">Sehen Sie sich weiteren [Python-Beispielcode](https://azure.microsoft.com/resources/samples/?platform=python) an, den Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="202c1-122">Explore more [sample Python code](https://azure.microsoft.com/resources/samples/?platform=python) you can use in your apps.</span></span>