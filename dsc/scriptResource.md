---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,配置,安装程序
title: DSC Script 资源
ms.openlocfilehash: 6a39fbd914f9a0bb0f192b7b1f81f404bb6b93c1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-script-resource"></a>DSC Script 资源


> 适用于：Windows PowerShell 4.0 和 Windows PowerShell 5.0

Windows PowerShell Desired State Configuration (DSC) 中的 **Script** 资源提供了在目标节点上运行 Windows PowerShell 脚本的机制。 `Script` 资源具有 `GetScript`、`SetScript` 和 `TestScript` 属性。 应将这些属性设置为将在每个目标节点上运行的脚本块。

`GetScript` 脚本块应返回表示当前节点状态的哈希表。 哈希表必须只包含一个键 `Result`，并且值必须属于 `String` 类型。 它不需要返回任何内容。 DSC 不与此脚本块的输出执行任何操作。

`TestScript` 脚本块应确定当前节点是否需要进行修改。 如果节点是最新的，它应返回 `$true`。 如果节点的配置已过期，它应返回 `$false`，并且应使用 `SetScript` 脚本块进行更新。 `TestScript` 脚本块由 DSC 调用。

`SetScript` 脚本块应修改该节点。 如果 `TestScript` 块返回 `$false`，则其由 DSC 调用。

如果需要从 `GetScript`、`TestScript` 或者 `SetScript` 脚本块内的配置脚本使用变量，请使用 `$using:` 作用域（参见以下内容为例）。


## <a name="syntax"></a>语法

```
Script [string] #ResourceName
{
    GetScript = [string]
    SetScript = [string]
    TestScript = [string]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a>“属性”

|  属性  |  说明   |
|---|---|
| GetScript| 提供调用 [Get-DscConfiguration](https://technet.microsoft.com/library/dn407379.aspx) cmdlet 时运行的 Windows PowerShell 脚本块。 此块必须返回一个哈希表。 哈希表必须只包含一个键 **Result**，并且值必须属于 **String** 类型。|
| SetScript| 提供 Windows PowerShell 脚本块。 调用 [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) cmdlet 时，将首先运行 **TestScript** 块。 如果 **TestScript** 块返回 **$false**，则将运行 **SetScript** 块。 如果 **TestScript** 块返回 **$true**，**SetScript** 块将不会运行。|
| TestScript| 提供 Windows PowerShell 脚本块。 调用 [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) cmdlet 时，将运行此块。 如果它返回 **$false**，将运行 SetScript 块。 如果它返回 **$true**，将不运行 SetScript 块。 调用 [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) cmdlet 时，也将运行 **TestScript** 块。 但是，在这种情况下，无论 TestScript 返回何值，都不会运行 **SetScript**。 如果实际配置与当前所需状态配置相匹配，**TestScript** 块必返回 True，如果不匹配，则返回 False。 （当前所需状态配置是在使用 DSC 的节点上执行的最后一个配置。）|
| 凭据| 指示要用于运行此脚本的凭据（如果需要凭据）。|
| DependsOn| 指示必须先运行其他资源的配置，再配置此资源。 例如，如果你想要首先运行 ID 为 **ResourceName**、类型为 **ResourceType** 的资源配置脚本块，则使用此属性的语法为 `DependsOn = "[ResourceType]ResourceName"`。

## <a name="example-1"></a>示例 1
```powershell
Configuration ScriptTest
{
    Import-DscResource –ModuleName 'PSDesiredStateConfiguration'

    Script ScriptExample
    {
        SetScript =
        {
            $sw = New-Object System.IO.StreamWriter("C:\TempFolder\TestFile.txt")
            $sw.WriteLine("Some sample string")
            $sw.Close()
        }
        TestScript = { Test-Path "C:\TempFolder\TestFile.txt" }
        GetScript = { @{ Result = (Get-Content C:\TempFolder\TestFile.txt) } }
    }
}
```

## <a name="example-2"></a>示例 2
```powershell
$version = Get-Content 'version.txt'

Configuration ScriptTest
{
    Import-DscResource –ModuleName 'PSDesiredStateConfiguration'

    Script UpdateConfigurationVersion
    {
        GetScript = {
            $currentVersion = Get-Content (Join-Path -Path $env:SYSTEMDRIVE -ChildPath 'version.txt')
            return @{ 'Result' = "$currentVersion" }
        }
        TestScript = {
            $state = $GetScript
            if( $state['Result'] -eq $using:version )
            {
                Write-Verbose -Message ('{0} -eq {1}' -f $state['Result'],$using:version)
                return $true
            }
            Write-Verbose -Message ('Version up-to-date: {0}' -f $using:version)
            return $false
        }
        SetScript = {
            $using:version | Set-Content -Path (Join-Path -Path $env:SYSTEMDRIVE -ChildPath 'version.txt')
        }
    }
}
```

此资源正在将配置的版本写入文本文件。 此版本在客户端计算机上可用，但不在任何节点上，因此必须通过 PowerShell 的 `using` 作用域将其传递到每个 `Script` 资源的脚本块。 生成节点的 MOF 文件时，将从客户端计算机上的文本文件读取 `$version` 变量的值。 DSC 将每个脚本块中的 `$using:version` 变量替换为 `$version` 变量的值。