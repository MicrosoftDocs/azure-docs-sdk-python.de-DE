---
title: Installation
description: Installieren des Azure Python SDK
keywords: Azure, Python, SDK, API
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/05/2017
ms.topic: install
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.assetid: 
ms.openlocfilehash: 1ee0c110673f908832c1c9e8fd6dac4c90c16e8e
ms.sourcegitcommit: ce2921d9a6f21d58fdf77cbc843c9b4af0ea796d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/31/2017
---
# <a name="installation"></a><span data-ttu-id="45f74-104">Installation</span><span class="sxs-lookup"><span data-stu-id="45f74-104">Installation</span></span>

## <a name="installation-with-pip"></a><span data-ttu-id="45f74-105">Installation mit pip</span><span class="sxs-lookup"><span data-stu-id="45f74-105">Installation with pip</span></span>

<span data-ttu-id="45f74-106">Sie können die einzelnen Azure-Dienstbibliotheken separat installieren:</span><span class="sxs-lookup"><span data-stu-id="45f74-106">You can install each Azure service's library individually:</span></span>

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="45f74-107">Vorschaupakete können mit dem `--pre` -Flag installiert werden:</span><span class="sxs-lookup"><span data-stu-id="45f74-107">Preview packages can be installed using the `--pre` flag:</span></span>

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

<span data-ttu-id="45f74-108">Sie können auch eine Gruppe von Azure-Bibliotheken mithilfe des Metapakets `azure` in einer einzelnen Zeile installieren.</span><span class="sxs-lookup"><span data-stu-id="45f74-108">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span>

```bash
pip install azure
```

<span data-ttu-id="45f74-109">Von diesem Paket wird eine Vorschauversion veröffentlicht, auf die Sie über das Flag „--pre“ zugreifen können:</span><span class="sxs-lookup"><span data-stu-id="45f74-109">We publish a preview version of this package, which you can access using the --pre flag:</span></span>

```bash
pip install --pre azure
```

## <a name="install-from-github"></a><span data-ttu-id="45f74-110">Installieren über GitHub</span><span class="sxs-lookup"><span data-stu-id="45f74-110">Install from GitHub</span></span>

<span data-ttu-id="45f74-111">Vorgehensweise bei der Installation von `azure` über die Quelle:</span><span class="sxs-lookup"><span data-stu-id="45f74-111">If you want to install `azure` from source:</span></span>

    git clone git://github.com/Azure/azure-sdk-for-python.git
    cd azure-sdk-for-python
    python setup.py install
