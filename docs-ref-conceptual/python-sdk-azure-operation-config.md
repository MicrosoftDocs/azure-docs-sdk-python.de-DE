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
# <a name="operation-config"></a><span data-ttu-id="01649-104">Vorgangskonfiguration</span><span class="sxs-lookup"><span data-stu-id="01649-104">Operation config</span></span> 

<span data-ttu-id="01649-105">Methoden für Vorgänge weisen zusätzliche Parameter auf, die in `kwargs` bereitgestellt werden können.</span><span class="sxs-lookup"><span data-stu-id="01649-105">Methods on operations have extra parameters which can be provided in the `kwargs`.</span></span> <span data-ttu-id="01649-106">Dies wird als „operation_config“ bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="01649-106">This is called operation_config.</span></span>

<span data-ttu-id="01649-107">Die Optionen für die Vorgangskonfiguration sind:</span><span class="sxs-lookup"><span data-stu-id="01649-107">The options for operation configuration are:</span></span>

|<span data-ttu-id="01649-108">Parametername</span><span class="sxs-lookup"><span data-stu-id="01649-108">Parameter name</span></span>|<span data-ttu-id="01649-109">Type</span><span class="sxs-lookup"><span data-stu-id="01649-109">Type</span></span>|<span data-ttu-id="01649-110">Rolle</span><span class="sxs-lookup"><span data-stu-id="01649-110">Role</span></span>|
|----------------------|------|---------------|
| <span data-ttu-id="01649-111">Überprüfen</span><span class="sxs-lookup"><span data-stu-id="01649-111">verify</span></span> |`bool`|<span data-ttu-id="01649-112">Legt fest, ob das SSL-Zertifikat überprüft wird.</span><span class="sxs-lookup"><span data-stu-id="01649-112">Whether to verify the SSL certificate.</span></span> <span data-ttu-id="01649-113">Der Standardwert ist TRUE.</span><span class="sxs-lookup"><span data-stu-id="01649-113">Default is True.</span></span>|
|  <span data-ttu-id="01649-114">cert</span><span class="sxs-lookup"><span data-stu-id="01649-114">cert</span></span> |`str`| <span data-ttu-id="01649-115">Pfad zum lokalen Zertifikat für die clientseitige Überprüfung.</span><span class="sxs-lookup"><span data-stu-id="01649-115">Path to local certificate for client side verification.</span></span>|
|  <span data-ttu-id="01649-116">timeout</span><span class="sxs-lookup"><span data-stu-id="01649-116">timeout</span></span> |`int`| <span data-ttu-id="01649-117">Zeitlimit für das Herstellen einer Serververbindung in Sekunden.</span><span class="sxs-lookup"><span data-stu-id="01649-117">Timeout for establishing a server connection in seconds.</span></span>|
|  <span data-ttu-id="01649-118">allow_redirects</span><span class="sxs-lookup"><span data-stu-id="01649-118">allow_redirects</span></span> |`bool` | <span data-ttu-id="01649-119">Legt fest, ob Umleitungen zulässig sind.</span><span class="sxs-lookup"><span data-stu-id="01649-119">Whether to allow redirects.</span></span>|
|  <span data-ttu-id="01649-120">max_redirects</span><span class="sxs-lookup"><span data-stu-id="01649-120">max_redirects</span></span>  |`int`| <span data-ttu-id="01649-121">Maximale Anzahl zulässiger Umleitungen.</span><span class="sxs-lookup"><span data-stu-id="01649-121">Maimum number of allowed redirects.</span></span>|
|  <span data-ttu-id="01649-122">proxies</span><span class="sxs-lookup"><span data-stu-id="01649-122">proxies</span></span>  |`dict` |<span data-ttu-id="01649-123">Proxyservereinstellungen.</span><span class="sxs-lookup"><span data-stu-id="01649-123">Proxy server settings.</span></span>|
|  <span data-ttu-id="01649-124">use_env_proxies</span><span class="sxs-lookup"><span data-stu-id="01649-124">use_env_proxies</span></span> |`bool` |<span data-ttu-id="01649-125">Legt fest, ob Proxyeinstellungen aus lokalen Umgebungsvariablen gelesen werden.</span><span class="sxs-lookup"><span data-stu-id="01649-125">Whether to read proxy settings from local environment variables.</span></span>|
|  <span data-ttu-id="01649-126">retries</span><span class="sxs-lookup"><span data-stu-id="01649-126">retries</span></span>  |`int` | <span data-ttu-id="01649-127">Gesamtanzahl der Wiederholungsversuche.</span><span class="sxs-lookup"><span data-stu-id="01649-127">Total number of retry attempts.</span></span>|
|  <span data-ttu-id="01649-128">enable_http_logger</span><span class="sxs-lookup"><span data-stu-id="01649-128">enable_http_logger</span></span> | `bool`| <span data-ttu-id="01649-129">Aktivieren von Protokollen von HTTP im Debugmodus (standardmäßig „False“).</span><span class="sxs-lookup"><span data-stu-id="01649-129">Enable logs of HTTP in debug mode (False by default).</span></span>|
