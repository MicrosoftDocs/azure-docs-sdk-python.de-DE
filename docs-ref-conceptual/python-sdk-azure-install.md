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
ms.openlocfilehash: 9fd11cbc7b987b970ceee85c7b11b22e3d6299ea
ms.sourcegitcommit: 31d7df367b15ec09a5a610eb333295bba0f6b351
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/26/2019
ms.locfileid: "67395447"
---
# <a name="installation"></a><span data-ttu-id="1cfdd-104">Installation</span><span class="sxs-lookup"><span data-stu-id="1cfdd-104">Installation</span></span>

## <a name="which-python-and-which-version-to-use"></a><span data-ttu-id="1cfdd-105">Welche Python und welche Version sollte verwendet werden?</span><span class="sxs-lookup"><span data-stu-id="1cfdd-105">Which Python and which version to use</span></span>

<span data-ttu-id="1cfdd-106">Verschiedene Python-Interpreter sind verfügbar. Einige Beispiele:</span><span class="sxs-lookup"><span data-stu-id="1cfdd-106">There are several Python interpreters available - examples include:</span></span>

* <span data-ttu-id="1cfdd-107">CPython – der standardmäßige und am häufigsten verwendete Python-Interpreter</span><span class="sxs-lookup"><span data-stu-id="1cfdd-107">CPython - the standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="1cfdd-108">PyPy – schnelle, kompatible alternative Implementierung zu CPython</span><span class="sxs-lookup"><span data-stu-id="1cfdd-108">PyPy - fast, compliant alternative implementation to CPython</span></span>
* <span data-ttu-id="1cfdd-109">IronPython – Python-Interpreter, der unter .Net/CLR ausgeführt wird</span><span class="sxs-lookup"><span data-stu-id="1cfdd-109">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="1cfdd-110">Jython – Python-Interpreter, der in JVM (Java Virtual Machine) ausgeführt wird</span><span class="sxs-lookup"><span data-stu-id="1cfdd-110">Jython - Python interpreter that runs on the Java Virtual Machine</span></span>

<span data-ttu-id="1cfdd-111">**CPython**, v2.7 oder v3.4 und höher und PyPy 5.4.0 wurden getestet und unterstützen das Python Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="1cfdd-111">**CPython** v2.7 or v3.4+ and PyPy 5.4.0 are tested and supported for the Python Azure SDK.</span></span>

## <a name="where-to-get-python"></a><span data-ttu-id="1cfdd-112">Wo erhalte ich Python?</span><span class="sxs-lookup"><span data-stu-id="1cfdd-112">Where to get Python?</span></span>

<span data-ttu-id="1cfdd-113">Es gibt mehrere Möglichkeiten, CPython zu beziehen:</span><span class="sxs-lookup"><span data-stu-id="1cfdd-113">There are several ways to get CPython:</span></span>

