---
title: "Azure-Bibliotheken für Python"
description: "Übersicht über die Azure-Verwaltungsbibliotheken und -Dienstbibliotheken für Python"
keywords: Azure, Python, SDK, API
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/01/2017
ms.topic: article
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.assetid: 
ms.openlocfilehash: 2b3e6d31edd7b946664853b3478e22205ab8c92e
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
---
# <a name="azure-libraries-for-python"></a>Azure-Bibliotheken für Python

Die Azure-Bibliotheken für Python ermöglichen Ihnen die Nutzung von Azure-Diensten und die Verwaltung von Azure-Ressourcen mithilfe Ihres Anwendungscodes. 

## <a name="manage-azure-resources"></a>Verwalten von Azure-Ressourcen

Erstellen und verwalten Sie Azure-Ressourcen in Ihren Python-Anwendungen mithilfe der Azure-Bibliotheken für Python.

Für die Erstellung einer SQL Server-Instanz können Sie beispielsweise den folgenden Code verwenden:

```python
sql_client = SqlManagementClient(
    credentials,
    subscription_id
)

server = sql_client.servers.create_or_update(
    'myresourcegroup',
    'myservername',
    {
        'location': 'eastus',
        'version': '12.0', # Required for create
        'administrator_login': 'mysecretname', # Required for create
        'administrator_login_password': 'HusH_Sec4et' # Required for create
    }
)
```

Eine vollständige Liste der Bibliotheken und Informationen zu ihrem Import in Ihre Projekte finden Sie in den [Installationsanweisungen](python-sdk-azure-install.md). Lesen Sie anschließend den [Artikel mit den ersten Schritten](python-sdk-azure-get-started.yml), um die Authentifizierung einzurichten und Beispielcode für Ihr eigenes Azure-Abonnement auszuführen.

## <a name="connect-to-azure-services"></a>Herstellen einer Verbindung mit Azure-Diensten

Mit Python-Bibliotheken können Sie nicht nur Ressourcen in Azure erstellen und verwalten, sondern diese auch in Ihren Apps verbinden und nutzen. Beispielsweise können Sie eine tabellarische SQL-Datenbank aktualisieren oder Dateien in Azure Storage speichern. Wählen Sie die für einen bestimmten Dienst erforderliche Bibliothek aus der vollständigen Liste der Bibliotheken aus, und sehen Sie sich im Python Developer Center Tutorials und Beispielcode zur Verwendung in Ihren Apps an.

Zum Hochladen einer einfachen HTML-Seite in einen Blob und zum Abrufen der URL verwenden Sie beispielsweise folgenden Code:

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

## <a name="sample-code-and-reference"></a>Beispielcode und Referenz
Die folgenden Beispiele behandeln allgemeine Automatisierungsaufgaben mit den Azure-Verwaltungsbibliotheken für Python und enthalten Code, der direkt in Ihren eigenen Apps verwendet werden kann:
- [Virtual Machines](python-sdk-azure-virtual-machine-samples.md)
- [Web-Apps](python-sdk-azure-web-apps-samples.md)
- [SQL-Datenbank](python-sdk-azure-sql-database-samples.md)

Sowohl in den Dienst- als auch den Verwaltungsbibliotheken ist eine [Referenz](/python/api/overview/azure) für alle Pakete verfügbar. Neue Funktionen, wichtige Änderungen und Migrationsanweisungen aus älteren Versionen finden Sie in den [Versionshinweisen](python-sdk-azure-release-notes.md). 

## <a name="get-help-and-give-feedback"></a>Hilfe und Feedback

Senden Sie Fragen an die [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-sdk-python)-Community, und öffnen Sie SDK-Probleme im [Projekt-GitHub](https://github.com/Azure/azure-sdk-for-python).
