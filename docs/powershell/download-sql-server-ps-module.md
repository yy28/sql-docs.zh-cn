---
title: 下载 SQL Server PowerShell 模块 | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
keywords:
- 安装 sql server powershell, 下载 sql server powershell
ms.assetid: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f0f14a3cee050fff07c7fe5bc2467bcb8209a53c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62672577"
---
# <a name="install-sql-server-powershell-module"></a>安装 SQL Server PowerShell 模块
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

本文提供安装 SqlServer  PowerShell 模块的指导。
> [!NOTE]
> 提供两种 SQL Server PowerShell 模块： 
> * **SQLPS**：此模块随附于 SQL Server 安装（用于实现后向兼容性），但不再更新。 最新的 PowerShell 模块是 SqlServer 模块  。
> * **SqlServer**：此模块包括新的 cmdlet，用于支持最新的 SQL 功能。 该模块还包含 SQLPS 中 cmdlet 的更新版本  。 

虽然 SQL Server Management Studio (SSMS) 随附了以前版本的 SqlServer 模块，但仅限 16.x 版本的 SSMS   。 要在 SSMS 17.0 和更高版本中使用 PowerShell，则必须从 [PowerShell 库](https://www.powershellgallery.com/packages/Sqlserver)安装 SqlServer 模块  。
“SqlServer”模块的当前版本为 21.1.18080  。 这基于 Microsoft.SQLServer.SMO 的 v150 版本，并支持下一版本的 SQL Server。 基于 Microsoft.SQLServer.SMO 版本 v140 模块的最新版本是 21.0.17279。

模块的预发布版本可能会被更频繁地使用：请参阅本页底部部分，了解如何获得此类模块的版本。

要从 PowerShell 库安装 SqlServer  模块，请启用 [PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting) 会话并使用以下命令。 如果在安装过程中出现问题，请参阅[安装模块文档](https://docs.microsoft.com/powershell/gallery/psget/module/psget_install-module)和[安装模块参考](https://docs.microsoft.com/powershell/module/powershellget/Install-Module)。

安装 SqlServer 模块  ：

```Install-Module -Name SqlServer```

如果计算机上有以前版本的 SqlServer 模块，则可使用 `Update-Module`（后文有述）或提供 `-AllowClobber` 参数  ：  

```Install-Module -Name SqlServer -AllowClobber```

如果不能以管理员身份运行 PowerShell 会话，则可为当前用户安装：

```Install-Module -Name SqlServer -Scope CurrentUser```

当 SqlServer 模块的更新版本可用时，可使用 `Update-Module` 更新版本  ：

```Update-Module -Name SqlServer```

查看已安装模块的版本：

```Get-Module SqlServer -ListAvailable```

要使用特定版本的模块，可以使用类似以下形式的特定版本号将其导入：

```Import-Module SqlServer -Version 21.1.18080```

> [!NOTE]
> PowerShell 库中可能提供模块的预发行（或“预览”）版本。 可通过传递 -AllowPrerelease 切换，使用更新后的 Find-Module 和 Install-Module cmdlet（属于 [PowerShellGet](https://www.powershellgallery.com/packages/PowerShellGet) 模块）找到并安装这些版本。   
>
> 若要找到模块的预发行/预览版本，可运行以下命令：
>
> ```Find-Module SqlServer -AllowPrerelease```
>
> 若要安装模块的特定预发行/预览版本，可使用特定版本号进行安装，命令如下：
>
> ```Install-Module SqlServer -RequiredVersion 21.1.18040-preview -AllowPrerelease```
> 

PowerShell 库中这些版本的 SqlServer  模块支持版本控制并且要求 PowerShell 5.0 或更高版本。 

* [PowerShell 库中的 SqlServer 模块](https://www.powershellgallery.com/packages/Sqlserver) 
* [SqlServer cmdlet](https://docs.microsoft.com/powershell/module/sqlserver)
* [SQLPS cmdlet](https://docs.microsoft.com/powershell/module/sqlps)
