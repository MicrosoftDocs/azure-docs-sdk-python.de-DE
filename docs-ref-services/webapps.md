---
title: Azure-Web-Apps-Bibliotheken für Python
description: ''
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
ms.openlocfilehash: 8e8dd78cbc2d5887308361a47a9571ce242aee6e
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
ms.locfileid: "29479223"
---
# <a name="azure-web-apps-libraries-for-python"></a>Azure-Web-Apps-Bibliotheken für Python

## <a name="overview"></a>Übersicht

[Azure App Service](/azure/app-service) ermöglicht Ihnen das Bereitstellen und Skalieren von Websites, Webanwendungen, Diensten und REST-APIs.

Informationen zu den ersten Schritten mit Azure App Service finden Sie unter [Erstellen einer Python-Web-App in Azure](/azure/app-service-web/app-service-web-get-started-python).

## <a name="management-api"></a>Verwaltungs-API

Sie können Elemente, die in Azure App Service gehostet werden, mit der Verwaltungs-API bereitstellen, verwalten und skalieren.

Installieren Sie die Bibliothek über pip:

```bash
pip install azure-mgmt-web
```

### <a name="example"></a>Beispiel

Stellen Sie eine Web-App aus einem GitHub-Repository in einer Azure-Web-App bereit:

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
> [Informationen zu den Verwaltungs-APIs](/python/api/overview/azure/webapps/management)

## <a name="samples"></a>Beispiele 

* [Verwalten von Azure-Websites mit Python][1]
* [Erstellen eines Logik-App-Workflows][2]
 
Zeigen Sie die [vollständige Liste](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=web-app) der Webanwendungsbeispiele an.

[1]: https://azure.microsoft.com/resources/samples/app-service-web-python-manage
[2]: ../docs-ref-conceptual/python-sdk-azure-samples-logic-app-workflow.md