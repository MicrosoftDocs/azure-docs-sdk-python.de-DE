---
title: Azure-Überwachungsbibliotheken für Python
description: Referenz zu Azure-Überwachungsbibliotheken für Python
keywords: Azure, Python, SDK, API, Überwachung
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/19/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 2d4172fa206b89437cca88fb2c5d0a7965be4e9b
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2018
ms.locfileid: "52277172"
---
# <a name="azure-monitoring-libraries-for-python"></a><span data-ttu-id="c8586-104">Azure-Überwachungsbibliotheken für Python</span><span class="sxs-lookup"><span data-stu-id="c8586-104">Azure Monitoring libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="c8586-105">Übersicht</span><span class="sxs-lookup"><span data-stu-id="c8586-105">Overview</span></span> 
<span data-ttu-id="c8586-106">Die Überwachung stellt Daten bereit, auf deren Grundlage die ordnungsgemäße Ausführung der Anwendung sichergestellt werden kann.</span><span class="sxs-lookup"><span data-stu-id="c8586-106">Monitoring provides data to ensure that your application stays up and running in a healthy state.</span></span> <span data-ttu-id="c8586-107">Sie trägt auch zur Vermeidung potenzieller Probleme bei und hilft bei der Behandlung bereits aufgetretener Probleme.</span><span class="sxs-lookup"><span data-stu-id="c8586-107">It also helps you to stave off potential problems or troubleshoot past ones.</span></span> <span data-ttu-id="c8586-108">Darüber hinaus können Sie auf der Grundlage von Überwachungsdaten umfassende Erkenntnisse über Ihre Anwendung gewinnen.</span><span class="sxs-lookup"><span data-stu-id="c8586-108">In addition, you can use monitoring data to gain deep insights about your application.</span></span> <span data-ttu-id="c8586-109">Mithilfe dieser Kenntnisse können Sie die Leistung oder Wartungsfreundlichkeit der Anwendung verbessern oder Aktionen automatisieren, die andernfalls manuell ausgeführt werden müssten.</span><span class="sxs-lookup"><span data-stu-id="c8586-109">That knowledge can help you to improve application performance or maintainability, or automate actions that would otherwise require manual intervention.</span></span>

<span data-ttu-id="c8586-110">Weitere Informationen zu Azure Monitor finden Sie [hier](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor).</span><span class="sxs-lookup"><span data-stu-id="c8586-110">Learn more about Azure Monitor [here](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor).</span></span> 

## <a name="installation"></a><span data-ttu-id="c8586-111">Installation</span><span class="sxs-lookup"><span data-stu-id="c8586-111">Installation</span></span>
```bash
pip install azure-mgmt-monitor
```

## <a name="example---metrics"></a><span data-ttu-id="c8586-112">Beispiel – Metriken</span><span class="sxs-lookup"><span data-stu-id="c8586-112">Example - Metrics</span></span>
<span data-ttu-id="c8586-113">In diesem Beispiel werden die Metriken einer Ressource in Azure (virtuelle Computer, usw.) abgerufen.</span><span class="sxs-lookup"><span data-stu-id="c8586-113">This sample obtains the metrics of a resource on Azure (VMs, etc.).</span></span> <span data-ttu-id="c8586-114">Für dieses Beispiel ist mindestens Version 0.4.0 des Python-Pakets erforderlich.</span><span class="sxs-lookup"><span data-stu-id="c8586-114">This sample requires version 0.4.0 of the Python package at least.</span></span>

