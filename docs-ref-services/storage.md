---
title: Azure Storage-Bibliotheken für Python
description: ''
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
ms.openlocfilehash: e45b12af9e026e0f6390556813385d86784feaa4
ms.sourcegitcommit: 86f7f40295271ef94272642efb89b471aae99a2c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/18/2018
ms.locfileid: "35720061"
---
# <a name="azure-storage-libraries-for-python"></a><span data-ttu-id="bbc47-103">Azure Storage-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="bbc47-103">Azure Storage libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="bbc47-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="bbc47-104">Overview</span></span>
- <span data-ttu-id="bbc47-105">Mit [Azure Blob Storage](https://docs.microsoft.com/en-us/azure/storage/storage-python-how-to-use-blob-storage) können Sie Objekte und Dateien lesen und schreiben.</span><span class="sxs-lookup"><span data-stu-id="bbc47-105">Read and write objects and files from [Azure Blob storage](https://docs.microsoft.com/en-us/azure/storage/storage-python-how-to-use-blob-storage)</span></span>
- <span data-ttu-id="bbc47-106">Senden und Empfangen von Nachrichten zwischen Anwendungen mit Cloudverbindung per [Azure Queue Storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage)</span><span class="sxs-lookup"><span data-stu-id="bbc47-106">Send and receive messages between cloud-connected applications with [Azure Queue storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage)</span></span>
- <span data-ttu-id="bbc47-107">Lesen und Schreiben von großen strukturierten Datenmengen per [Azure Table Storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage)</span><span class="sxs-lookup"><span data-stu-id="bbc47-107">Read and write large structured data with [Azure Table storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage)</span></span> 
- <span data-ttu-id="bbc47-108">Freigeben von Speicher zwischen Apps mit [Azure-Dateispeicher](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage)</span><span class="sxs-lookup"><span data-stu-id="bbc47-108">Share storage between apps with [Azure File storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage)</span></span>

<span data-ttu-id="bbc47-109">Mit den Verwaltungsbibliotheken können Sie Azure Storage-Konten erstellen, aktualisieren und verwalten und Zugriffsschlüssel über Ihren Python-Code abfragen und neu generieren.</span><span class="sxs-lookup"><span data-stu-id="bbc47-109">Create, update, and manage Azure Storage accounts and query and regenerate access keys from your Python code with the management libraries.</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="bbc47-110">Installieren der Bibliotheken</span><span class="sxs-lookup"><span data-stu-id="bbc47-110">Install the libraries</span></span>

### <a name="client"></a><span data-ttu-id="bbc47-111">Client</span><span class="sxs-lookup"><span data-stu-id="bbc47-111">Client</span></span>

<span data-ttu-id="bbc47-112">Azure Storage-Clientbibliotheken bestehen aus vier Paketen: Blob, Datei, Warteschlange und Tabelle.</span><span class="sxs-lookup"><span data-stu-id="bbc47-112">Azure Storage Client Libraries consist of 4 packages: Blob, File, Queue and Table.</span></span> <span data-ttu-id="bbc47-113">Führen Sie zum Installieren der Blobpakets Folgendes aus:</span><span class="sxs-lookup"><span data-stu-id="bbc47-113">To install the blob package, run:</span></span>

```bash
pip install azure-storage-blob
```

### <a name="management"></a><span data-ttu-id="bbc47-114">Verwaltung</span><span class="sxs-lookup"><span data-stu-id="bbc47-114">Management</span></span>

```bash
pip install azure-mgmt-storage
```

## <a name="example"></a><span data-ttu-id="bbc47-115">Beispiel</span><span class="sxs-lookup"><span data-stu-id="bbc47-115">Example</span></span>
```python
from azure.storage.blob import BlockBlobService

blob_service = BlockBlobService(account_name, account_key)

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

## <a name="samples"></a><span data-ttu-id="bbc47-116">Beispiele</span><span class="sxs-lookup"><span data-stu-id="bbc47-116">Samples</span></span>

| | |
|--|--|
| [<span data-ttu-id="bbc47-117">Erste Schritte mit Azure Blob Storage in Python</span><span class="sxs-lookup"><span data-stu-id="bbc47-117">Get started with Azure Blob Storage in Python</span></span>](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-python-how-to-use-blob-storage) | <span data-ttu-id="bbc47-118">Erstellen, Lesen, Aktualisieren, Beschränken des Zugriffs und Löschen von Dateien und Objekten in Azure Storage</span><span class="sxs-lookup"><span data-stu-id="bbc47-118">Create, read, update, restrict access, and delete files and objects in Azure Storage.</span></span> |
| [<span data-ttu-id="bbc47-119">Erste Schritte mit Azure Queue Storage in Python</span><span class="sxs-lookup"><span data-stu-id="bbc47-119">Get started with Azure Queue Storage in Python</span></span>](https://docs.microsoft.com/en-us/azure/storage/queues/storage-python-how-to-use-queue-storage) | <span data-ttu-id="bbc47-120">Einfügen, Einsehen, Abrufen und Löschen von Nachrichten aus Azure Storage-Warteschlangen</span><span class="sxs-lookup"><span data-stu-id="bbc47-120">Insert, peek, retrieve and delete messages from Azure Storage queues.</span></span> | 
| [<span data-ttu-id="bbc47-121">Verwalten von Azure Storage-Konten</span><span class="sxs-lookup"><span data-stu-id="bbc47-121">Manage Azure Storage accounts</span></span>](https://azure.microsoft.com/resources/samples/storage-python-manage) | <span data-ttu-id="bbc47-122">Erstellen, Aktualisieren und Löschen von Speicherkonten</span><span class="sxs-lookup"><span data-stu-id="bbc47-122">Create, update , and delete storage accounts.</span></span> <span data-ttu-id="bbc47-123">Abrufen und erneutes Generieren von Speicherzugriffsschlüsseln</span><span class="sxs-lookup"><span data-stu-id="bbc47-123">Retrieve and regenerate storage account access keys.</span></span>

<span data-ttu-id="bbc47-124">Sehen Sie sich weiteren [Python-Beispielcode](https://azure.microsoft.com/resources/samples/?platform=python) an, den Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="bbc47-124">Explore more [sample Python code](https://azure.microsoft.com/resources/samples/?platform=python) you can use in your apps.</span></span>
