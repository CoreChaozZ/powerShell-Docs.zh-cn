---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,配置,安装程序
title: MSFT_DSCLocalConfigurationManager 类的 DisableDebugConfiguration 方法
ms.openlocfilehash: 9392a721a542c89be8794882a800b374f11ca5fd
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2018
---
# <a name="disabledebugconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>MSFT_DSCLocalConfigurationManager 类的 DisableDebugConfiguration 方法

禁用 DSC 资源调试。

<a name="syntax"></a>语法
------

```mof
uint32 DisableDebugConfiguration();
```

<a name="parameters"></a>参数
----------

此方法没有任何参数。

## <a name="return-value"></a>返回值
------------

如果成功，则返回零；否则返回错误代码。

## <a name="remarks"></a>备注

这是一种静态方法。

## <a name="requirements"></a>要求
------------
>**MOF：** DscCore.mof

>**命名空间**：Root\Microsoft\Windows\DesiredStateConfiguration


## <a name="see-also"></a>另请参阅


[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)