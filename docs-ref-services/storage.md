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
# <a name="azure-storage-libraries-for-python"></a>Azure Storage-Bibliotheken für Python

## <a name="overview"></a>Übersicht
- Mit [Azure Blob Storage](https://docs.microsoft.com/en-us/azure/storage/storage-python-how-to-use-blob-storage) können Sie Objekte und Dateien lesen und schreiben.
- Senden und Empfangen von Nachrichten zwischen Anwendungen mit Cloudverbindung per [Azure Queue Storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage)
- Lesen und Schreiben von großen strukturierten Datenmengen per [Azure Table Storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage) 
- Freigeben von Speicher zwischen Apps mit [Azure-Dateispeicher](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage)

Mit den Verwaltungsbibliotheken können Sie Azure Storage-Konten erstellen, aktualisieren und verwalten und Zugriffsschlüssel über Ihren Python-Code abfragen und neu generieren.

## <a name="install-the-libraries"></a>Installieren der Bibliotheken

### <a name="client"></a>Client

Azure Storage-Clientbibliotheken bestehen aus vier Paketen: Blob, Datei, Warteschlange und Tabelle. Führen Sie zum Installieren der Blobpakets Folgendes aus:

```bash
pip install azure-storage-blob
```

### <a name="management"></a>Verwaltung

```bash
pip install azure-mgmt-storage
```

## <a name="example"></a>Beispiel
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

## <a name="samples"></a>Beispiele

| | |
|--|--|
| [Erste Schritte mit Azure Blob Storage in Python](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-python-how-to-use-blob-storage) | Erstellen, Lesen, Aktualisieren, Beschränken des Zugriffs und Löschen von Dateien und Objekten in Azure Storage |
| [Erste Schritte mit Azure Queue Storage in Python](https://docs.microsoft.com/en-us/azure/storage/queues/storage-python-how-to-use-queue-storage) | Einfügen, Einsehen, Abrufen und Löschen von Nachrichten aus Azure Storage-Warteschlangen | 
| [Verwalten von Azure Storage-Konten](https://azure.microsoft.com/resources/samples/storage-python-manage) | Erstellen, Aktualisieren und Löschen von Speicherkonten Abrufen und erneutes Generieren von Speicherzugriffsschlüsseln

Sehen Sie sich weiteren [Python-Beispielcode](https://azure.microsoft.com/resources/samples/?platform=python) an, den Sie in Ihren Apps verwenden können.
