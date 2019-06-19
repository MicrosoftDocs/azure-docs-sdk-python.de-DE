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
ms.openlocfilehash: 5890c2091f8456dd9b8bcb68f8a34eed3cae6e04
ms.sourcegitcommit: d7ad0e8b4ba4add5e6f63e6b9eac54ecccdc7090
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/14/2019
ms.locfileid: "67148170"
---
# <a name="azure-cognitive-services-modules-for-python"></a><span data-ttu-id="8b55b-104">Azure Cognitive Services-Module für Python</span><span class="sxs-lookup"><span data-stu-id="8b55b-104">Azure Cognitive Services modules for Python</span></span>

<span data-ttu-id="8b55b-105">Fügen Sie mit den Azure Cognitive Services-Modulen für Python Funktionen für Bild- und Gesichtserkennung, Sprachanalyse und Suche zu Ihren Python-Apps, -Websites und -Tools hinzu.</span><span class="sxs-lookup"><span data-stu-id="8b55b-105">Add image and face recognition, language analysis, and search to your Python apps, websites, and tools using the Azure Cognitive Services modules for Python.</span></span>

## <a name="vision-modules"></a><span data-ttu-id="8b55b-106">Bildanalysemodul</span><span class="sxs-lookup"><span data-stu-id="8b55b-106">Vision modules</span></span>

### <a name="computer-vision"></a><span data-ttu-id="8b55b-107">Maschinelles Sehen</span><span class="sxs-lookup"><span data-stu-id="8b55b-107">Computer Vision</span></span> 

<span data-ttu-id="8b55b-108">Gibt Informationen zu visuellen Inhalten in einem Bild zurück:</span><span class="sxs-lookup"><span data-stu-id="8b55b-108">Returns information about visual content found in an image:</span></span>

- <span data-ttu-id="8b55b-109">Nutzen Sie Tagging, Beschreibungen und bereichspezifische Modelle, um Inhalte zu identifizieren und zuverlässig zu kennzeichnen.</span><span class="sxs-lookup"><span data-stu-id="8b55b-109">Use tagging, descriptions, and domain-specific models to identify content and label it with confidence.</span></span>
- <span data-ttu-id="8b55b-110">Wenden Sie Einstellungen für nicht jugendfreie oder anzügliche Inhalte an, um eine automatische Einschränkung dieser Inhalte zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="8b55b-110">Apply adult/racy settings to enable automated restriction of adult content.</span></span>
- <span data-ttu-id="8b55b-111">Bestimmen Sie Bildtypen und Farbschemas in Bildern.</span><span class="sxs-lookup"><span data-stu-id="8b55b-111">Identify image types and color schemes in pictures.</span></span>

