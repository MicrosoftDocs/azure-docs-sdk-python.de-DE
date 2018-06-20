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
ms.openlocfilehash: d7be7cd76d019c6741d93c04458376a9352e363b
ms.sourcegitcommit: 41e6e6b5469271f4ec497a322b460e2a2af2c73d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
ms.locfileid: "30204259"
---
# <a name="operation-config"></a><span data-ttu-id="44ab5-104">Vorgangskonfiguration</span><span class="sxs-lookup"><span data-stu-id="44ab5-104">Operation config</span></span> 

<span data-ttu-id="44ab5-105">Methoden für Vorgänge weisen zusätzliche Parameter auf, die in „kwargs“ bereitgestellt werden können.</span><span class="sxs-lookup"><span data-stu-id="44ab5-105">Methods on operations have extra parameters which can be provided in the kwargs.</span></span> <span data-ttu-id="44ab5-106">Dies wird als „operation_config“ bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="44ab5-106">This is called operation_config.</span></span>

<span data-ttu-id="44ab5-107">Die Optionen für die Vorgangskonfiguration sind:</span><span class="sxs-lookup"><span data-stu-id="44ab5-107">The options for operation configuration are:</span></span>

|<span data-ttu-id="44ab5-108">Parametername</span><span class="sxs-lookup"><span data-stu-id="44ab5-108">Parameter name</span></span>|<span data-ttu-id="44ab5-109">Typ</span><span class="sxs-lookup"><span data-stu-id="44ab5-109">Type</span></span>|<span data-ttu-id="44ab5-110">Rolle</span><span class="sxs-lookup"><span data-stu-id="44ab5-110">Role</span></span>|
|----------------------|------|---------------|
| <span data-ttu-id="44ab5-111">Überprüfen</span><span class="sxs-lookup"><span data-stu-id="44ab5-111">verify</span></span> |`bool`|<span data-ttu-id="44ab5-112">Legt fest, ob das SSL-Zertifikat überprüft wird.</span><span class="sxs-lookup"><span data-stu-id="44ab5-112">Whether to verify the SSL certificate.</span></span> <span data-ttu-id="44ab5-113">Der Standardwert ist TRUE.</span><span class="sxs-lookup"><span data-stu-id="44ab5-113">Default is True.</span></span>|
|  <span data-ttu-id="44ab5-114">cert</span><span class="sxs-lookup"><span data-stu-id="44ab5-114">cert</span></span> |`str`| <span data-ttu-id="44ab5-115">Pfad zum lokalen Zertifikat für die clientseitige Überprüfung.</span><span class="sxs-lookup"><span data-stu-id="44ab5-115">Path to local certificate for client side verification.</span></span>|
|  <span data-ttu-id="44ab5-116">timeout</span><span class="sxs-lookup"><span data-stu-id="44ab5-116">timeout</span></span> |`int`| <span data-ttu-id="44ab5-117">Zeitlimit für das Herstellen einer Serververbindung in Sekunden.</span><span class="sxs-lookup"><span data-stu-id="44ab5-117">Timeout for establishing a server connection in seconds.</span></span>|
|  <span data-ttu-id="44ab5-118">allow_redirects</span><span class="sxs-lookup"><span data-stu-id="44ab5-118">allow_redirects</span></span> |`bool` | <span data-ttu-id="44ab5-119">Legt fest, ob Umleitungen zulässig sind.</span><span class="sxs-lookup"><span data-stu-id="44ab5-119">Whether to allow redirects.</span></span>|
|  <span data-ttu-id="44ab5-120">max_redirects</span><span class="sxs-lookup"><span data-stu-id="44ab5-120">max_redirects</span></span>  |`int`| <span data-ttu-id="44ab5-121">Maximale Anzahl zulässiger Umleitungen.</span><span class="sxs-lookup"><span data-stu-id="44ab5-121">Maimum number of allowed redirects.</span></span>|
|  <span data-ttu-id="44ab5-122">proxies</span><span class="sxs-lookup"><span data-stu-id="44ab5-122">proxies</span></span>  |`dict` |<span data-ttu-id="44ab5-123">Proxyservereinstellungen.</span><span class="sxs-lookup"><span data-stu-id="44ab5-123">Proxy server settings.</span></span>|
|  <span data-ttu-id="44ab5-124">use_env_proxies</span><span class="sxs-lookup"><span data-stu-id="44ab5-124">use_env_proxies</span></span> |`bool` |<span data-ttu-id="44ab5-125">Legt fest, ob Proxyeinstellungen aus lokalen Umgebungsvariablen gelesen werden.</span><span class="sxs-lookup"><span data-stu-id="44ab5-125">Whether to read proxy settings from local environment variables.</span></span>|
|  <span data-ttu-id="44ab5-126">retries</span><span class="sxs-lookup"><span data-stu-id="44ab5-126">retries</span></span>  |`int` | <span data-ttu-id="44ab5-127">Gesamtanzahl der Wiederholungsversuche.</span><span class="sxs-lookup"><span data-stu-id="44ab5-127">Total number of retry attempts.</span></span>|
|  <span data-ttu-id="44ab5-128">enable_http_logger</span><span class="sxs-lookup"><span data-stu-id="44ab5-128">enable_http_logger</span></span> | `bool`| <span data-ttu-id="44ab5-129">Aktivieren von Protokollen von HTTP im Debugmodus (standardmäßig „False“).</span><span class="sxs-lookup"><span data-stu-id="44ab5-129">Enable logs of HTTP in debug mode (False by default).</span></span>|