* <span data-ttu-id="1cfdd-114">Direkt über [Python](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="1cfdd-114">Directly from [Python](https://www.python.org/)</span></span>
* <span data-ttu-id="1cfdd-115">Von angesehenen Distributoren wie [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) oder [ActiveState](https://www.activestate.com/)</span><span class="sxs-lookup"><span data-stu-id="1cfdd-115">From a reputable distro such as [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) or [ActiveState](https://www.activestate.com/)</span></span>
* <span data-ttu-id="1cfdd-116">Aus der Source erzeugen!</span><span class="sxs-lookup"><span data-stu-id="1cfdd-116">Build from source!</span></span>

<span data-ttu-id="1cfdd-117">Sofern Sie keine spezifischen Anforderungen haben, empfehlen wir Ihnen die ersten beiden Optionen.</span><span class="sxs-lookup"><span data-stu-id="1cfdd-117">Unless you have a specific need, we recommend the first two options.</span></span>

## <a name="installation-with-pip"></a><span data-ttu-id="1cfdd-118">Installation mit pip</span><span class="sxs-lookup"><span data-stu-id="1cfdd-118">Installation with pip</span></span>

<span data-ttu-id="1cfdd-119">Sie können die einzelnen Azure-Dienstbibliotheken separat installieren:</span><span class="sxs-lookup"><span data-stu-id="1cfdd-119">You can install each Azure service's library individually:</span></span>

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="1cfdd-120">Vorschaupakete können mit dem `--pre` -Flag installiert werden:</span><span class="sxs-lookup"><span data-stu-id="1cfdd-120">Preview packages can be installed using the `--pre` flag:</span></span>

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

<span data-ttu-id="1cfdd-121">Sie können auch eine Gruppe von Azure-Bibliotheken mithilfe des Metapakets `azure` in einer einzelnen Zeile installieren.</span><span class="sxs-lookup"><span data-stu-id="1cfdd-121">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span>

```bash
pip install azure
```

<span data-ttu-id="1cfdd-122">Von diesem Paket wird eine Vorschauversion veröffentlicht, auf die Sie über das Flag „--pre“ zugreifen können:</span><span class="sxs-lookup"><span data-stu-id="1cfdd-122">We publish a preview version of this package, which you can access using the --pre flag:</span></span>

```bash
pip install --pre azure
```

## <a name="install-from-github"></a><span data-ttu-id="1cfdd-123">Installieren über GitHub</span><span class="sxs-lookup"><span data-stu-id="1cfdd-123">Install from GitHub</span></span>

<span data-ttu-id="1cfdd-124">Vorgehensweise bei der Installation von `azure` über die Quelle:</span><span class="sxs-lookup"><span data-stu-id="1cfdd-124">If you want to install `azure` from source:</span></span>

```bash
git clone git://github.com/Azure/azure-sdk-for-python.git
cd azure-sdk-for-python
python setup.py install
```

## <a name="install-an-older-version-with-pip"></a><span data-ttu-id="1cfdd-125">Installieren einer älteren Version mit pip</span><span class="sxs-lookup"><span data-stu-id="1cfdd-125">Install an older version with pip</span></span>
<span data-ttu-id="1cfdd-126">Sie können eine ältere Version von `azure` installieren, indem Sie die Versionsdetails „azure==3.0.0“ angeben.</span><span class="sxs-lookup"><span data-stu-id="1cfdd-126">You can install an older version of `azure` by specifying 'azure==3.0.0' version details.</span></span>
```bash
pip install azure==3.0.0 
```
## <a name="check-sdk-installation-details-with-pip"></a><span data-ttu-id="1cfdd-127">Überprüfen der SDK-Installationsdetails mit pip</span><span class="sxs-lookup"><span data-stu-id="1cfdd-127">Check SDK installation details with pip</span></span>
<span data-ttu-id="1cfdd-128">Sie können u. a. den Installationspfad und die Versionsdetails des `azure` SDK überprüfen.</span><span class="sxs-lookup"><span data-stu-id="1cfdd-128">You can check `azure` SDK installation location, version details etc.</span></span>
```bash
pip show azure # Show installed version, location details etc.
pip freeze     # Output installed packages in requirements format.
pip list       # List installed packages, including editables.
```
## <a name="to-uninstall-with-pip"></a><span data-ttu-id="1cfdd-129">So führen Sie eine Deinstallation mit pip aus</span><span class="sxs-lookup"><span data-stu-id="1cfdd-129">To uninstall with pip</span></span>
<span data-ttu-id="1cfdd-130">Sie können alle Azure-Bibliotheken mithilfe des Metapakets `azure` in einer einzelnen Zeile deinstallieren.</span><span class="sxs-lookup"><span data-stu-id="1cfdd-130">You can uninstall all Azure libraries in a single line using the `azure` meta-package.</span></span>
```bash
pip uninstall azure 
```
> [!NOTE]
> <span data-ttu-id="1cfdd-131">`pip uninstall azure` entfernt das Metapaket `azure`, hinterlässt jedoch Pakete vom Typ `azure-*` (sowie weitere Pakete wie `adal` und `msrest` ).</span><span class="sxs-lookup"><span data-stu-id="1cfdd-131">`pip uninstall azure`removes the `azure` meta-package but leaves the individual `azure-*` packages behind (and others, like `adal` and `msrest` ).</span></span> <span data-ttu-id="1cfdd-132">Eine Besonderheit von Python und pip besteht darin, dass bei Paketen mit Abhängigkeiten die Deinstallation des ursprünglichen Pakets nicht zur Deinstallation der Abhängigkeiten führt.</span><span class="sxs-lookup"><span data-stu-id="1cfdd-132">An aspect of Python and pip is that for all packages that have dependencies, uninstalling the initial package does not uninstall the dependencies.</span></span> <span data-ttu-id="1cfdd-133">Wenn Sie `azure-` und die unterstützenden Pakete entfernen möchten, führen Sie den Befehl `pip freeze | grep 'azure-' | xargs pip uninstall -y` aus. (Deinstallieren Sie anschließend adal, msrest und msrestazure.)</span><span class="sxs-lookup"><span data-stu-id="1cfdd-133">To remove `azure-` and its supporting packages, run the command `pip freeze | grep 'azure-' | xargs pip uninstall -y` (and then perform individual uninstalls for adal, msrest, and msrestazure).</span></span>

