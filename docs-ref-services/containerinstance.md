---
title: Azure Container Instances-Bibliotheken für Python
description: Referenz zu Azure Container Instances-Bibliotheken für Python
keywords: Azure, Python, SDK, API, Container, Instances
author: mmacy
manager: jeconnoc
ms.date: 06/04/2018
ms.author: marsma
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: container-instances
ms.openlocfilehash: 09f39375e0e92b6d09a965c3972d772a1437d0d4
ms.sourcegitcommit: 8c70bfd95309c3a77a4c0f73373c1785d59cdd10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/05/2018
ms.locfileid: "34761324"
---
# <a name="azure-container-instances-libraries-for-python"></a><span data-ttu-id="2b3b9-104">Azure Container Instances-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="2b3b9-104">Azure Container Instances libraries for Python</span></span>

<span data-ttu-id="2b3b9-105">Verwenden Sie die Azure Container Instances-Bibliotheken für Python zum Erstellen und Verwalten von Azure-Containerinstanzen.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-105">Use the Microsoft Azure Container Instances libraries for Python to create and manage Azure container instances.</span></span> <span data-ttu-id="2b3b9-106">In der [Übersicht über Azure Container Instances](/azure/container-instances/container-instances-overview) erfahren Sie mehr.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-106">Learn more by reading the [Azure Container Instances overview](/azure/container-instances/container-instances-overview).</span></span>

## <a name="management-apis"></a><span data-ttu-id="2b3b9-107">Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="2b3b9-107">Management APIs</span></span>

<span data-ttu-id="2b3b9-108">Verwenden Sie die Verwaltungsbibliothek zum Erstellen und Verwalten von Azure-Containerinstanzen in Azure.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-108">Use the management library to create and manage Azure container instances in Azure.</span></span>

<span data-ttu-id="2b3b9-109">Installieren Sie das Verwaltungspaket über pip:</span><span class="sxs-lookup"><span data-stu-id="2b3b9-109">Install the management package via pip:</span></span>

```bash
pip install azure-mgmt-containerinstance
```

## <a name="example-source"></a><span data-ttu-id="2b3b9-110">Beispielquelle</span><span class="sxs-lookup"><span data-stu-id="2b3b9-110">Example source</span></span>

<span data-ttu-id="2b3b9-111">Wenn Sie die folgenden Codebeispiele im Kontext sehen möchten, finden Sie sie im folgenden GitHub-Repository:</span><span class="sxs-lookup"><span data-stu-id="2b3b9-111">If you'd like to see the following code examples in context, you can find them in the following GitHub repository:</span></span>

