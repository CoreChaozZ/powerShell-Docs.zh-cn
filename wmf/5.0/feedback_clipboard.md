---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,安装程序
ms.openlocfilehash: d34a267bae7e48afe4442256d7f112da3a97eb7d
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2018
---
# <a name="clipboard-cmdlets"></a>剪贴板 cmdlet
通过 **Get-Clipboard** 和 **Set-Clipboard**，你可以更轻松地将内容传入和传出 Windows PowerShell 会话。 例如，如果你使用 Windows 资源管理器将三个文件复制到剪贴板（例如，通过选择它们并按 `ctrl-c`），然后就可以轻松地以文件列表的方式访问剪贴板的内容：

```powershell
PS C:\\&gt; Get-Clipboard -Format FileDropList

Directory: C:\\Users\\slee\\Downloads\\Example

Mode LastWriteTime Length Name

---- ------------- ------ ----

-a---- 4/14/2015 1:19 PM 0 File2.txt

-a---- 4/14/2015 1:19 PM 0 File3.txt

-a---- 4/14/2015 1:19 PM 0 File1.txt
```


剪贴板 cmdlet 支持图像、音频文件、文件列表和文本。