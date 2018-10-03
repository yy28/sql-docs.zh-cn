---
title: 管理 Tab 填写功能 (SQL Server PowerShell) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 6296848a-890f-4ad3-8d9f-92ed6a79aa00
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: afe3a53c3bc6208bc723ec5f30afc6f8add1f46a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47762525"
---
# <a name="manage-tab-completion-sql-server-powershell"></a>管理 Tab 填写功能 (SQL Server PowerShell)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]


[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 管理单元引入了三个变量 (**$SqlServerMaximumTabCompletion**、 **$SqlServerMaximumChildItems**和 **$SqlServerIncludeSystemObjects**) 来控制 Windows PowerShell Tab 补全。 Tab 填写功能通过返回名称以您正在键入的字符串开头的项目的表，而减少了必须键入的内容量。  

> [!NOTE]
> SQL Server PowerShell 模块有两种；SqlServer 和 SQLPS。 虽然 SQL Server 安装附带了 SQLPS 模块（用于向后兼容），但该模块不再更新。 最新的 PowerShell 模块是 SqlServer 模块。 SqlServer 模块不仅包含 SQLPS 更新版本的 cmdlet，并且还包含新的 cmdlet 以支持最新的 SQL 功能。  
> 虽然 SQL Server Management Studio (SSMS) 随附了以前版本的 SqlServer 模块，但仅限 16.x 版本的 SSMS。 要在 SSMS 17.0 和更高版本中使用 PowerShell，则必须从 PowerShell 库安装 SqlServer 模块。
> 要安装 SqlServer 模块，请参阅[安装 SQL Server PowerShell](download-sql-server-ps-module.md)。
  
使用 Windows PowerShell 的 Tab 填写功能，在键入路径或 cmdlet 名称的一部分之后，可以按 Tab 键获得其名称与已键入内容相匹配的项列表。 之后，可以从该列表中选择所需的项，而不必键入该名称的其余部分。  
  
如果正在处理的数据库中包含大量对象，则 Tab 自动补全列表可能会变得非常大。 某些 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 对象类型（如视图）也具有大量系统对象。  
  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理单元引入了三个可用来控制由 Tab 补全和 **Get-ChildItem**所提供的信息量的系统变量。  
  
 **$SqlServerMaximumTabCompletion =** *n*  
 指定要包括在 Tab 填写列表中的对象的最大数量。 如果你在具有多于 *n* 个对象的路径节点处选择 Tab，则 Tab 补全列表会在 *n*处被截断。 *n* 为整数。 默认设置为 0，表示对所列出对象的数量没有限制。  
  
 **$SqlServerMaximumChildItems =** *n*  
 指定由 **Get-ChildItem**显示的对象的最大数量。 如果在具有多于 **n** 个对象的路径节点处运行 *Get-ChildItem* ，则该列表会在 *n*处被截断。 *n* 为整数。 默认设置为 0，表示对所列出对象的数量没有限制。  
  
 **$SqlServerIncludeSystemObjects =** { **$True** | **$False** }  
 如果为 **$True**，则 Tab 补全和 **Get-ChildItem**将显示系统对象。 如果为 **$False**，则将不显示系统对象。 默认设置为 **$False**。  
  
## <a name="set-the-sql-server-tab-completion-variables"></a>设置 SQL Server 的 Tab 填写变量  
 对于您要更改其默认值的任何变量，将该变量设置为新值。  
  
### <a name="example-powershell"></a>示例 (PowerShell)  
 以下示例将对所有三个变量进行设置并列出其设置：  
  
```  
$SqlServerMaximumTabCompletion = 20  
$SqlServerMaximumChildItems = 10  
$SqlServerIncludeSystemObjects = $False  
dir variable:sqlserver*  
```  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
