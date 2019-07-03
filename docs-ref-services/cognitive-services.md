---
title: Azure Cognitive Services-Module für Python
description: Referenz zu Azure Cognitive Services-Modulen für Python
keywords: Azure, Python, SDK, API, Cognitive Services
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 04/04/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 5a23a52414e70facd6feae3af3956a5131f6b5c4
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534344"
---
# <a name="azure-cognitive-services-modules-for-python"></a>Azure Cognitive Services-Module für Python

Fügen Sie mit den Azure Cognitive Services-Modulen für Python Funktionen für Bild- und Gesichtserkennung, Sprachanalyse und Suche zu Ihren Python-Apps, -Websites und -Tools hinzu.

## <a name="vision-modules"></a>Bildanalysemodul

### <a name="computer-vision"></a>Maschinelles Sehen 

Gibt Informationen zu visuellen Inhalten in einem Bild zurück:

- Nutzen Sie Tagging, Beschreibungen und bereichspezifische Modelle, um Inhalte zu identifizieren und zuverlässig zu kennzeichnen.
- Wenden Sie Einstellungen für nicht jugendfreie oder anzügliche Inhalte an, um eine automatische Einschränkung dieser Inhalte zu ermöglichen.
- Bestimmen Sie Bildtypen und Farbschemas in Bildern.

