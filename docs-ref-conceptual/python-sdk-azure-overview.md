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
ms.openlocfilehash: 7c069f849007ea2c02cf4347ce213dd033dcd68b
ms.sourcegitcommit: c57305dad01cad925faf50a64953c408429d4ca9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="azure-libraries-for-python"></a><span data-ttu-id="44f47-104">Azure-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="44f47-104">Azure libraries for Python</span></span>

<span data-ttu-id="44f47-105">Die Azure-Bibliotheken für Python ermöglichen Ihnen die Nutzung von Azure-Diensten und die Verwaltung von Azure-Ressourcen mithilfe Ihres Anwendungscodes.</span><span class="sxs-lookup"><span data-stu-id="44f47-105">The Azure libraries for Python let you use Azure services and manage Azure resources from your application code.</span></span> <span data-ttu-id="44f47-106">Die Bibliotheken stehen in [PyPI](python-sdk-azure-install.md) für die Verwendung in Ihren Python-Projekten zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="44f47-106">The libraries are available in [PyPI](python-sdk-azure-install.md) for use in your Python projects.</span></span>

## <a name="manage-azure-resources"></a><span data-ttu-id="44f47-107">Verwalten von Azure-Ressourcen</span><span class="sxs-lookup"><span data-stu-id="44f47-107">Manage Azure resources</span></span>

<span data-ttu-id="44f47-108">Erstellen und verwalten Sie Azure-Ressourcen in Ihren Python-Anwendungen mithilfe der Azure-Bibliotheken für Python.</span><span class="sxs-lookup"><span data-stu-id="44f47-108">Create and manage Azure resources from Python applications using the Azure libraries for Python.</span></span>

<span data-ttu-id="44f47-109">Für die Erstellung einer SQL Server-Instanz können Sie beispielsweise den folgenden Code verwenden:</span><span class="sxs-lookup"><span data-stu-id="44f47-109">For example, to create a SQL Server instance, you can use the following code:</span></span>

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

<span data-ttu-id="44f47-110">Eine vollständige Liste der Bibliotheken und Informationen zu ihrem Import in Ihre Projekte finden Sie in den [Installationsanweisungen](python-sdk-azure-install.md). Lesen Sie anschließend den [Artikel mit den ersten Schritten](python-sdk-azure-get-started.yml), um die Authentifizierung einzurichten und Beispielcode für Ihr eigenes Azure-Abonnement auszuführen.</span><span class="sxs-lookup"><span data-stu-id="44f47-110">Review the [install instructions](python-sdk-azure-install.md) for a full list of the libraries and how to import them into your projects and then read the [get started article](python-sdk-azure-get-started.yml) to set up your authentication and run sample code against your own Azure subscription.</span></span>

## <a name="connect-to-azure-services"></a><span data-ttu-id="44f47-111">Herstellen einer Verbindung mit Azure-Diensten</span><span class="sxs-lookup"><span data-stu-id="44f47-111">Connect to Azure services</span></span>

<span data-ttu-id="44f47-112">Mit Python-Bibliotheken können Sie nicht nur Ressourcen in Azure erstellen und verwalten, sondern diese auch in Ihren Apps verbinden und nutzen.</span><span class="sxs-lookup"><span data-stu-id="44f47-112">In addition to using Python libraries to create and manage resources within Azure, you can also use Python libraries to connect and use those resources in your apps.</span></span> <span data-ttu-id="44f47-113">Beispielsweise können Sie eine tabellarische SQL-Datenbank aktualisieren oder Dateien in Azure Storage speichern.</span><span class="sxs-lookup"><span data-stu-id="44f47-113">For example, you might update a table SQL Database or store files in Azure Storage.</span></span> <span data-ttu-id="44f47-114">Wählen Sie die für einen bestimmten Dienst erforderliche Bibliothek aus der vollständigen Liste der Bibliotheken aus, und sehen Sie sich im Python Developer Center Tutorials und Beispielcode zur Verwendung in Ihren Apps an.</span><span class="sxs-lookup"><span data-stu-id="44f47-114">Select the library you need for a particular service from the complete list of libraries and visit the Python developer center for tutorials and sample code for help using them in your apps.</span></span>

<span data-ttu-id="44f47-115">Zum Hochladen einer einfachen HTML-Seite in einen Blob und zum Abrufen der URL verwenden Sie beispielsweise folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="44f47-115">For example, to upload a simple HTML page on a blob and get the Url:</span></span>

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

## <a name="sample-code-and-reference"></a><span data-ttu-id="44f47-116">Beispielcode und Referenz</span><span class="sxs-lookup"><span data-stu-id="44f47-116">Sample code and reference</span></span>
<span data-ttu-id="44f47-117">Die folgenden Beispiele behandeln allgemeine Automatisierungsaufgaben mit den Azure-Verwaltungsbibliotheken für Python und enthalten Code, der direkt in Ihren eigenen Apps verwendet werden kann:</span><span class="sxs-lookup"><span data-stu-id="44f47-117">The following samples cover common automation tasks with the Azure management libraries for Python and have code ready to use in your own apps:</span></span>
- [<span data-ttu-id="44f47-118">Virtuelle Computer</span><span class="sxs-lookup"><span data-stu-id="44f47-118">Virtual Machines</span></span>](python-sdk-azure-virtual-machine-samples.md)
- [<span data-ttu-id="44f47-119">Web-Apps</span><span class="sxs-lookup"><span data-stu-id="44f47-119">Web apps</span></span>](python-sdk-azure-web-apps-samples.md)
- [<span data-ttu-id="44f47-120">SQL-Datenbank</span><span class="sxs-lookup"><span data-stu-id="44f47-120">SQL Database</span></span>](python-sdk-azure-sql-database-samples.md)

<span data-ttu-id="44f47-121">Sowohl in den Dienst- als auch den Verwaltungsbibliotheken ist eine [Referenz](/python/api/overview/azure) für alle Pakete verfügbar.</span><span class="sxs-lookup"><span data-stu-id="44f47-121">A [reference](/python/api/overview/azure) is available for all packages in both the service an management libraries.</span></span> <span data-ttu-id="44f47-122">Neue Funktionen, wichtige Änderungen und Migrationsanweisungen aus älteren Versionen finden Sie in den [Versionshinweisen](python-sdk-azure-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="44f47-122">New features, breaking changes, and migration instructions from previous versions are available in the [release notes](python-sdk-azure-release-notes.md).</span></span> 

## <a name="get-help-and-give-feedback"></a><span data-ttu-id="44f47-123">Hilfe und Feedback</span><span class="sxs-lookup"><span data-stu-id="44f47-123">Get help and give feedback</span></span>

<span data-ttu-id="44f47-124">Senden Sie Fragen an die [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-sdk-python)-Community, und öffnen Sie SDK-Probleme im [Projekt-GitHub](https://github.com/Azure/azure-sdk-for-python).</span><span class="sxs-lookup"><span data-stu-id="44f47-124">Post questions to the community on [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-sdk-python) and open issues against the SDK on the [project GitHub](https://github.com/Azure/azure-sdk-for-python).</span></span>