<span data-ttu-id="c8586-115">Eine vollständige Liste der verfügbaren Schlüsselwörter für Filter ist [hier](https://msdn.microsoft.com/library/azure/mt743622.aspx) verfügbar.</span><span class="sxs-lookup"><span data-stu-id="c8586-115">A complete list of available keywords for filters is available [here](https://msdn.microsoft.com/library/azure/mt743622.aspx).</span></span>

<span data-ttu-id="c8586-116">Unterstützte Metriken pro Ressourcentyp sind [hier](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-supported-metrics) verfügbar.</span><span class="sxs-lookup"><span data-stu-id="c8586-116">Supported metrics per resource type is available [here](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-supported-metrics).</span></span>

```python
import datetime
from azure.mgmt.monitor import MonitorManagementClient

# Get the ARM id of your resource. You might chose to do a "get"
# using the according management or to build the URL directly
# Example for a ARM VM
resource_id = (
    "subscriptions/{}/"
    "resourceGroups/{}/"
    "providers/Microsoft.Compute/virtualMachines/{}"
).format(subscription_id, resource_group_name, vm_name)

# create client
client = MonitorManagementClient(
    credentials,
    subscription_id
)

# You can get the available metrics of this specific resource
for metric in client.metric_definitions.list(resource_id):
    # azure.monitor.models.MetricDefinition
    print("{}: id={}, unit={}".format(
        metric.name.localized_value,
        metric.name.value,
        metric.unit
    ))

# Example of result for a VM:
# Percentage CPU: id=Percentage CPU, unit=Unit.percent
# Network In: id=Network In, unit=Unit.bytes
# Network Out: id=Network Out, unit=Unit.bytes
# Disk Read Bytes: id=Disk Read Bytes, unit=Unit.bytes
# Disk Write Bytes: id=Disk Write Bytes, unit=Unit.bytes
# Disk Read Operations/Sec: id=Disk Read Operations/Sec, unit=Unit.count_per_second
# Disk Write Operations/Sec: id=Disk Write Operations/Sec, unit=Unit.count_per_second

# Get CPU total of yesterday for this VM, by hour

today = datetime.datetime.now().date()
yesterday = today - datetime.timedelta(days=1)

metrics_data = client.metrics.list(
    resource_id,
    timespan="{}/{}".format(yesterday, today),
    interval='PT1H',
    metric='Percentage CPU',
    aggregation='Total'
)

for item in metrics_data.value:
    # azure.mgmt.monitor.models.Metric
    print("{} ({})".format(item.name.localized_value, item.unit.name))
    for timeserie in item.timeseries:
        for data in timeserie.data:
            # azure.mgmt.monitor.models.MetricData
            print("{}: {}".format(data.time_stamp, data.total))

# Example of result:
# Percentage CPU (percent)
# 2016-11-16 00:00:00+00:00: 72.0
# 2016-11-16 01:00:00+00:00: 90.59
# 2016-11-16 02:00:00+00:00: 60.58
# 2016-11-16 03:00:00+00:00: 65.78
# 2016-11-16 04:00:00+00:00: 43.96
# 2016-11-16 05:00:00+00:00: 43.96
# 2016-11-16 06:00:00+00:00: 114.9
# 2016-11-16 07:00:00+00:00: 45.4
```

## <a name="example---alerts"></a><span data-ttu-id="c8586-117">Beispiel – Warnungen</span><span class="sxs-lookup"><span data-stu-id="c8586-117">Example - Alerts</span></span>
<span data-ttu-id="c8586-118">In diesem Beispiel wird gezeigt, wie Sie Warnungen für Ihre Ressourcen gleich bei der Erstellung automatisch einrichten, um sicherzustellen, dass alle Ressourcen ordnungsgemäß überwacht werden.</span><span class="sxs-lookup"><span data-stu-id="c8586-118">This example shows how to automatically set up alerts on your resources when they are created to ensure that all resources are monitored correctly.</span></span>

<span data-ttu-id="c8586-119">Erstellen Sie eine Datenquelle auf einem virtuellen Computer, um eine Warnung für die CPU-Nutzung auszugeben:</span><span class="sxs-lookup"><span data-stu-id="c8586-119">Create a data source on a VM to alert on CPU usage:</span></span>
```python
from azure.mgmt.monitor import MonitorMgmtClient
from azure.mgmt.monitor.models import RuleMetricDataSource

resource_id = (
    "subscriptions/{}/"
    "resourceGroups/MonitorTestsDoNotDelete/"
    "providers/Microsoft.Compute/virtualMachines/MonitorTest"
).format(self.settings.SUBSCRIPTION_ID)

# create client
client = MonitorMgmtClient(
    credentials,
    subscription_id
)

# I need a subclass of "RuleDataSource"
data_source = RuleMetricDataSource(
    resource_uri = resource_id,
    metric_name = 'Percentage CPU'
)
```
<span data-ttu-id="c8586-120">Erstellen Sie eine Schwellenwertbedingung, die ausgelöst wird, wenn die durchschnittliche CPU-Nutzung eines virtuellen Computers in den letzten fünf Minuten über 90 Prozent betrug (unter Verwendung der vorhergehenden Datenquelle):</span><span class="sxs-lookup"><span data-stu-id="c8586-120">Create a threshold condition that triggers when the average CPU usage of a VM for the last 5 minutes is above 90% (using the preceding data source):</span></span>
```python
from azure.mgmt.monitor.models import ThresholdRuleCondition

# I need a subclasses of "RuleCondition"
rule_condition = ThresholdRuleCondition(
    data_source = data_source,
    operator = 'GreaterThanOrEqual',
    threshold = 90,
    window_size = 'PT5M',
    time_aggregation = 'Average'
)
```

<span data-ttu-id="c8586-121">Erstellen einer E-Mail-Aktion:</span><span class="sxs-lookup"><span data-stu-id="c8586-121">Create an email action:</span></span>
```python
from azure.mgmt.monitor.models import RuleEmailAction

# I need a subclass of "RuleAction"
rule_action = RuleEmailAction(
    send_to_service_owners = True,
    custom_emails = [
        'monitoringemail@microsoft.com'
    ]
)
```

<span data-ttu-id="c8586-122">Erstellen der Warnungsregel:</span><span class="sxs-lookup"><span data-stu-id="c8586-122">Create the alert:</span></span>
```python
rule_name = 'MyPyTestAlertRule'
my_alert = client.alert_rules.create_or_update(
    group_name,
    rule_name,
    {
        'location': 'westus',
        'alert_rule_resource_name': rule_name,
        'description': 'Testing Alert rule creation',
        'is_enabled': True,
        'condition': rule_condition,
        'actions': [
            rule_action
        ]
    }
)
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="c8586-123">Informationen zu den Verwaltungs-APIs</span><span class="sxs-lookup"><span data-stu-id="c8586-123">Explore the Management APIs</span></span>](/python/api/overview/azure/monitoring/management)
