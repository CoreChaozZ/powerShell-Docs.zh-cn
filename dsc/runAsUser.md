---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,配置,安装程序
title: 使用用户凭据运行 DSC
ms.openlocfilehash: 37e6ff64c9c6d3960653d417e22a6c93c653230c
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2018
---
# <a name="running-dsc-with-user-credentials"></a>使用用户凭据运行 DSC

> 适用于：Windows PowerShell 5.0 和 Windows PowerShell 5.1

可以通过在配置中使用 **PsDscRunAsCredential** 属性，在指定的一组凭据之下运行 DSC 资源。
默认情况下，DSC 以系统帐户身份运行每个资源。
有时需要以用户身份运行，例如在特定用户上下文中安装 MSI 程序包、设置用户的注册表项、访问用户的特定本地目录或访问网络共享。

每个 DSC 资源都具有 **PsDscRunAsCredential** 属性，它可以设置为任何用户凭据（[PSCredential](https://msdn.microsoft.com/library/ms572524(v=VS.85).aspx) 对象）。
凭据可以硬编码为配置中属性的值，你也可以将值设置为 [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx)，这会在编译配置时提示用户输入凭据（有关编译配置的信息，请参阅[配置](configurations.md)）。

>**注意：**在 PowerShell 5.0 中，不支持在调用复合资源的配置中使用 **PsDscRunAsCredential** 属性。
>在 PowerShell 5.1 中，支持在调用复合资源的配置中使用 **PsDscRunAsCredential** 属性。

>**注意：****PsDscRunAsCredential** 属性在 PowerShell 4.0 中不可用。

在下面的示例中，**Get-Credential** 用于提示用户输入凭据。
[Registry](registryResource.md) 资源用于更改可指定 Windows 命令提示符窗口背景色的注册表项。

```powershell
Configuration ChangeCmdBackGroundColor
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node $AllNodes.NodeName
    {
        Registry CmdPath
        {
            Key                  = 'HKEY_CURRENT_USER\SOFTWARE\Microsoft\Command Processor'
            ValueName            = 'DefaultColor'
            ValueData            = '1F'
            ValueType            = 'DWORD'
            Ensure               = 'Present'
            Force                = $true
            Hex                  = $true
            PsDscRunAsCredential = Get-Credential
        }
    }
}

$configData = @{
    AllNodes = @(
        @{
            NodeName             = 'localhost';
            PSDscAllowDomainUser = $true
            CertificateFile      = 'C:\publicKeys\targetNode.cer'
            Thumbprint           = '7ee7f09d-4be0-41aa-a47f-96b9e3bdec25'
        }
    )
}

ChangeCmdBackGroundColor -ConfigurationData $configData
```
>**注意：**此示例假定你在 `C:\publicKeys\targetNode.cer` 上具有有效证书，并且该证书的指纹是显示的值。
>若要了解如何在 DSC 配置 MOF 文件中加密凭据，请参阅[保护 MOF 文件](secureMOF.md)。