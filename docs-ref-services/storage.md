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
# <a name="azure-storage-libraries-for-python"></a>Azure Storage-Bibliotheken für Python

## <a name="overview"></a>Übersicht
- Mit [Azure Blob Storage](https://docs.microsoft.com/en-us/azure/storage/storage-python-how-to-use-blob-storage) können Sie Objekte und Dateien lesen und schreiben.
- Senden und Empfangen von Nachrichten zwischen Anwendungen mit Cloudverbindung per [Azure Queue Storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage)
- Lesen und Schreiben von großen strukturierten Datenmengen per [Azure Table Storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage) 
- Freigeben von Speicher zwischen Apps mit [Azure-Dateispeicher](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage)

Mit den Verwaltungsbibliotheken können Sie Azure Storage-Konten erstellen, aktualisieren und verwalten und Zugriffsschlüssel über Ihren Python-Code abfragen und neu generieren.

## <a name="install-the-libraries"></a>Installieren der Bibliotheken

### <a name="client"></a>Client-

```bash
pip install azure-storage
```

### <a name="management"></a>Verwaltung

```bash
pip install azure-mgmt-storage
```

## <a name="example"></a>Beispiel
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

## <a name="samples"></a>Beispiele

| | |
|--|--|
| [Erste Schritte mit Azure Blob Storage in Python](https://azure.microsoft.com/resources/samples/storage-blob-python-getting-started/) | Erstellen, Lesen, Aktualisieren, Beschränken des Zugriffs und Löschen von Dateien und Objekten in Azure Storage |
| [Erste Schritte mit Azure Queue Storage in Python](https://azure.microsoft.com/resources/samples/storage-queue-python-getting-started/) | Einfügen, Einsehen, Abrufen und Löschen von Nachrichten aus Azure Storage-Warteschlangen | 
| [Verwalten von Azure Storage-Konten](https://azure.microsoft.com/resources/samples/storage-python-manage) | Erstellen, Aktualisieren und Löschen von Speicherkonten Abrufen und erneutes Generieren von Speicherzugriffsschlüsseln

Sehen Sie sich weiteren [Python-Beispielcode](https://azure.microsoft.com/resources/samples/?platform=python) an, den Sie in Ihren Apps verwenden können.