---
title: "下载 SQL Server PowerShell 模块 | Microsoft Docs"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
keywords: "安装 sql server powershell, 下载 sql server powershell"
ms.assetid: 
caps.latest.revision: "113"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 208bf291819a3e847e784e76611acdec0bf2f2d0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="download-sql-server-powershell-module"></a>下载 SQL Server PowerShell 模块
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]SQL Server PowerShell 模块是 17.0 版本 SQL Server Management Studio 的一部分，现通过 PowerShell 库提供。  该模块不再随附在 SSMS 安装包中。 若要将 PowerShell 与 SSMS 17.0 及更新版本配合使用，必须执行额外步骤 - 在计算机上安装 SQL Server 模块。

有关安装最新版本 Windows Management Framework 和安装 PowerShell 模块的常规方法的完整文档，请在 [PowerShell 库](https://www.powershellgallery.com/)网站中查找。

用于安装 SQL Server 模块的 PowerShell 命令为：

> Install-Module -Name SqlServer

此命令将为计算机的所有用户安装该模块。 需要以管理员身份运行 PowerShell 进程。

> Install-Module -Name SqlServer -Scope CurrentUser

此命令将为运行当前 PowerShell 进程的用户安装模块。 不需要以管理员权限运行 PowerShell 进程。

如果计算机上存在以前版本的 SQL Server PowerShell 模块，可能需要提供“-AllowClobber”参数。  

如果以管理员身份运行或者为计算机的所有用户安装模块

> Install-Module -Name SqlServer -AllowClobber

如果不能以管理员身份运行或者仅为当前用户安装

> Install-Module -Name SqlServer -Scope CurrentUser -AllowClobber

当 SqlServer 模块的更新版本可用时，你将能够使用 Update-Module 命令更新版本

> Update-Module -Name SqlServer

查看你可以使用的计算机上安装的模块版本

> Get-Module SqlServer -ListAvailable

在可以使用其导入的脚本中使用模块的特定版本

> Import-Module SqlServer -Version 21.0.17178

PowerShell 库随附的 SQL Server PowerShell 模块版本支持版本控制，并且要求 PowerShell 5.0 或更高版本。 你可以在 [PowerShell 库](https://www.powershellgallery.com/packages/Sqlserver/)上找到 SqlServer 模块 