[<span data-ttu-id="2b3b9-112">Azure-Samples/aci-docs-sample-python</span><span class="sxs-lookup"><span data-stu-id="2b3b9-112">Azure-Samples/aci-docs-sample-python</span></span>](https://github.com/Azure-Samples/aci-docs-sample-python)

## <a name="authentication"></a><span data-ttu-id="2b3b9-113">Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="2b3b9-113">Authentication</span></span>

<span data-ttu-id="2b3b9-114">Am einfachsten werden SDK-Clients (etwa der Azure Container Instances- und der Resource Manager-Client im folgenden Beispiel) mit der [dateibasierten Authentifizierung](/python/azure/python-sdk-azure-authenticate#mgmt-auth-file) authentifiziert.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-114">One of the easiest ways to authenticate SDK clients (like the Azure Container Instances and Resource Manager clients in the following example) is with [file-based authentication](/python/azure/python-sdk-azure-authenticate#mgmt-auth-file).</span></span> <span data-ttu-id="2b3b9-115">Bei der dateibasierten Authentifizierung wird die Umgebungsvariable `AZURE_AUTH_LOCATION` für den Pfad zu einer Datei mit Anmeldeinformationen abgefragt.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-115">File-based authentication queries the `AZURE_AUTH_LOCATION` environment variable for the path to a credentials file.</span></span> <span data-ttu-id="2b3b9-116">So verwenden Sie die dateibasierte Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="2b3b9-116">To use file-based authentication:</span></span>

1. <span data-ttu-id="2b3b9-117">Erstellen Sie mit der [Azure CLI](/cli/azure) oder mit [Cloud Shell](https://shell.azure.com/) eine Datei mit Anmeldeinformationen:</span><span class="sxs-lookup"><span data-stu-id="2b3b9-117">Create a credentials file with the [Azure CLI](/cli/azure) or [Cloud Shell](https://shell.azure.com/):</span></span>

   `az ad sp create-for-rbac --sdk-auth > my.azureauth`

   <span data-ttu-id="2b3b9-118">Wenn Sie [Cloud Shell](https://shell.azure.com/) zum Erstellen der Datei mit Anmeldeinformationen verwenden, kopieren Sie ihren Inhalt in eine lokale Datei, auf die die Python-Anwendung zugreifen kann.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-118">If you use the [Cloud Shell](https://shell.azure.com/) to generate the credentials file, copy its contents into a local file that your Python application can access.</span></span>

2. <span data-ttu-id="2b3b9-119">Legen Sie die Umgebungsvariable `AZURE_AUTH_LOCATION` auf den vollständigen Pfad der erstellten Datei mit Anmeldeinformationen fest.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-119">Set the `AZURE_AUTH_LOCATION` environment variable to the full path of the generated credentials file.</span></span> <span data-ttu-id="2b3b9-120">Beispiel (in Bash):</span><span class="sxs-lookup"><span data-stu-id="2b3b9-120">For example (in Bash):</span></span>

   ```bash
   export AZURE_AUTH_LOCATION=/home/yourusername/my.azureauth
   ```

<span data-ttu-id="2b3b9-121">Nachdem Sie die Datei mit Anmeldeinformationen erstellt und die Umgebungsvariable `AZURE_AUTH_LOCATION` aufgefüllt haben, initialisieren Sie mit der Methode `get_client_from_auth_file` des [client_factory][client_factory]-Moduls die Objekte [ResourceManagementClient][ResourceManagementClient] und [ContainerInstanceManagementClient][ContainerInstanceManagementClient].</span><span class="sxs-lookup"><span data-stu-id="2b3b9-121">Once you've created the credentials file and populated the `AZURE_AUTH_LOCATION` environment variable, use the `get_client_from_auth_file` method of the [client_factory][client_factory] module to initialize the [ResourceManagementClient][ResourceManagementClient] and [ContainerInstanceManagementClient][ContainerInstanceManagementClient] objects.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[authenticate](~/aci-docs-sample-python/src/aci_docs_sample.py#L45-L58 "Authenticate ACI and Resource Manager clients")]

<span data-ttu-id="2b3b9-122">Weitere Informationen zu den verfügbaren Authentifizierungsmethoden in den Python-Verwaltungsbibliotheken für Azure finden Sie unter [Authentifizieren bei den Azure-Verwaltungsbibliotheken für Python](/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="2b3b9-122">For more details about the available authentication methods in the Python management libraries for Azure, see [Authenticate with the Azure Management Libraries for Python](/python/azure/python-sdk-azure-authenticate).</span></span>

## <a name="create-container-group---single-container"></a><span data-ttu-id="2b3b9-123">Erstellen einer Containergruppe – einzelner Container</span><span class="sxs-lookup"><span data-stu-id="2b3b9-123">Create container group - single container</span></span>

<span data-ttu-id="2b3b9-124">In diesem Beispiel wird eine Containergruppe mit einem einzelnen Container erstellt.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-124">This example creates a container group with a single container</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L94-L140 "Create single-container group")]

## <a name="create-container-group---multiple-containers"></a><span data-ttu-id="2b3b9-125">Erstellen einer Containergruppe – mehrere Container</span><span class="sxs-lookup"><span data-stu-id="2b3b9-125">Create container group - multiple containers</span></span>

<span data-ttu-id="2b3b9-126">In diesem Beispiel wird eine Containergruppe mit zwei Containern erstellt: einem Anwendungscontainer und einem Sidecar-Container.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-126">This example creates a container group with two containers: an application container and a sidecar container.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group_multi](~/aci-docs-sample-python/src/aci_docs_sample.py#L143-L196 "Create multi-container group")]

## <a name="create-task-based-container-group"></a><span data-ttu-id="2b3b9-127">Erstellen einer aufgabenbasierten Containergruppe</span><span class="sxs-lookup"><span data-stu-id="2b3b9-127">Create task-based container group</span></span>

<span data-ttu-id="2b3b9-128">In diesem Beispiel wird eine Containergruppe mit einem einzelnen aufgabenbasierten Container erstellt.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-128">This example creates a container group with a single task-based container.</span></span> <span data-ttu-id="2b3b9-129">In diesem Beispiel werden mehrere Funktionen veranschaulicht:</span><span class="sxs-lookup"><span data-stu-id="2b3b9-129">This example demonstrates several features:</span></span>

* <span data-ttu-id="2b3b9-130">[Außerkraftsetzung der Befehlszeile:](/azure/container-instances/container-instances-restart-policy#command-line-override) Es wird eine andere benutzerdefinierte Befehlszeile angegeben als die, die in der Zeile `CMD` der Dockerfile-Datei des Containers angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-130">[Command line override](/azure/container-instances/container-instances-restart-policy#command-line-override) - A custom command line, different from that which is specified in the container's Dockerfile `CMD` line, is specified.</span></span> <span data-ttu-id="2b3b9-131">Die Außerkraftsetzung der Befehlszeile ermöglicht Ihnen die Angabe einer benutzerdefinierten Befehlszeile zur Ausführung beim Containerstart. Dabei wird die in den Container integrierte Standardbefehlszeile außer Kraft gesetzt.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-131">Command line override allows you to specify a custom command line to execute at container startup, overriding the default command line baked-in to the container.</span></span> <span data-ttu-id="2b3b9-132">Für die Ausführung mehrerer Befehle beim Containerstart gilt Folgendes:</span><span class="sxs-lookup"><span data-stu-id="2b3b9-132">Regarding executing multiple commands at container startup, the following applies:</span></span>

   <span data-ttu-id="2b3b9-133">Wenn Sie einen **einzelnen Befehl** mit mehreren Befehlszeilenargumenten ausführen möchten, z.B. `echo FOO BAR`, müssen Sie sie als Zeichenfolgenliste für die `command`-Eigenschaft des [Containers][Container] angeben.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-133">If you want to run a **single command** with several command-line arguments, for example `echo FOO BAR`, you must supply them as a string list to the `command` property of the [Container][Container].</span></span> <span data-ttu-id="2b3b9-134">Beispiel: </span><span class="sxs-lookup"><span data-stu-id="2b3b9-134">For example:</span></span>

   `command = ['echo', 'FOO', 'BAR']`

   <span data-ttu-id="2b3b9-135">Wenn Sie jedoch **mehrere Befehle** mit (potenziell) mehreren Argumente ausführen möchten, müssen Sie eine Shell ausführen und die verketteten Befehle als Argument übergeben.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-135">If, however, you want to run **multiple commands** with (potentially) multiple arguments, you must execute a shell and pass the chained commands as an argument.</span></span> <span data-ttu-id="2b3b9-136">Hiermit wird beispielsweise ein `echo`- sowie ein `tail`-Befehl ausgeführt:</span><span class="sxs-lookup"><span data-stu-id="2b3b9-136">For example, this executes both an `echo` and a `tail` command:</span></span>

   `command = ['/bin/sh', '-c', 'echo FOO BAR && tail -f /dev/null']`
* <span data-ttu-id="2b3b9-137">[Umgebungsvariablen:](/azure/container-instances/container-instances-environment-variables) Zwei Umgebungsvariablen werden für den Container in der Containergruppe angegeben.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-137">[Environment variables](/azure/container-instances/container-instances-environment-variables) - Two environment variables are specified for the container in the container group.</span></span> <span data-ttu-id="2b3b9-138">Verwenden Sie Umgebungsvariablen, um das Skript- oder Anwendungsverhalten zur Laufzeit zu ändern oder dynamische Informationen an eine im Container ausgeführte Anwendung zu übergeben.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-138">Use environment variables to modify script or application behavior at runtime, or otherwise pass dynamic information to an application running in the container.</span></span>
* <span data-ttu-id="2b3b9-139">[Neustartrichtlinie:](/azure/container-instances/container-instances-restart-policy) Der Container wird mit der Neustartrichtlinie „Nie“ konfiguriert. Dies ist nützlich für aufgabenbasierte Container, die als Teil eines Batchauftrags ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-139">[Restart policy](/azure/container-instances/container-instances-restart-policy) - The container is configured with a restart policy of "Never," useful for task-based containers that are executed as part of a batch job.</span></span>
* <span data-ttu-id="2b3b9-140">Vorgangsabruf mit [AzureOperationPoller][AzureOperationPoller]: Nach dem Aufrufen der Create-Methode wird der Vorgang abgerufen, um zu ermitteln, wann er abgeschlossen wurde und wann die Protokolle der Containergruppe abgerufen werden können.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-140">Operation polling with [AzureOperationPoller][AzureOperationPoller] - After the create method is invoked, the operation is polled to determine when it has completed and the container group's logs can be obtained.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group_task](~/aci-docs-sample-python/src/aci_docs_sample.py#L199-L275 "Run a task-based container")]

## <a name="list-container-groups"></a><span data-ttu-id="2b3b9-141">Auflisten von Containergruppen</span><span class="sxs-lookup"><span data-stu-id="2b3b9-141">List container groups</span></span>

<span data-ttu-id="2b3b9-142">In diesem Beispiel werden die Containergruppen in einer Ressourcengruppe aufgelistet und dann einige ihrer Eigenschaften zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-142">This example lists the container groups in a resource group and then prints a few of their properties.</span></span>

<span data-ttu-id="2b3b9-143">Beim Auflisten der Containergruppen ist für [instance_view][instance_view] jeder zurückgegebenen Gruppe `None` angegeben.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-143">When you list container groups,the [instance_view][instance_view] of each returned group is `None`.</span></span> <span data-ttu-id="2b3b9-144">Um die Details der Containers in einer Containergruppe zu erhalten, müssen Sie dann die Containergruppe [abrufen][containergroupoperations_get]. Dabei wird die Gruppe mit aufgefüllter `instance_view`-Eigenschaft zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-144">To get the details of the containers within a container group, you must then [get][containergroupoperations_get] the container group, which returns the group with its `instance_view` property populated.</span></span> <span data-ttu-id="2b3b9-145">Der nächste Abschnitt ([Abrufen einer vorhandenen Containergruppe](#get-an-existing-container-group)) enthält ein Beispiel zum Durchlaufen der Container einer Containergruppe in `instance_view`.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-145">See the next section, [Get an existing container group](#get-an-existing-container-group), for an example of iterating over a container group's containers in its `instance_view`.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[list_container_groups](~/aci-docs-sample-python/src/aci_docs_sample.py#L278-L292 "List container groups")]

## <a name="get-an-existing-container-group"></a><span data-ttu-id="2b3b9-146">Abrufen einer vorhandenen Containergruppe</span><span class="sxs-lookup"><span data-stu-id="2b3b9-146">Get an existing container group</span></span>

<span data-ttu-id="2b3b9-147">In diesem Beispiel wird eine bestimmte Containergruppe aus einer Ressourcengruppe abgerufen. Dann werden einige ihrer Eigenschaften (einschließlich der Container) und deren Werte ausgegeben.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-147">This example gets a specific container group from a resource group, and then prints a few of its properties (including its containers) and their values.</span></span>

<span data-ttu-id="2b3b9-148">Der [GET-Vorgang][containergroupoperations_get] gibt eine Containergruppe mit aufgefülltem [instance_view][instance_view]-Objekt zurück, wodurch das Durchlaufen der einzelnen Container in der Gruppe ermöglicht wird.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-148">The [get operation][containergroupoperations_get] returns a container group with its [instance_view][instance_view] populated, which allows you to iterate over each container in the group.</span></span> <span data-ttu-id="2b3b9-149">Nur der `get`-Vorgang füllt die Eigenschaft `instance_vew` der Containergruppe auf. Durch das Auflisten der Containergruppen in einem Abonnement oder einer Ressourcengruppe wird die Instanzenansicht nicht aufgefüllt, da der Vorgang unter Umständen kostspielig sein kann (beispielsweise beim Auflisten Hunderter Containergruppen, die wiederum unter Umständen mehrere Container enthalten).</span><span class="sxs-lookup"><span data-stu-id="2b3b9-149">Only the `get` operation populates the `instance_vew` property of the container group--listing the container groups in a subscription or resource group doesn't populate the instance view due to the potentially expensive nature of the operation (for example, when listing hundreds of container groups, each potentially containing multiple containers).</span></span> <span data-ttu-id="2b3b9-150">Wie bereits im Abschnitt [Auflisten von Containergruppen](#list-container-groups) erwähnt müssen Sie nach einem `list`-Vorgang einen `get`-Vorgang für eine bestimmte Containergruppe ausführen, um ihre Containerinstanzdetails abzurufen.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-150">As mentioned previously in the [List container groups](#list-container-groups) section, after a `list`, you must subsequently `get` a specific container group to obtain its container instance details.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[get_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L295-L324 "Get container group")]

## <a name="delete-a-container-group"></a><span data-ttu-id="2b3b9-151">Löschen einer Containergruppe</span><span class="sxs-lookup"><span data-stu-id="2b3b9-151">Delete a container group</span></span>

<span data-ttu-id="2b3b9-152">Dieses Beispiel löscht mehrere Containergruppen aus einer Ressourcengruppe sowie die Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-152">This example deletes several container groups from a resource group, as well as the resource group.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[delete_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L83-L91 "Delete container groups and resource group")]

## <a name="next-steps"></a><span data-ttu-id="2b3b9-153">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="2b3b9-153">Next steps</span></span>

* <span data-ttu-id="2b3b9-154">Der Quellcode für die vorhergehenden Beispiele ist auf GitHub zu finden:</span><span class="sxs-lookup"><span data-stu-id="2b3b9-154">The source code for the preceding examples can be found on GitHub:</span></span>

  <span data-ttu-id="2b3b9-155">[Azure-Samples/aci-docs-sample-python][aci-docs-sample-python]</span><span class="sxs-lookup"><span data-stu-id="2b3b9-155">[Azure-Samples/aci-docs-sample-python][aci-docs-sample-python]</span></span>

* <span data-ttu-id="2b3b9-156">Weitere Azure Container Instances-Codebeispiele:</span><span class="sxs-lookup"><span data-stu-id="2b3b9-156">More Azure Container Instances code samples:</span></span>

  <span data-ttu-id="2b3b9-157">[Azure-Codebeispiele][samples-aci]</span><span class="sxs-lookup"><span data-stu-id="2b3b9-157">[Azure Code Samples][samples-aci]</span></span>

* <span data-ttu-id="2b3b9-158">Sehen Sie sich weiteren [Python-Beispielcode][samples-python] an, den Sie in Ihren Apps verwenden können.</span><span class="sxs-lookup"><span data-stu-id="2b3b9-158">Explore more [sample Python code][samples-python] you can use in your apps.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2b3b9-159">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="2b3b9-159">Explore the management APIs</span></span>](/python/api/overview/azure/containerinstance/management)

<!-- LINKS - External -->
[aci-docs-sample-python]: https://github.com/Azure-Samples/aci-docs-sample-python
[samples-aci]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[samples-python]: https://azure.microsoft.com/resources/samples/?platform=python

<!-- TYPES -->
[AzureOperationPoller]: /python/api/msrestazure.azure_operation.AzureOperationPoller
[client_factory]: /python/api/azure.common.client_factory
[Container]: /python/api/azure.mgmt.containerinstance.models.container
[ContainerGroupInstanceView]: /python/api/azure.mgmt.containerinstance.models.containergrouppropertiesinstanceview
[containergroupoperations_get]: /python/api/azure.mgmt.containerinstance.operations.containergroupsoperations#get
[ContainerInstanceManagementClient]: /python/api/azure.mgmt.containerinstance.containerinstancemanagementclient
[instance_view]: /python/api/azure.mgmt.containerinstance.models.containergroup#variables
[ResourceManagementClient]: /python/api/azure.mgmt.resource.resources.resourcemanagementclient