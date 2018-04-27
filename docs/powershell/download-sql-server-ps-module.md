---
title: 下载 SQL Server PowerShell 模块 | Microsoft Docs
ms.custom: ''
ms.date: 01/05/2018
ms.prod: sql
ms.prod_service: powershell
ms.service: ''
ms.component: powershell
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
keywords:
- 安装 sql server powershell, 下载 sql server powershell
ms.assetid: ''
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: 12d4e52940e704d5cca38e490b2b975c03827d4c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="install-sql-server-powershell-module"></a>安装 SQL Server PowerShell 模块
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

本文提供安装 SqlServer PowerShell 模块的指导。

> [!NOTE]
> SQL Server PowerShell 模块有两种；SqlServer 和 SQLPS。 虽然 SQL Server 安装附带了 SQLPS 模块（用于向后兼容），但该模块不再更新。 最新的 PowerShell 模块是 SqlServer 模块。 SqlServer 模块不仅包含 SQLPS 更新版本的 cmdlet，并且还包含新的 cmdlet 以支持最新的 SQL 功能。 虽然 SQL Server Management Studio (SSMS) 随附了以前版本的 SqlServer 模块，但仅限 16.x 版本的 SSMS。 要在 SSMS 17.0 和更高版本中使用 PowerShell，则必须从 PowerShell 库安装 SqlServer 模块。

要从 PowerShell 库安装 SqlServer 模块，请启用 [PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting) 会话并使用以下命令。 如果在安装过程中出现问题，请参阅[安装模块文档](https://docs.microsoft.com/powershell/gallery/psget/module/psget_install-module)和[安装模块参考](https://docs.microsoft.com/powershell/module/powershellget/Install-Module)。

安装 SqlServer 模块：

```Install-Module -Name SqlServer```

如果计算机上有以前版本的 SqlServer 模块，则可使用 `Update-Module`（后文有述）或提供 `-AllowClobber` 参数：  

```Install-Module -Name SqlServer -AllowClobber```

如果不能以管理员身份运行 PowerShell 会话，则可为当前用户安装：

```Install-Module -Name SqlServer -Scope CurrentUser```

当 SqlServer 模块的更新版本可用时，可使用 `Update-Module` 更新版本：

```Update-Module -Name SqlServer```

查看已安装模块的版本：

```Get-Module SqlServer -ListAvailable```

要使用特定版本的模块，可以使用类似以下形式的特定版本号将其导入：

```Import-Module SqlServer -Version 21.0.17178```


PowerShell 库中这些版本的 SqlServer 模块支持版本控制并且要求 PowerShell 5.0 或更高版本。 

* [PowerShell 库中的 SqlServer 模块](https://www.powershellgallery.com/packages/Sqlserver) 
* [SqlServer cmdlet](https://docs.microsoft.com/powershell/module/sqlserver)
* [SQLPS cmdlet](https://docs.microsoft.com/powershell/module/sqlps)