Testen Sie [maschinelles Sehen](https://azure.microsoft.com/en-us/services/cognitive-services/computer-vision/) kostenlos in Ihrem Browser.

Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:

```python
pip install azure-cognitiveservices-vision-computervision
```

[Weitere Informationen](/azure/cognitive-services/computer-vision/home) zur Maschinelles Sehen-API und erste Schritte mit dem [Schnellstart für die Maschinelles Sehen-API mit Python](/azure/cognitive-services/computer-vision/quickstarts/python)

### <a name="content-moderator"></a>Content Moderator

Computergestützte Moderation von Texten, Videos und Bildern, erweitert um Tools für die Überprüfung durch Personen.

Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:

```python
pip install azure-cognitiveservices-vision-contentmoderator
```

[Weitere Informationen](/azure/cognitive-services/content-moderator/overview) zum Content Moderator-Dienst

### <a name="custom-vision-service"></a>Custom Vision Service

Laden Sie Bilder hoch, um ein Modell für maschinelles Sehen für Ihren bestimmten Anwendungsfall zu trainieren und anzupassen. Nach dem Trainieren des Modells können Sie die API verwenden, um mithilfe des Modells Bilder mit Tags zu versehen und die Ergebnisse auszuwerten, um die Klassifizierung zu verbessern.

Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:

```python
pip install azure-cognitiveservices-vision-customvision
```

[Weitere Informationen](/azure/cognitive-services/Custom-Vision-Service/home) zum Custom Vision Service und erste Schritte mit dem [Tutorial zu Custom Vision mit Python](/azure/cognitive-services/Custom-Vision-Service/python-tutorial)

### <a name="face-api"></a>Gesichtserkennungs-API

Nutzen Sie die Erkennung, Analyse, Organisation und Markierung von Gesichtern auf Fotos. 

Testen Sie die [Gesichtserkennungs-API](https://azure.microsoft.com/en-us/services/cognitive-services/face/) in Ihrem Browser.

Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:

```python
pip install cognitive-face
```

[Weitere Informationen](/azure/cognitive-services/face/overview) zur Gesichtserkennungs-API und erste Schritte mit dem [Schnellstart für die Gesichtserkennungs-API mit Python](/azure/cognitive-services/Face/Tutorials/FaceAPIinPythonTutorial)

## <a name="search-modules"></a>Suchmodule

### <a name="web-search"></a>Websuche

Rufen Sie durch die Bing-Websuche-API indizierte Webdokumente ab, und grenzen Sie die Ergebnisse anhand des Ergebnistyps, der Aktualität und anderer Faktoren ein. 

Testen Sie die [Websuche-API](https://azure.microsoft.com/en-us/services/cognitive-services/bing-web-search-api/) in Ihrem Browser.

Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:

```python
pip install azure-cognitiveservices-search-websearch
```

[Weitere Informationen](/azure/cognitive-services/bing-web-search/overview) zur Bing-Websuche-API und erste Schritte mit dem [Schnellstart für die Websuche-API mit Python](/azure/cognitive-services/bing-web-search/quickstarts/python)

### <a name="image-search"></a>Bildersuche

Suchen Sie nach Bildern, und erhalten Sie Ergebnisse mit Miniaturansichten, vollständigen URLs von Bildern, Bildmetadaten und vielem mehr.

Testen Sie die [Bildersuche-API](https://azure.microsoft.com/en-us/services/cognitive-services/bing-image-search-api/) in Ihrem Browser.

Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:

```python
pip install azure-cognitiveservices-search-imagesearch
```

[Weitere Informationen](/azure/cognitive-services/bing-image-search/overview) zur Bing-Bildersuche-API und erste Schritte mit dem [Schnellstart für die Bildersuche-API mit Python](/azure/cognitive-services/bing-image-search/quickstarts/python)


### <a name="entity-search"></a>Entitätssuche

Suchen Sie nach der relevantesten Entität (Orte, Personen oder Dinge) für einen bestimmten Suchbegriff oder Ort.

Testen Sie die [Entitätssuche-API](https://azure.microsoft.com/services/cognitive-services/bing-entity-search-api/) in Ihrem Browser.

Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:

```python
pip install azure-cognitiveservices-search-entitysearch
```

[Weitere Informationen](/azure/cognitive-services/bing-entities-search/search-the-web) zur Bing-Entitätssuche-API und erste Schritte mit dem [Schnellstart für die Entitätssuche-API mit Python](/azure/cognitive-services/bing-entities-search/quickstarts/python)

### <a name="custom-search"></a>Benutzerdefinierte Suche

Erstellen Sie eine benutzerdefinierte Websuche für Ihren spezifischen Suchbereich.

Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:

```python
pip install azure-cognitiveservices-search-customsearch
```

[Weitere Informationen](/azure/cognitive-services/bing-custom-search/) zur benutzerdefinierten Bing-Suche und erste Schritte beim Abfragen der benutzerdefinierten Suche über Python mit dem [Schnellstart für die benutzerdefinierte Such-API mit Python](/azure/cognitive-services/bing-custom-search/call-endpoint-python)

### <a name="video-search"></a>Videosuche

Finden Sie Videos überall im Web, und erhalten Sie Ergebnisse mit Metadaten wie Ersteller, Codierungsformat, Länge und Aufrufe.

Testen Sie die [Videosuche-API](https://azure.microsoft.com/services/cognitive-services/bing-video-search-api/) in Ihrem Browser.

Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:

```python
pip install azure-cognitiveservices-search-videosearch
```

[Weitere Informationen](/azure/cognitive-services/bing-video-search/search-the-web) zur Bing-Videosuche-API und erste Schritte mit dem [Schnellstart für die Videosuche-API mit Python](/azure/cognitive-services/bing-video-search/python)


### <a name="news-search"></a>News-Suche

Durchsuchen Sie das Web nach Nachrichtenartikeln, und nutzen Sie Metadaten zu Artikeln, zugehörigen News, Bildern und Informationen zur Quelle.

Testen Sie die [News-Suche-API](https://azure.microsoft.com/services/cognitive-services/bing-news-search-api/) in Ihrem Browser.

Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:

```python
pip install azure-cognitiveservices-search-newssearch
```

[Weitere Informationen](/azure/cognitive-services/bing-news-search/search-the-web) zum Bing-Dienst für die News-Suche und erste Schritte mit dem [Schnellstart für die News-Suche-API mit Python ](/azure/cognitive-services/bing-news-search/python)


## <a name="language-modules"></a>Sprachmodule

### <a name="text-analytics"></a>Textanalyse 

Die Textanalyse-API ist ein cloudbasierter Dienst für die Verarbeitung natürlicher Sprache aus unformatiertem Text. Die API bietet drei Hauptfunktionen:

- Stimmungsanalyse
- Schlüsselwortextraktion
- Spracherkennung

Testen Sie die [Textanalyse-API](https://azure.microsoft.com/en-us/services/cognitive-services/text-analytics/) in Ihrem Browser.

Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:

```python
pip install azure-cognitiveservices-language-textanalytics
```

[Weitere Informationen](/azure/cognitive-services/text-analytics/overview) zur Textanalyse-API und erste Schritte mit dem [Schnellstart für die Textanalyse-API mit Python](/azure/cognitive-services/text-analytics/quickstarts/python)


### <a name="spell-check"></a>Rechtschreibprüfung

Überprüfen Sie mit der Bing-Rechtschreibprüfungs-API Grammatik und Rechtschreibung im Kontext.

Testen Sie die [Rechtschreibprüfungs-API](https://azure.microsoft.com/en-us/services/cognitive-services/spell-check/) in Ihrem Browser.

Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:

```python
pip install azure-cognitiveservices-language-spellcheck
```

[Weitere Informationen](/azure/cognitive-services/bing-spell-check/proof-text) zur Rechtschreibprüfungs-API und erste Schritte mit dem [Schnellstart für die Rechtschreibprüfungs-API mit Python](/azure/cognitive-services/bing-spell-check/quickstarts/python)
