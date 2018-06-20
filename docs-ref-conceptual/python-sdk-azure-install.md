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
ms.openlocfilehash: 792feac12f8328e2467017530065350e347c59b7
ms.sourcegitcommit: 757bf84535fd9d8299c4b51ec92a5ab1926cb671
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2018
ms.locfileid: "29565819"
---
# <a name="installation"></a><span data-ttu-id="38d40-104">Installation</span><span class="sxs-lookup"><span data-stu-id="38d40-104">Installation</span></span>

## <a name="which-python-and-which-version-to-use"></a><span data-ttu-id="38d40-105">Welche Python und welche Version sollte verwendet werden?</span><span class="sxs-lookup"><span data-stu-id="38d40-105">Which Python and which version to use</span></span>
<span data-ttu-id="38d40-106">Verschiedene Python-Interpreter sind verfügbar. Einige Beispiele:</span><span class="sxs-lookup"><span data-stu-id="38d40-106">There are several Python interpreters available - examples include:</span></span>

* <span data-ttu-id="38d40-107">CPython – der standardmäßige und am häufigsten verwendete Python-Interpreter</span><span class="sxs-lookup"><span data-stu-id="38d40-107">CPython - the standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="38d40-108">PyPy – schnelle, kompatible alternative Implementierung zu CPython</span><span class="sxs-lookup"><span data-stu-id="38d40-108">PyPy - fast, compliant alternative implementation to CPython</span></span>
* <span data-ttu-id="38d40-109">IronPython – Python-Interpreter, der unter .Net/CLR ausgeführt wird</span><span class="sxs-lookup"><span data-stu-id="38d40-109">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="38d40-110">Jython – Python-Interpreter, der in JVM (Java Virtual Machine) ausgeführt wird</span><span class="sxs-lookup"><span data-stu-id="38d40-110">Jython - Python interpreter that runs on the Java Virtual Machine</span></span>

<span data-ttu-id="38d40-111">**CPython**, v2.7 oder v3.4 und höher und PyPy 5.4.0 wurden getestet und unterstützen das Python Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="38d40-111">**CPython** v2.7 or v3.4+ and PyPy 5.4.0 are tested and supported for the Python Azure SDK.</span></span>

## <a name="where-to-get-python"></a><span data-ttu-id="38d40-112">Wo erhalte ich Python?</span><span class="sxs-lookup"><span data-stu-id="38d40-112">Where to get Python?</span></span>
<span data-ttu-id="38d40-113">Es gibt mehrere Möglichkeiten, CPython zu beziehen:</span><span class="sxs-lookup"><span data-stu-id="38d40-113">There are several ways to get CPython:</span></span>

* <span data-ttu-id="38d40-114">Direkt über [Python](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="38d40-114">Directly from [Python](https://www.python.org/)</span></span>
* <span data-ttu-id="38d40-115">Von angesehenen Distributoren wie [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) oder [ActiveState](https://www.activestate.com/)</span><span class="sxs-lookup"><span data-stu-id="38d40-115">From a reputable distro such as [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) or [ActiveState](https://www.activestate.com/)</span></span>
* <span data-ttu-id="38d40-116">Aus der Source erzeugen!</span><span class="sxs-lookup"><span data-stu-id="38d40-116">Build from source!</span></span>

<span data-ttu-id="38d40-117">Sofern Sie keine spezifischen Anforderungen haben, empfehlen wir Ihnen die ersten beiden Optionen.</span><span class="sxs-lookup"><span data-stu-id="38d40-117">Unless you have a specific need, we recommend the first two options.</span></span>

## <a name="installation-with-pip"></a><span data-ttu-id="38d40-118">Installation mit pip</span><span class="sxs-lookup"><span data-stu-id="38d40-118">Installation with pip</span></span>

<span data-ttu-id="38d40-119">Sie können die einzelnen Azure-Dienstbibliotheken separat installieren:</span><span class="sxs-lookup"><span data-stu-id="38d40-119">You can install each Azure service's library individually:</span></span>

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="38d40-120">Vorschaupakete können mit dem `--pre` -Flag installiert werden:</span><span class="sxs-lookup"><span data-stu-id="38d40-120">Preview packages can be installed using the `--pre` flag:</span></span>

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

<span data-ttu-id="38d40-121">Sie können auch eine Gruppe von Azure-Bibliotheken mithilfe des Metapakets `azure` in einer einzelnen Zeile installieren.</span><span class="sxs-lookup"><span data-stu-id="38d40-121">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span>

```bash
pip install azure
```

<span data-ttu-id="38d40-122">Von diesem Paket wird eine Vorschauversion veröffentlicht, auf die Sie über das Flag „--pre“ zugreifen können:</span><span class="sxs-lookup"><span data-stu-id="38d40-122">We publish a preview version of this package, which you can access using the --pre flag:</span></span>

```bash
pip install --pre azure
```

## <a name="install-from-github"></a><span data-ttu-id="38d40-123">Installieren über GitHub</span><span class="sxs-lookup"><span data-stu-id="38d40-123">Install from GitHub</span></span>

<span data-ttu-id="38d40-124">Vorgehensweise bei der Installation von `azure` über die Quelle:</span><span class="sxs-lookup"><span data-stu-id="38d40-124">If you want to install `azure` from source:</span></span>

    git clone git://github.com/Azure/azure-sdk-for-python.git
    cd azure-sdk-for-python
    python setup.py install