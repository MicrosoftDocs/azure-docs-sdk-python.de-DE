---
title: "Azure-Web-Apps-Bibliotheken für Python"
description: 
keywords: Azure, Python, SDK, API, Web-Apps, App Service
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/12/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: appservice
ms.openlocfilehash: 05f6ad173f4ec051654b5eb2a986b2c2a93cc33a
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2017
---
# <a name="azure-web-apps-libraries-for-python"></a><span data-ttu-id="9a42e-103">Azure-Web-Apps-Bibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="9a42e-103">Azure Web Apps libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="9a42e-104">Übersicht</span><span class="sxs-lookup"><span data-stu-id="9a42e-104">Overview</span></span>

<span data-ttu-id="9a42e-105">[Azure App Service](/azure/app-service) ermöglicht Ihnen das Bereitstellen und Skalieren von Websites, Webanwendungen, Diensten und REST-APIs.</span><span class="sxs-lookup"><span data-stu-id="9a42e-105">Deploy and scale websites, web applications, services, and REST APIs with [Azure App Service](/azure/app-service).</span></span>

<span data-ttu-id="9a42e-106">Informationen zu den ersten Schritten mit Azure App Service finden Sie unter [Erstellen einer Python-Web-App in Azure](/azure/app-service-web/app-service-web-get-started-python).</span><span class="sxs-lookup"><span data-stu-id="9a42e-106">To get started with Azure App Service, see [Create a Python web app in Azure](/azure/app-service-web/app-service-web-get-started-python).</span></span>

## <a name="management-api"></a><span data-ttu-id="9a42e-107">Verwaltungs-API</span><span class="sxs-lookup"><span data-stu-id="9a42e-107">Management API</span></span>

<span data-ttu-id="9a42e-108">Sie können Elemente, die in Azure App Service gehostet werden, mit der Verwaltungs-API bereitstellen, verwalten und skalieren.</span><span class="sxs-lookup"><span data-stu-id="9a42e-108">Deploy, manage, and scale elements hosted in the Azure App Service with the management API.</span></span>

<span data-ttu-id="9a42e-109">Installieren Sie die Bibliothek über pip:</span><span class="sxs-lookup"><span data-stu-id="9a42e-109">Install the library via pip.</span></span>

```bash
pip install azure-mgmt-web
```

### <a name="example"></a><span data-ttu-id="9a42e-110">Beispiel</span><span class="sxs-lookup"><span data-stu-id="9a42e-110">Example</span></span>

<span data-ttu-id="9a42e-111">Stellen Sie eine Web-App aus einem GitHub-Repository in einer Azure-Web-App bereit:</span><span class="sxs-lookup"><span data-stu-id="9a42e-111">Deploy a webapp from a GitHub repository into Azure Web App.</span></span>

```python
siteConfiguration = SiteConfig(
    python_version='3.4'
)

# create a web app
web_client.web_apps.create_or_update(
    RESOURCE_GROUP_NAME,
    WEB_APP_NAME,
    Site(
        location='eastus',
        server_farm_id=SERVICE_PLAN_ID,
        site_config=siteConfiguration
    )
)

# continuous deployment with GitHub
source_control_async_operation = web_client.web_apps.create_or_update_source_control(
    RESOURCE_GROUP_NAME,
    WEB_APP_NAME,
    SiteSourceControl(
        location='GitHub',
        repo_url='https://github.com/lisawong19/python-docs-hello-world',
        branch='master'
    )
)
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="9a42e-112">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="9a42e-112">Explore the Management APIs</span></span>](/python/api/overview/azure/webapps/managementlibrary)

## <a name="samples"></a><span data-ttu-id="9a42e-113">Beispiele</span><span class="sxs-lookup"><span data-stu-id="9a42e-113">Samples</span></span> 

* <span data-ttu-id="9a42e-114">[Verwalten von Azure-Websites mit Python][1]</span><span class="sxs-lookup"><span data-stu-id="9a42e-114">[Manage Azure websites with python][1]</span></span>
* <span data-ttu-id="9a42e-115">[Erstellen eines Logik-App-Workflows][2]</span><span class="sxs-lookup"><span data-stu-id="9a42e-115">[Create a Logic App workflow][2]</span></span>
 
<span data-ttu-id="9a42e-116">Zeigen Sie die [vollständige Liste](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=web-app) der Webanwendungsbeispiele an.</span><span class="sxs-lookup"><span data-stu-id="9a42e-116">View the [complete list](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=web-app) of web application samples.</span></span>

[1]: https://azure.microsoft.com/resources/samples/app-service-web-python-manage
[2]: ../docs-ref-conceptual/python-sdk-azure-samples-logic-app-workflow.md