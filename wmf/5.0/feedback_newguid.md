---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,安装程序
ms.openlocfilehash: 91c115c7f0553cd5edf7fecf04e6a5c71c0a1aa2
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2018
---
# <a name="new-guid"></a>New-Guid
通常脚本（或写入 DSC 资源）需要唯一标识符。 GUID 使用效果良好，并且调用 .NET Framework Guid 类即可轻松生成 GUID，但使用 cmdlet 可让尚不熟悉 .NET Framework 类的终端用户更容易发现此操作：

PS C:\\&gt; New-Guid

Guid

----

e19d6ea5-3cc2-4db9-8095-0cdaed5a703d