---
ms.date: 06/05/2017
keywords: powershell,cmdlet
title: Windows PowerShell ISE 简介
ms.openlocfilehash: b09e64d0258d11f1f16f96b319ef232ebdfa0c49
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2018
---
# <a name="introducing-the-windows-powershell-ise"></a>Windows PowerShell ISE 简介

Windows PowerShell 集成脚本环境 (ISE) 是 Windows PowerShell 的主机应用程序。 在 Windows PowerShell ISE 中，你可以在单个基于 Windows 的图形用户界面（包含多行编辑、Tab 自动补全、语法颜色设置、选择性执行、上下文相关帮助以及从右向左语言支持功能）中运行命令并编写、测试和调试脚本。 你可以使用菜单项和键盘快捷方式执行许多将会在 Windows PowerShell 控制台中执行的相同任务。 例如，当你在 Windows PowerShell ISE 中调试脚本以在脚本中设置行断点时，右键单击代码行，然后单击**切换断点**。

尝试 Windows PowerShell ISE 中的这些功能。

- 多行编辑：若要在“命令”窗格中的当前行下插入一个空行，请按 SHIFT+ENTER。
- 选择性执行：若要运行部分脚本，请选择要运行的文本，然后单击“运行脚本”按钮。 或者，按 F5。
- 上下文相关帮助：键入 **Invoke-Item**，然后按 F1。 帮助文件将打开到 **Invoke-Item** cmdlet 的帮助主题。

Windows PowerShell ISE 允许你自定义其外观的某些方面。 它还具有自己的 Windows PowerShell 配置文件，你可以在其中存储在 Windows PowerShell ISE 中使用的函数、别名、变量和命令。

## <a name="to-start-the-windows-powershell-ise"></a>启动 Windows PowerShell ISE

执行下列操作之一：

- 单击“开始”，依次指向“所有程序”和“Windows PowerShell V2”，然后单击 **Windows PowerShell ISE**。
- 在 Windows PowerShell console Cmd.exe 或“运行”框中，键入 **powershell_ise.exe**。

## <a name="to-get-help-in-the-windows-powershell-ise"></a>在 Windows PowerShell ISE 中获取帮助

在“帮助”菜单上，单击“Windows PowerShell 帮助”。 或者，按 F1。 打开的文件介绍了 Windows PowerShell ISE 和 Windows PowerShell，其中包括 Get-Help cmdlet 中提供的所有帮助。