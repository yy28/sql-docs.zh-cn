---
title: "下载 SQL Server PowerShell 模块 | Microsoft Docs"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "安装 sql server powershell, 下载 sql server powershell"
ms.assetid: 
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: b68d454230d414ff52d90b4f3f71dd68ee65c6bc
ms.openlocfilehash: f55266b6ec28e2552047cc36a5060945006b2caa
ms.contentlocale: zh-cn
ms.lasthandoff: 07/31/2017

---
# <a name="download-sql-server-powershell-module"></a>下载 SQL Server PowerShell 模块
SQL Server PowerShell 模块是 17.0 版本 SQL Server Management Studio 的一部分，现通过 PowerShell 库提供。  该模块不再随附在 SSMS 安装包中。 若要将 PowerShell 与 SSMS 17.0 及更新版本配合使用，必须执行额外步骤 - 在计算机上安装 SQL Server 模块。

有关安装最新版本 Windows Management Framework 和安装 PowerShell 模块的常规方法的完整文档，请在 [PowerShell 库](https://www.powershellgallery.com/)网站中查找。

用于安装 SQL Server 模块的 PowerShell 命令为：

> Install-module -Name SqlServer -Scope CurrentUser

如果计算机上存在以前版本的 SQL Server PowerShell 模块，可能需要提供“-AllowClobber”参数。  

PowerShell 库随附的 SQL Server PowerShell 模块版本支持版本控制，并且要求 PowerShell 5.0 或更高版本。

