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
ms.openlocfilehash: 6014937fb41d6074e94578ccc47c30eb7b3f63d2
ms.sourcegitcommit: 434186988284e0a8268a9de11645912a81226d6b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/29/2019
ms.locfileid: "66376876"
---
# <a name="installation"></a><span data-ttu-id="fd057-104">Installation</span><span class="sxs-lookup"><span data-stu-id="fd057-104">Installation</span></span>

## <a name="which-python-and-which-version-to-use"></a><span data-ttu-id="fd057-105">Welche Python und welche Version sollte verwendet werden?</span><span class="sxs-lookup"><span data-stu-id="fd057-105">Which Python and which version to use</span></span>

<span data-ttu-id="fd057-106">Verschiedene Python-Interpreter sind verfügbar. Einige Beispiele:</span><span class="sxs-lookup"><span data-stu-id="fd057-106">There are several Python interpreters available - examples include:</span></span>

* <span data-ttu-id="fd057-107">CPython – der standardmäßige und am häufigsten verwendete Python-Interpreter</span><span class="sxs-lookup"><span data-stu-id="fd057-107">CPython - the standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="fd057-108">PyPy – schnelle, kompatible alternative Implementierung zu CPython</span><span class="sxs-lookup"><span data-stu-id="fd057-108">PyPy - fast, compliant alternative implementation to CPython</span></span>
* <span data-ttu-id="fd057-109">IronPython – Python-Interpreter, der unter .Net/CLR ausgeführt wird</span><span class="sxs-lookup"><span data-stu-id="fd057-109">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="fd057-110">Jython – Python-Interpreter, der in JVM (Java Virtual Machine) ausgeführt wird</span><span class="sxs-lookup"><span data-stu-id="fd057-110">Jython - Python interpreter that runs on the Java Virtual Machine</span></span>

<span data-ttu-id="fd057-111">**CPython**, v2.7 oder v3.4 und höher und PyPy 5.4.0 wurden getestet und unterstützen das Python Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="fd057-111">**CPython** v2.7 or v3.4+ and PyPy 5.4.0 are tested and supported for the Python Azure SDK.</span></span>

## <a name="where-to-get-python"></a><span data-ttu-id="fd057-112">Wo erhalte ich Python?</span><span class="sxs-lookup"><span data-stu-id="fd057-112">Where to get Python?</span></span>

<span data-ttu-id="fd057-113">Es gibt mehrere Möglichkeiten, CPython zu beziehen:</span><span class="sxs-lookup"><span data-stu-id="fd057-113">There are several ways to get CPython:</span></span>

* <span data-ttu-id="fd057-114">Direkt über [Python](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="fd057-114">Directly from [Python](https://www.python.org/)</span></span>
* <span data-ttu-id="fd057-115">Von angesehenen Distributoren wie [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) oder [ActiveState](https://www.activestate.com/)</span><span class="sxs-lookup"><span data-stu-id="fd057-115">From a reputable distro such as [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) or [ActiveState](https://www.activestate.com/)</span></span>
* <span data-ttu-id="fd057-116">Aus der Source erzeugen!</span><span class="sxs-lookup"><span data-stu-id="fd057-116">Build from source!</span></span>

<span data-ttu-id="fd057-117">Sofern Sie keine spezifischen Anforderungen haben, empfehlen wir Ihnen die ersten beiden Optionen.</span><span class="sxs-lookup"><span data-stu-id="fd057-117">Unless you have a specific need, we recommend the first two options.</span></span>

## <a name="installation-with-pip"></a><span data-ttu-id="fd057-118">Installation mit pip</span><span class="sxs-lookup"><span data-stu-id="fd057-118">Installation with pip</span></span>

<span data-ttu-id="fd057-119">Sie können die einzelnen Azure-Dienstbibliotheken separat installieren:</span><span class="sxs-lookup"><span data-stu-id="fd057-119">You can install each Azure service's library individually:</span></span>

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="fd057-120">Vorschaupakete können mit dem `--pre` -Flag installiert werden:</span><span class="sxs-lookup"><span data-stu-id="fd057-120">Preview packages can be installed using the `--pre` flag:</span></span>

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

<span data-ttu-id="fd057-121">Sie können auch eine Gruppe von Azure-Bibliotheken mithilfe des Metapakets `azure` in einer einzelnen Zeile installieren.</span><span class="sxs-lookup"><span data-stu-id="fd057-121">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span>

```bash
pip install azure
```

<span data-ttu-id="fd057-122">Von diesem Paket wird eine Vorschauversion veröffentlicht, auf die Sie über das Flag „--pre“ zugreifen können:</span><span class="sxs-lookup"><span data-stu-id="fd057-122">We publish a preview version of this package, which you can access using the --pre flag:</span></span>

```bash
pip install --pre azure
```

## <a name="install-from-github"></a><span data-ttu-id="fd057-123">Installieren über GitHub</span><span class="sxs-lookup"><span data-stu-id="fd057-123">Install from GitHub</span></span>

<span data-ttu-id="fd057-124">Vorgehensweise bei der Installation von `azure` über die Quelle:</span><span class="sxs-lookup"><span data-stu-id="fd057-124">If you want to install `azure` from source:</span></span>

```bash
git clone git://github.com/Azure/azure-sdk-for-python.git
cd azure-sdk-for-python
python setup.py install
```
