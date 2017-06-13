---
title: "下载 SQL Server PowerShell 模块 |Microsoft 文档"
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
- "安装 sql server powershell，请下载 sql server powershell"
ms.assetid: 
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: b68d454230d414ff52d90b4f3f71dd68ee65c6bc
ms.openlocfilehash: f55266b6ec28e2552047cc36a5060945006b2caa
ms.contentlocale: zh-cn
ms.lasthandoff: 04/26/2017

---
# <a name="download-sql-server-powershell-module"></a>下载 SQL Server PowerShell 模块
作为 17.0 版本的 SQL Server Management Studio 的一部分，SQL Server PowerShell 模块现在提供通过 PowerShell 库。  SSMS 安装包中不再包含该模块。 若要使用 SSMS 17.0 和更高版本，请使用 PowerShell，SQL Server 模块必须安装在计算机上作为附加步骤。

完整有关安装 Windows Management Framework 的最新版本的文档和如何安装 PowerShell 模块一般情况下找不到上[PowerShell 库](https://www.powershellgallery.com/)站点。

PowerShell 命令来安装 SQL Server 模块是：

> 安装模块的名称 SqlServer-CurrentUser 作用域

如果存在以前版本的计算机上的 SQL Server PowerShell 模块，可能需要提供"-AllowClobber"参数。  

传送到 PowerShell 库的 SQL Server PowerShell 模块的版本支持版本控制，并要求 PowerShell 5.0 或更高版本。