<span data-ttu-id="8b55b-112">Testen Sie [maschinelles Sehen](https://azure.microsoft.com/en-us/services/cognitive-services/computer-vision/) kostenlos in Ihrem Browser.</span><span class="sxs-lookup"><span data-stu-id="8b55b-112">[Try Computer Vision](https://azure.microsoft.com/en-us/services/cognitive-services/computer-vision/) for free in your browser.</span></span>

<span data-ttu-id="8b55b-113">Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:</span><span class="sxs-lookup"><span data-stu-id="8b55b-113">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-vision-computervision
```

<span data-ttu-id="8b55b-114">[Weitere Informationen](/azure/cognitive-services/computer-vision/home) zur Maschinelles Sehen-API und erste Schritte mit dem [Schnellstart für die Maschinelles Sehen-API mit Python](/azure/cognitive-services/computer-vision/quickstarts/python)</span><span class="sxs-lookup"><span data-stu-id="8b55b-114">[Learn more](/azure/cognitive-services/computer-vision/home) about the Computer Vision API and get started with the [Computer Vision API Python quickstart](/azure/cognitive-services/computer-vision/quickstarts/python).</span></span>

### <a name="content-moderator"></a><span data-ttu-id="8b55b-115">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="8b55b-115">Content Moderator</span></span>

<span data-ttu-id="8b55b-116">Computergestützte Moderation von Texten, Videos und Bildern, erweitert um Tools für die Überprüfung durch Personen.</span><span class="sxs-lookup"><span data-stu-id="8b55b-116">Machine-assisted moderation of text, video and images, augmented with human review tools.</span></span>

<span data-ttu-id="8b55b-117">Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:</span><span class="sxs-lookup"><span data-stu-id="8b55b-117">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-vision-contentmoderator
```

<span data-ttu-id="8b55b-118">[Weitere Informationen](/azure/cognitive-services/content-moderator/overview) zum Content Moderator-Dienst</span><span class="sxs-lookup"><span data-stu-id="8b55b-118">[Learn more](/azure/cognitive-services/content-moderator/overview) about the Content Moderator service.</span></span>

### <a name="custom-vision-service"></a><span data-ttu-id="8b55b-119">Custom Vision Service</span><span class="sxs-lookup"><span data-stu-id="8b55b-119">Custom Vision Service</span></span>

<span data-ttu-id="8b55b-120">Laden Sie Bilder hoch, um ein Modell für maschinelles Sehen für Ihren bestimmten Anwendungsfall zu trainieren und anzupassen.</span><span class="sxs-lookup"><span data-stu-id="8b55b-120">Upload images to train and customize a computer vision model for your specific use case.</span></span> <span data-ttu-id="8b55b-121">Nach dem Trainieren des Modells können Sie die API verwenden, um mithilfe des Modells Bilder mit Tags zu versehen und die Ergebnisse auszuwerten, um die Klassifizierung zu verbessern.</span><span class="sxs-lookup"><span data-stu-id="8b55b-121">Once the model is trained, you can use the API to tag images using the model and evaluate the results to improve your classifier.</span></span>

<span data-ttu-id="8b55b-122">Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:</span><span class="sxs-lookup"><span data-stu-id="8b55b-122">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-vision-customvision
```

<span data-ttu-id="8b55b-123">[Weitere Informationen](/azure/cognitive-services/Custom-Vision-Service/home) zum Custom Vision Service und erste Schritte mit dem [Tutorial zu Custom Vision mit Python](/azure/cognitive-services/Custom-Vision-Service/python-tutorial)</span><span class="sxs-lookup"><span data-stu-id="8b55b-123">[Learn more](/azure/cognitive-services/Custom-Vision-Service/home) about the Custom Vision service and get started with the [Custom Vision Python tutorial](/azure/cognitive-services/Custom-Vision-Service/python-tutorial)</span></span>

### <a name="face-api"></a><span data-ttu-id="8b55b-124">Gesichtserkennungs-API</span><span class="sxs-lookup"><span data-stu-id="8b55b-124">Face API</span></span>

<span data-ttu-id="8b55b-125">Nutzen Sie die Erkennung, Analyse, Organisation und Markierung von Gesichtern auf Fotos.</span><span class="sxs-lookup"><span data-stu-id="8b55b-125">Detect, identify, analyze, organize, and tag faces in photos.</span></span> 

<span data-ttu-id="8b55b-126">Testen Sie die [Gesichtserkennungs-API](https://azure.microsoft.com/en-us/services/cognitive-services/face/) in Ihrem Browser.</span><span class="sxs-lookup"><span data-stu-id="8b55b-126">[Try the Face API](https://azure.microsoft.com/en-us/services/cognitive-services/face/) in your browser.</span></span>

<span data-ttu-id="8b55b-127">Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:</span><span class="sxs-lookup"><span data-stu-id="8b55b-127">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install cognitive-face
```

<span data-ttu-id="8b55b-128">[Weitere Informationen](/azure/cognitive-services/face/overview) zur Gesichtserkennungs-API und erste Schritte mit dem [Schnellstart für die Gesichtserkennungs-API mit Python](/azure/cognitive-services/Face/Tutorials/FaceAPIinPythonTutorial)</span><span class="sxs-lookup"><span data-stu-id="8b55b-128">[Learn more](/azure/cognitive-services/face/overview) about the Face API and get started with the [Face API Python quickstart](/azure/cognitive-services/Face/Tutorials/FaceAPIinPythonTutorial).</span></span>

## <a name="search-modules"></a><span data-ttu-id="8b55b-129">Suchmodule</span><span class="sxs-lookup"><span data-stu-id="8b55b-129">Search modules</span></span>

### <a name="web-search"></a><span data-ttu-id="8b55b-130">Websuche</span><span class="sxs-lookup"><span data-stu-id="8b55b-130">Web search</span></span>

<span data-ttu-id="8b55b-131">Rufen Sie durch die Bing-Websuche-API indizierte Webdokumente ab, und grenzen Sie die Ergebnisse anhand des Ergebnistyps, der Aktualität und anderer Faktoren ein.</span><span class="sxs-lookup"><span data-stu-id="8b55b-131">Retrieve web documents indexed by the Bing Web Search API and narrow down the results by result type, freshness and more.</span></span> 

<span data-ttu-id="8b55b-132">Testen Sie die [Websuche-API](https://azure.microsoft.com/en-us/services/cognitive-services/bing-web-search-api/) in Ihrem Browser.</span><span class="sxs-lookup"><span data-stu-id="8b55b-132">[Try the Web Search API](https://azure.microsoft.com/en-us/services/cognitive-services/bing-web-search-api/) in your browser.</span></span>

<span data-ttu-id="8b55b-133">Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:</span><span class="sxs-lookup"><span data-stu-id="8b55b-133">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-search-websearch
```

<span data-ttu-id="8b55b-134">[Weitere Informationen](/azure/cognitive-services/bing-web-search/overview) zur Bing-Websuche-API und erste Schritte mit dem [Schnellstart für die Websuche-API mit Python](/azure/cognitive-services/bing-web-search/quickstarts/python)</span><span class="sxs-lookup"><span data-stu-id="8b55b-134">[Learn more](/azure/cognitive-services/bing-web-search/overview) about the Bing Web Search API and get started with the [Web Search API Python quickstart](/azure/cognitive-services/bing-web-search/quickstarts/python).</span></span>

### <a name="image-search"></a><span data-ttu-id="8b55b-135">Bildersuche</span><span class="sxs-lookup"><span data-stu-id="8b55b-135">Image search</span></span>

<span data-ttu-id="8b55b-136">Suchen Sie nach Bildern, und erhalten Sie Ergebnisse mit Miniaturansichten, vollständigen URLs von Bildern, Bildmetadaten und vielem mehr.</span><span class="sxs-lookup"><span data-stu-id="8b55b-136">Search for images and get thumbnails, full image URLs, image metadata and more in your results.</span></span>

<span data-ttu-id="8b55b-137">Testen Sie die [Bildersuche-API](https://azure.microsoft.com/en-us/services/cognitive-services/bing-image-search-api/) in Ihrem Browser.</span><span class="sxs-lookup"><span data-stu-id="8b55b-137">[Try the Image Search API](https://azure.microsoft.com/en-us/services/cognitive-services/bing-image-search-api/) in your browser.</span></span>

<span data-ttu-id="8b55b-138">Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:</span><span class="sxs-lookup"><span data-stu-id="8b55b-138">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-search-imagesearch
```

<span data-ttu-id="8b55b-139">[Weitere Informationen](/azure/cognitive-services/bing-image-search/overview) zur Bing-Bildersuche-API und erste Schritte mit dem [Schnellstart für die Bildersuche-API mit Python](/azure/cognitive-services/bing-image-search/quickstarts/python)</span><span class="sxs-lookup"><span data-stu-id="8b55b-139">[Learn more](/azure/cognitive-services/bing-image-search/overview) about the Bing Image Search API and get started with the [Image Search API Python quickstart](/azure/cognitive-services/bing-image-search/quickstarts/python).</span></span>


### <a name="entity-search"></a><span data-ttu-id="8b55b-140">Entitätssuche</span><span class="sxs-lookup"><span data-stu-id="8b55b-140">Entity search</span></span>

<span data-ttu-id="8b55b-141">Suchen Sie nach der relevantesten Entität (Orte, Personen oder Dinge) für einen bestimmten Suchbegriff oder Ort.</span><span class="sxs-lookup"><span data-stu-id="8b55b-141">Search for the most relevant entity (place, person, or thing) for a given search term or location.</span></span>

<span data-ttu-id="8b55b-142">Testen Sie die [Entitätssuche-API](https://azure.microsoft.com/services/cognitive-services/bing-entity-search-api/) in Ihrem Browser.</span><span class="sxs-lookup"><span data-stu-id="8b55b-142">[Try the Entity Search API](https://azure.microsoft.com/services/cognitive-services/bing-entity-search-api/) in your browser.</span></span>

<span data-ttu-id="8b55b-143">Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:</span><span class="sxs-lookup"><span data-stu-id="8b55b-143">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-search-entitysearch
```

<span data-ttu-id="8b55b-144">[Weitere Informationen](/azure/cognitive-services/bing-entities-search/search-the-web) zur Bing-Entitätssuche-API und erste Schritte mit dem [Schnellstart für die Entitätssuche-API mit Python](/azure/cognitive-services/bing-entities-search/quickstarts/python)</span><span class="sxs-lookup"><span data-stu-id="8b55b-144">[Learn more](/azure/cognitive-services/bing-entities-search/search-the-web) about the Bing Entity Search API and get started with the [Entity Search API Python quickstart](/azure/cognitive-services/bing-entities-search/quickstarts/python).</span></span>

### <a name="custom-search"></a><span data-ttu-id="8b55b-145">Benutzerdefinierte Suche</span><span class="sxs-lookup"><span data-stu-id="8b55b-145">Custom search</span></span>

<span data-ttu-id="8b55b-146">Erstellen Sie eine benutzerdefinierte Websuche für Ihren spezifischen Suchbereich.</span><span class="sxs-lookup"><span data-stu-id="8b55b-146">Build and a custom web search that meets your specific search domain.</span></span>

<span data-ttu-id="8b55b-147">Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:</span><span class="sxs-lookup"><span data-stu-id="8b55b-147">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-search-customsearch
```

<span data-ttu-id="8b55b-148">[Weitere Informationen](/azure/cognitive-services/bing-custom-search/) zur benutzerdefinierten Bing-Suche und erste Schritte beim Abfragen der benutzerdefinierten Suche über Python mit dem [Schnellstart für die benutzerdefinierte Such-API mit Python](/azure/cognitive-services/bing-custom-search/call-endpoint-python)</span><span class="sxs-lookup"><span data-stu-id="8b55b-148">[Learn more](/azure/cognitive-services/bing-custom-search/) about the Bing Custom Search service and get started with querying your custom search from Python with the [Custom Search API Python quickstart](/azure/cognitive-services/bing-custom-search/call-endpoint-python).</span></span>

### <a name="video-search"></a><span data-ttu-id="8b55b-149">Videosuche</span><span class="sxs-lookup"><span data-stu-id="8b55b-149">Video search</span></span>

<span data-ttu-id="8b55b-150">Finden Sie Videos überall im Web, und erhalten Sie Ergebnisse mit Metadaten wie Ersteller, Codierungsformat, Länge und Aufrufe.</span><span class="sxs-lookup"><span data-stu-id="8b55b-150">Find videos across the web and get results with creator, encoding, length, and view count metadata.</span></span>

<span data-ttu-id="8b55b-151">Testen Sie die [Videosuche-API](https://azure.microsoft.com/services/cognitive-services/bing-video-search-api/) in Ihrem Browser.</span><span class="sxs-lookup"><span data-stu-id="8b55b-151">[Try the Video Search API](https://azure.microsoft.com/services/cognitive-services/bing-video-search-api/) in your browser.</span></span>

<span data-ttu-id="8b55b-152">Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:</span><span class="sxs-lookup"><span data-stu-id="8b55b-152">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-search-videosearch
```

<span data-ttu-id="8b55b-153">[Weitere Informationen](/azure/cognitive-services/bing-video-search/search-the-web) zur Bing-Videosuche-API und erste Schritte mit dem [Schnellstart für die Videosuche-API mit Python](/azure/cognitive-services/bing-video-search/python)</span><span class="sxs-lookup"><span data-stu-id="8b55b-153">[Learn more](/azure/cognitive-services/bing-video-search/search-the-web) about the Bing Video Search service and get started with the [Video Search API Python quickstart](/azure/cognitive-services/bing-video-search/python).</span></span>


### <a name="news-search"></a><span data-ttu-id="8b55b-154">News-Suche</span><span class="sxs-lookup"><span data-stu-id="8b55b-154">News search</span></span>

<span data-ttu-id="8b55b-155">Durchsuchen Sie das Web nach Nachrichtenartikeln, und nutzen Sie Metadaten zu Artikeln, zugehörigen News, Bildern und Informationen zur Quelle.</span><span class="sxs-lookup"><span data-stu-id="8b55b-155">Search the web for news articles and work with article, related news, images, and provider info metadata.</span></span>

<span data-ttu-id="8b55b-156">Testen Sie die [News-Suche-API](https://azure.microsoft.com/services/cognitive-services/bing-news-search-api/) in Ihrem Browser.</span><span class="sxs-lookup"><span data-stu-id="8b55b-156">[Try the News Search API](https://azure.microsoft.com/services/cognitive-services/bing-news-search-api/) in your browser.</span></span>

<span data-ttu-id="8b55b-157">Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:</span><span class="sxs-lookup"><span data-stu-id="8b55b-157">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-search-newssearch
```

<span data-ttu-id="8b55b-158">[Weitere Informationen](/azure/cognitive-services/bing-news-search/search-the-web) zum Bing-Dienst für die News-Suche und erste Schritte mit dem [Schnellstart für die News-Suche-API mit Python ](//azure/cognitive-services/bing-news-search/python)</span><span class="sxs-lookup"><span data-stu-id="8b55b-158">[Learn more](/azure/cognitive-services/bing-news-search/search-the-web) about the Bing News Search service and get started with the [News Search API Python quickstart](//azure/cognitive-services/bing-news-search/python).</span></span>


## <a name="language-modules"></a><span data-ttu-id="8b55b-159">Sprachmodule</span><span class="sxs-lookup"><span data-stu-id="8b55b-159">Language modules</span></span>

### <a name="text-analytics"></a><span data-ttu-id="8b55b-160">Textanalyse</span><span class="sxs-lookup"><span data-stu-id="8b55b-160">Text Analytics</span></span> 

<span data-ttu-id="8b55b-161">Die Textanalyse-API ist ein cloudbasierter Dienst für die Verarbeitung natürlicher Sprache aus unformatiertem Text.</span><span class="sxs-lookup"><span data-stu-id="8b55b-161">The Text Analytics API is a cloud-based service that provides  natural language processing over raw text.</span></span> <span data-ttu-id="8b55b-162">Die API bietet drei Hauptfunktionen:</span><span class="sxs-lookup"><span data-stu-id="8b55b-162">The API includes three main functions:</span></span>

- <span data-ttu-id="8b55b-163">Stimmungsanalyse</span><span class="sxs-lookup"><span data-stu-id="8b55b-163">Sentiment analysis</span></span>
- <span data-ttu-id="8b55b-164">Schlüsselwortextraktion</span><span class="sxs-lookup"><span data-stu-id="8b55b-164">Key phrase extraction</span></span>
- <span data-ttu-id="8b55b-165">Spracherkennung</span><span class="sxs-lookup"><span data-stu-id="8b55b-165">Language detection</span></span>

<span data-ttu-id="8b55b-166">Testen Sie die [Textanalyse-API](https://azure.microsoft.com/en-us/services/cognitive-services/text-analytics/) in Ihrem Browser.</span><span class="sxs-lookup"><span data-stu-id="8b55b-166">[Try the Text Analytics API](https://azure.microsoft.com/en-us/services/cognitive-services/text-analytics/) in your browser.</span></span>

<span data-ttu-id="8b55b-167">Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:</span><span class="sxs-lookup"><span data-stu-id="8b55b-167">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-language-textanalytics
```

<span data-ttu-id="8b55b-168">[Weitere Informationen](/azure/cognitive-services/text-analytics/overview) zur Textanalyse-API und erste Schritte mit dem [Schnellstart für die Textanalyse-API mit Python](/azure/cognitive-services/text-analytics/quickstarts/python)</span><span class="sxs-lookup"><span data-stu-id="8b55b-168">[Learn more](/azure/cognitive-services/text-analytics/overview) about the Text Analytics API and get started with the [Text Analytics API Python quickstart](/azure/cognitive-services/text-analytics/quickstarts/python).</span></span>


### <a name="spell-check"></a><span data-ttu-id="8b55b-169">Rechtschreibprüfung</span><span class="sxs-lookup"><span data-stu-id="8b55b-169">Spell Check</span></span>

<span data-ttu-id="8b55b-170">Überprüfen Sie mit der Bing-Rechtschreibprüfungs-API Grammatik und Rechtschreibung im Kontext.</span><span class="sxs-lookup"><span data-stu-id="8b55b-170">Perform contextual grammar and spell checking with the Bing Spell Check API.</span></span>

<span data-ttu-id="8b55b-171">Testen Sie die [Rechtschreibprüfungs-API](https://azure.microsoft.com/en-us/services/cognitive-services/spell-check/) in Ihrem Browser.</span><span class="sxs-lookup"><span data-stu-id="8b55b-171">[Try the Spell Check API](https://azure.microsoft.com/en-us/services/cognitive-services/spell-check/) in your browser.</span></span>

<span data-ttu-id="8b55b-172">Rufen Sie das Python-Modul mit [pip](https://pip.pypa.io/en/stable/quickstart/) ab:</span><span class="sxs-lookup"><span data-stu-id="8b55b-172">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-language-spellcheck
```

<span data-ttu-id="8b55b-173">[Weitere Informationen](/azure/cognitive-services/bing-spell-check/proof-text) zur Rechtschreibprüfungs-API und erste Schritte mit dem [Schnellstart für die Rechtschreibprüfungs-API mit Python](/azure/cognitive-services/bing-spell-check/quickstarts/python)</span><span class="sxs-lookup"><span data-stu-id="8b55b-173">[Learn more](/azure/cognitive-services/bing-spell-check/proof-text) about the Spell Check API and get started with the [Spell Check API Python quickstart](/azure/cognitive-services/bing-spell-check/quickstarts/python).</span></span>
