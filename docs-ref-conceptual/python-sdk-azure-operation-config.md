---
title: Azure SDK-Konfiguration für Python-Vorgänge
description: C vom Azure SDK für Python ausgelöst
keywords: Azure, Python, SDK, API, Ausnahmen
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 03/07/2018
ms.topic: article
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: adeb6aa8a2c363c3119e97503df9536fb0633b4c
ms.sourcegitcommit: 434186988284e0a8268a9de11645912a81226d6b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/29/2019
ms.locfileid: "66376866"
---
# <a name="operation-config"></a>Vorgangskonfiguration 

Methoden für Vorgänge weisen zusätzliche Parameter auf, die in `kwargs` bereitgestellt werden können. Dies wird als „operation_config“ bezeichnet.

Die Optionen für die Vorgangskonfiguration sind:

|Parametername|Type|Rolle|
|----------------------|------|---------------|
| Überprüfen |`bool`|Legt fest, ob das SSL-Zertifikat überprüft wird. Der Standardwert ist TRUE.|
|  cert |`str`| Pfad zum lokalen Zertifikat für die clientseitige Überprüfung.|
|  timeout |`int`| Zeitlimit für das Herstellen einer Serververbindung in Sekunden.|
|  allow_redirects |`bool` | Legt fest, ob Umleitungen zulässig sind.|
|  max_redirects  |`int`| Maximale Anzahl zulässiger Umleitungen.|
|  proxies  |`dict` |Proxyservereinstellungen.|
|  use_env_proxies |`bool` |Legt fest, ob Proxyeinstellungen aus lokalen Umgebungsvariablen gelesen werden.|
|  retries  |`int` | Gesamtanzahl der Wiederholungsversuche.|
|  enable_http_logger | `bool`| Aktivieren von Protokollen von HTTP im Debugmodus (standardmäßig „False“).|
