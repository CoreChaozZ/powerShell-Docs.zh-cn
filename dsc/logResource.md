---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,配置,安装程序
title: DSC Log 资源
ms.openlocfilehash: f1a528767508d4a0e7f0ea2e58fd27a6a4d7ec75
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-log-resource"></a>DSC Log 资源

> 适用于：Windows PowerShell 4.0 和 Windows PowerShell 5.0

Windows PowerShell Desired State Configuration (DSC) 内的 __Log__ 资源提供了将消息写入 Microsoft-Windows-Desired State Configuration/Analytic 事件日志的机制。

```
Syntax

Log [string] #ResourceName
{
    Message = [string]
    [ DependsOn = [string[]] ]
}
```

注意：默认情况下，仅启用 DSC 的“操作”日志。
必须先启用“分析”日志才能看到或使用它。
请参阅以下文章。

[DSC 事件日志在哪里？](https://msdn.microsoft.com/en-us/powershell/dsc/troubleshooting#where-are-dsc-event-logs)

## <a name="properties"></a>“属性”
|  属性  |  说明   |
|---|---|
| 消息| 指示要写入 Microsoft-Windows-Desired State Configuration/Analytic 事件日志的消息。|
| DependsOn | 指示必须先运行其他资源的配置，再写入此日志消息。 例如，如果你想要首先运行 ID 为 __ResourceName__、类型为 __ResourceType__ 的资源配置脚本块，则使用此属性的语法为 `DependsOn = "[ResourceType]ResourceName"`。|

## <a name="example"></a>示例

下面的示例演示如何在 Microsoft-Windows-Desired State Configuration/Analytic 事件日志中纳入消息。

> **注意**：如果你在配置此资源后运行 [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx)，它将始终返回 **$false**。

```powershell
Configuration logResourceTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node localhost

    {
        Log LogExample
        {
            Message = "This message will appear in the Microsoft-Windows-Desired State Configuration/Analytic event log."
        }
    }
}
```