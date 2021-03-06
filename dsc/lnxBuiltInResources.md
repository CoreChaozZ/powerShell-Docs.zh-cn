---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,配置,安装程序
title: 适用于 Linux 的内置 Desired State Configuration 资源
ms.openlocfilehash: 77617b72584f39c46fc4b9eb67235378bbfc19aa
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2018
---
# <a name="built-in-desired-state-configuration-resources-for-linux"></a>适用于 Linux 的内置 Desired State Configuration 资源

资源是可用于编写 PowerShell Desired State Configuration (DSC) 脚本的构建基块。 适用于 Linux 的 DSC 附带了一套用于配置资源（如文件和文件夹、程序包、环境变量、服务和进程）的内置功能。

## <a name="built-in-resources"></a>内置资源

下表提供了关于主题的资源和链接列表，其中进行了详细介绍。

* [nxArchive 资源](lnxArchiveResource.md)--提供了用于在特定路径解压存档文件（.tar、.zip）的机制。
* [nxEnvironment 资源](lnxEnvironmentResource.md)--管理目标节点上的环境变量。
* [nxFile 资源](lnxFileResource.md)--管理 Linux 文件和目录。
* [nxFileLine 资源](lnxFileLineResource.md)--管理 Linux 文件中的各个行。
* [nxGroup 资源](lnxGroupResource.md)--管理本地 Linux 组。
* [nxPackage 资源](lnxPackageResource.md) - 管理 Linux 节点上的包。
* [nxScript 资源](lnxScriptResource.md) - 在目标节点上运行脚本。
* [nxService 资源](lnxServiceResource.md)--管理 Linux 服务（守护程序）。
* [nxSshAuthorizedKeys 资源](lnxSshAuthorizedKeysResource.md)--为 Linux 用户管理公共 ssh 密钥。
* [nxUser 资源](lnxUserResource.md)--管理本地 Linux 用户。