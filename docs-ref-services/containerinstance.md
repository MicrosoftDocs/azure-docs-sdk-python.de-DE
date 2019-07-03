---
title: Azure Container Instances-Bibliotheken für Python
description: Referenz zu Azure Container Instances-Bibliotheken für Python
keywords: Azure, Python, SDK, API, Container, Instances
author: dlepow
manager: jeconnoc
ms.date: 04/15/2019
ms.author: danlep
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: container-instances
ms.openlocfilehash: 19e0e629253462f77d58740857b853d1c94d53cf
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534321"
---
# <a name="azure-container-instances-libraries-for-python"></a>Azure Container Instances-Bibliotheken für Python

Verwenden Sie die Azure Container Instances-Bibliotheken für Python zum Erstellen und Verwalten von Azure-Containerinstanzen. In der [Übersicht über Azure Container Instances](/azure/container-instances/container-instances-overview) erfahren Sie mehr.

## <a name="management-apis"></a>Verwaltungs-APIs

Verwenden Sie die Verwaltungsbibliothek zum Erstellen und Verwalten von Azure-Containerinstanzen in Azure.

Installieren Sie das Verwaltungspaket über pip:

```bash
pip install azure-mgmt-containerinstance
```

## <a name="example-source"></a>Beispielquelle

Wenn Sie die folgenden Codebeispiele im Kontext sehen möchten, finden Sie sie im folgenden GitHub-Repository:

