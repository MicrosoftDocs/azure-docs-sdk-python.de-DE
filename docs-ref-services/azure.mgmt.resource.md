---
title: Azure-Ressourcenbibliotheken für Python
description: ''
keywords: Azure, Python, SDK, API, Ressourcen
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 06/19/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: resources
ms.openlocfilehash: d708a5e7296b166b6e55b9b7b0d995e72e264267
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534371"
---
# <a name="azure-resources-libraries-for-python"></a>Azure-Ressourcenbibliotheken für Python 

## <a name="overview"></a>Übersicht 
Verwalten von Azure-Ressourcen in Ressourcengruppen

| Paket  |  BESCHREIBUNG |
|---|---|
|[azure.mgmt.resource.features][1]|Die Steuerung für die Azure-Featureanzeige (Azure Feature Exposure Control, AFEC) ist ein Mechanismus, mit dem Ressourcenanbieter die Anzeige von Features für Benutzer steuern können.|
|[azure.mgmt.resource.links][2]|Azure-Ressourcen können verknüpft werden, um logische Beziehungen zu bilden. Sie können Verknüpfungen zwischen Ressourcen aus verschiedenen Ressourcengruppen herstellen.|
|[azure.mgmt.resource.locks][3]|Azure-Ressourcen können gesperrt werden, um zu verhindern, dass andere Benutzer in Ihrer Organisation Ressourcen löschen oder ändern.|
|[azure.mgmt.resource.managedapplications][4]|Über ARM verwaltete Anwendungen (Geräte)|
|[azure.mgmt.resource.policy][5]|Zur Verwaltung und Steuerung des Ressourcenzugriffs können Sie benutzerdefinierte Richtlinien definieren und bereichsweise zuweisen.|
|[azure.mgmt.resource.resources][6]| Stellt Vorgänge für die Arbeit mit Ressourcen und Ressourcengruppen bereit.|
|[azure.mgmt.resource.subscriptions][7]|Alle Ressourcengruppen und Ressourcen befinden sich in Abonnements. Diese Vorgänge ermöglichen das Abrufen von Informationen zu Abonnements und Mandanten.|

[1]: /python/api/azure.mgmt.resource.features
[2]: /python/api/azure.mgmt.resource.links
[3]: /python/api/azure.mgmt.resource.locks
[4]: /python/api/azure.mgmt.resource.managedapplications
[5]: /python/api/azure.mgmt.resource.policy
[6]: /python/api/azure.mgmt.resource.resources
[7]: /python/api/azure.mgmt.resource.subscriptions

## <a name="install-the-libraries"></a>Installieren der Bibliotheken 
```bash
pip install azure-mgmt-resource
```

## <a name="example"></a>Beispiel
Hier sehen Sie ein Beispiel zum Erstellen einer Ressourcengruppe: 

```python
from azure.mgmt.resource import ResourceManagementClient
client = ResourceManagementClient(credentials, subscription_id)
client.resource_groups.create(RESOURCE_GROUP_NAME, {'location':'eastus'})
```

Sehen Sie sich weiteren [Python-Beispielcode](https://azure.microsoft.com/resources/samples/?platform=python) an, den Sie in Ihren Apps verwenden können. 