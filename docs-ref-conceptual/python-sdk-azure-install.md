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
# <a name="installation"></a>Installation

## <a name="installation-with-pip"></a>Installation mit pip

Sie können die einzelnen Azure-Dienstbibliotheken separat installieren:

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

Vorschaupakete können mit dem `--pre` -Flag installiert werden:

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

Sie können auch eine Gruppe von Azure-Bibliotheken mithilfe des Metapakets `azure` in einer einzelnen Zeile installieren.

```bash
pip install azure
```

Von diesem Paket wird eine Vorschauversion veröffentlicht, auf die Sie über das Flag „--pre“ zugreifen können:

```bash
pip install --pre azure
```

## <a name="install-from-github"></a>Installieren über GitHub

Vorgehensweise bei der Installation von `azure` über die Quelle:

    git clone git://github.com/Azure/azure-sdk-for-python.git
    cd azure-sdk-for-python
    python setup.py install