[Azure-Samples/aci-docs-sample-python](https://github.com/Azure-Samples/aci-docs-sample-python)

## <a name="authentication"></a>Authentication

Am einfachsten werden SDK-Clients (etwa der Azure Container Instances- und der Resource Manager-Client im folgenden Beispiel) mit der [dateibasierten Authentifizierung](/python/azure/python-sdk-azure-authenticate#mgmt-auth-file) authentifiziert. Bei der dateibasierten Authentifizierung wird die Umgebungsvariable `AZURE_AUTH_LOCATION` für den Pfad zu einer Datei mit Anmeldeinformationen abgefragt. So verwenden Sie die dateibasierte Authentifizierung

1. Erstellen Sie mit der [Azure CLI](/cli/azure) oder mit [Cloud Shell](https://shell.azure.com/) eine Datei mit Anmeldeinformationen:

   `az ad sp create-for-rbac --sdk-auth > my.azureauth`

   Wenn Sie [Cloud Shell](https://shell.azure.com/) zum Erstellen der Datei mit Anmeldeinformationen verwenden, kopieren Sie ihren Inhalt in eine lokale Datei, auf die die Python-Anwendung zugreifen kann.

2. Legen Sie die Umgebungsvariable `AZURE_AUTH_LOCATION` auf den vollständigen Pfad der erstellten Datei mit Anmeldeinformationen fest. Beispiel (in Bash):

   ```bash
   export AZURE_AUTH_LOCATION=/home/yourusername/my.azureauth
   ```

Nachdem Sie die Datei mit Anmeldeinformationen erstellt und die Umgebungsvariable `AZURE_AUTH_LOCATION` aufgefüllt haben, initialisieren Sie mit der Methode `get_client_from_auth_file` des [client_factory][client_factory]-Moduls die Objekte module to initialize the [ResourceManagementClient][ResourceManagementClient] und [ContainerInstanceManagementClient][ContainerInstanceManagementClient].

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[authenticate](~/aci-docs-sample-python/src/aci_docs_sample.py#L45-L58 "Authenticate ACI and Resource Manager clients")]

Weitere Informationen zu den verfügbaren Authentifizierungsmethoden in den Python-Verwaltungsbibliotheken für Azure finden Sie unter [Authentifizieren bei den Azure-Verwaltungsbibliotheken für Python](/python/azure/python-sdk-azure-authenticate).

## <a name="create-container-group---single-container"></a>Erstellen einer Containergruppe – einzelner Container

In diesem Beispiel wird eine Containergruppe mit einem einzelnen Container erstellt.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L94-L141 "Create single-container group")]

## <a name="create-container-group---multiple-containers"></a>Erstellen einer Containergruppe – mehrere Container

In diesem Beispiel wird eine Containergruppe mit zwei Containern erstellt: einem Anwendungscontainer und einem Sidecar-Container.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group_multi](~/aci-docs-sample-python/src/aci_docs_sample.py#L144-L197 "Create multi-container group")]

## <a name="create-task-based-container-group"></a>Erstellen einer aufgabenbasierten Containergruppe

In diesem Beispiel wird eine Containergruppe mit einem einzelnen aufgabenbasierten Container erstellt. In diesem Beispiel werden mehrere Funktionen veranschaulicht:

* [Außerkraftsetzung der Befehlszeile:](/azure/container-instances/container-instances-start-command) Es wird eine andere benutzerdefinierte Befehlszeile angegeben als die, die in der Zeile `CMD` der Dockerfile-Datei des Containers angegeben ist. Die Außerkraftsetzung der Befehlszeile ermöglicht Ihnen die Angabe einer benutzerdefinierten Befehlszeile zur Ausführung beim Containerstart. Dabei wird die in den Container integrierte Standardbefehlszeile außer Kraft gesetzt. Für die Ausführung mehrerer Befehle beim Containerstart gilt Folgendes:

   Wenn Sie einen **einzelnen Befehl** mit mehreren Befehlszeilenargumenten ausführen möchten (etwa `echo FOO BAR`), müssen Sie sie als Zeichenfolgenliste für die `command`-Eigenschaft des [Containers][Container] angeben. Beispiel:

   `command = ['echo', 'FOO', 'BAR']`

   Wenn Sie jedoch **mehrere Befehle** mit (potenziell) mehreren Argumente ausführen möchten, müssen Sie eine Shell ausführen und die verketteten Befehle als Argument übergeben. Hiermit wird beispielsweise ein `echo`- sowie ein `tail`-Befehl ausgeführt:

   `command = ['/bin/sh', '-c', 'echo FOO BAR && tail -f /dev/null']`
* [Umgebungsvariablen:](/azure/container-instances/container-instances-environment-variables) Zwei Umgebungsvariablen werden für den Container in der Containergruppe angegeben. Verwenden Sie Umgebungsvariablen, um das Skript- oder Anwendungsverhalten zur Laufzeit zu ändern oder dynamische Informationen an eine im Container ausgeführte Anwendung zu übergeben.
* [Neustartrichtlinie:](/azure/container-instances/container-instances-restart-policy) Der Container wird mit der Neustartrichtlinie „Nie“ konfiguriert. Dies ist nützlich für aufgabenbasierte Container, die als Teil eines Batchauftrags ausgeführt werden.
* Vorgangsabruf mit [AzureOperationPoller][AzureOperationPoller]: Nach dem Aufrufen der Create-Methode wird der Vorgang abgerufen, um zu ermitteln, wann er abgeschlossen wurde und wann die Protokolle der Containergruppe abgerufen werden können.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group_task](~/aci-docs-sample-python/src/aci_docs_sample.py#L200-L276 "Run a task-based container")]

## <a name="list-container-groups"></a>Auflisten von Containergruppen

In diesem Beispiel werden die Containergruppen in einer Ressourcengruppe aufgelistet und dann einige ihrer Eigenschaften zurückgegeben.

Beim Auflisten der Containergruppen ist für [instance_view][instance_view] jeder zurückgegebenen Gruppe `None` angegeben. Um die Details der Containers in einer Containergruppe zu erhalten, müssen Sie dann die Containergruppe [abrufen][containergroupoperations_get]. Dabei wird die Gruppe mit aufgefüllter `instance_view`-Eigenschaft zurückgegeben. Der nächste Abschnitt ([Abrufen einer vorhandenen Containergruppe](#get-an-existing-container-group)) enthält ein Beispiel zum Durchlaufen der Container einer Containergruppe in `instance_view`.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[list_container_groups](~/aci-docs-sample-python/src/aci_docs_sample.py#L279-L293 "List container groups")]

## <a name="get-an-existing-container-group"></a>Abrufen einer vorhandenen Containergruppe

In diesem Beispiel wird eine bestimmte Containergruppe aus einer Ressourcengruppe abgerufen. Dann werden einige ihrer Eigenschaften (einschließlich der Container) und deren Werte ausgegeben.

Der [GET-Vorgang][containergroupoperations_get] gibt eine Containergruppe mit aufgefülltem returns a container group with its [instance_view][instance_view]-Objekt zurück, wodurch das Durchlaufen der einzelnen Container in der Gruppe ermöglicht wird. Nur der `get`-Vorgang füllt die Eigenschaft `instance_vew` der Containergruppe auf. Durch das Auflisten der Containergruppen in einem Abonnement oder einer Ressourcengruppe wird die Instanzenansicht nicht aufgefüllt, da der Vorgang unter Umständen kostspielig sein kann (beispielsweise beim Auflisten Hunderter Containergruppen, die wiederum unter Umständen mehrere Container enthalten). Wie bereits im Abschnitt [Auflisten von Containergruppen](#list-container-groups) erwähnt müssen Sie nach einem `list`-Vorgang einen `get`-Vorgang für eine bestimmte Containergruppe ausführen, um ihre Containerinstanzdetails abzurufen.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[get_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L296-L325 "Get container group")]

## <a name="delete-a-container-group"></a>Löschen einer Containergruppe

Dieses Beispiel löscht mehrere Containergruppen aus einer Ressourcengruppe sowie die Ressourcengruppe.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[delete_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L83-L91 "Delete container groups and resource group")]

## <a name="next-steps"></a>Nächste Schritte

* Der Quellcode für die vorhergehenden Beispiele ist auf GitHub zu finden:

  [Azure-Samples/aci-docs-sample-python][aci-docs-sample-python]

* Weitere Azure Container Instances-Codebeispiele:

  [Azure-Codebeispiele][samples-aci]

* Sehen Sie sich weiteren [Python-Beispielcode][samples-python] an, den Sie in Ihren Apps verwenden können.

> [!div class="nextstepaction"]
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/containerinstance/management)

<!-- LINKS - External -->
[aci-docs-sample-python]: https://github.com/Azure-Samples/aci-docs-sample-python
[samples-aci]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[samples-python]: https://azure.microsoft.com/resources/samples/?platform=python

<!-- TYPES -->
[AzureOperationPoller]: /python/api/msrestazure.azure_operation.AzureOperationPoller
[client_factory]: /python/api/azure.common.client_factory
[Container]: /python/api/azure.mgmt.containerinstance.models.container
[ContainerGroupInstanceView]: /python/api/azure.mgmt.containerinstance.models.containergrouppropertiesinstanceview
[containergroupoperations_get]: /python/api/azure.mgmt.containerinstance.operations.containergroupsoperations#get-resource-group-name--container-group-name--custom-headers-none--raw-false----operation-config-
[ContainerInstanceManagementClient]: /python/api/azure.mgmt.containerinstance.containerinstancemanagementclient
[instance_view]: /python/api/azure.mgmt.containerinstance.models.containergroup#variables
[ResourceManagementClient]: /python/api/azure.mgmt.resource.resources.resourcemanagementclient