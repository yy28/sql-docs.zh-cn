---
title: 使用 SQL Server PowerShell 路径 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f31d8e2c-8d59-4fee-ac2a-324668e54262
caps.latest.revision: 10
author: mgblythe
ms.author: mblythe
manager: jhubbard
ms.openlocfilehash: 7a0f936daca1683c4aeb54e01c8b8cb567d145c3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025483"
---
# <a name="work-with-sql-server-powershell-paths"></a>使用 SQL ServerPowerShell 路径
  在您导航到 [!INCLUDE[ssDE](../includes/ssde-md.md)] 提供程序路径中的某一节点后，可通过使用与该节点相关联的 [!INCLUDE[ssDE](../includes/ssde-md.md)] 管理对象中的方法和属性，执行工作或检索信息。  
  
1.  [开始之前](#BeforeYouBegin)  
  
2.  **To work on a path node:**  [Listing Methods and Properties](#ListPropMeth), [Using Methods and Properties](#UsePropMeth)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
 在导航到 [!INCLUDE[ssDE](../includes/ssde-md.md)] 提供程序路径中的节点之后，可以执行两种类型的操作：  
  
-   可以运行作用于节点的 Windows PowerShell cmdlet，如 **Rename-Item**。  
  
-   可以调用相关联的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理对象模型中的方法，如 SMO。 例如，如果你导航到路径中的 Databases 节点，则可以使用 <xref:Microsoft.SqlServer.Management.Smo.Database> 类的方法和属性。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供程序用于管理 [!INCLUDE[ssDE](../includes/ssde-md.md)]实例中的对象， 而不能用于处理数据库中的数据。 如果您已经导航到表或视图，则不能使用该提供程序选择、插入、更新或删除数据。 可以使用 **Invoke-Sqlcmd** cmdlet 来查询或更改 Windows PowerShell 环境内表和视图中的数据。 有关详细信息，请参阅 [Invoke-Sqlcmd cmdlet](../database-engine/invoke-sqlcmd-cmdlet.md)。  
  
##  <a name="ListPropMeth"></a> 列出方法和属性  
 **列出方法和属性**  
  
 若要查看可供特定对象或对象类使用的方法和属性，请使用 **Get-Member** cmdlet。  
  
### <a name="examples-listing-methods-and-properties"></a>示例：列出方法和属性  
 下面的示例将 Windows PowerShell 变量设置为 SMO <xref:Microsoft.SqlServer.Management.Smo.Database> 类并列出其方法和属性：  
  
```  
$MyDBVar = New-Object Microsoft.SqlServer.Management.SMO.Database  
$MyDBVar | Get-Member –Type Methods  
$MyDBVar | Get-Member -Type Properties  
```  
  
 还可以使用 **Get-Member** 列出与 Windows PowerShell 路径的结束节点相关联的方法和属性。  
  
 下面的示例导航到 SQLSERVER: 路径中的 Databases 节点，并列出集合属性：  
  
```  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases  
Get-Item . | Get-Member -Type Properties  
```  
  
 下面的示例导航到 SQLSERVER: 路径中的 AdventureWorks2012 节点，并列出对象属性：  
  
```  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012  
Get-Item . | Get-Member -Type Properties  
```  
  
##  <a name="UsePropMeth"></a> 使用方法和属性  
 **使用 SMO 方法和属性**  
  
 若要从 [!INCLUDE[ssDE](../includes/ssde-md.md)] 提供程序路径对对象执行操作，您可以使用 SMO 方法和属性。  
  
### <a name="examples-using-methods-and-properties"></a>示例：使用方法和属性  
 下面的示例使用 SMO **Schema** 属性，从 AdventureWorks2012 中的 Sales 架构中获取表的列表：  
  
```  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012\Tables  
Get-ChildItem | where {$_.Schema -eq "Sales"}  
```  
  
 此示例使用 SMO**脚本**方法来生成脚本，其中包含`CREATE VIEW`必须重新创建 AdventureWorks2012 中的视图的语句：  
  
```  
Remove-Item C:\PowerShell\CreateViews.sql  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012\Views  
foreach ($Item in Get-ChildItem) { $Item.Script() | Out-File -Filepath C:\PowerShell\CreateViews.sql -append }  
```  
  
 下面的示例使用 SMO **Create** 方法创建一个数据库，然后使用 **State** 属性显示该数据库是否存在：  
  
```  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases  
$MyDBVar = New-Object Microsoft.SqlServer.Management.SMO.Database  
$MyDBVar.Parent = (Get-Item ..)  
$MyDBVar.Name = "NewDB"  
$MyDBVar.Create()  
$MyDBVar.State  
```  
  
## <a name="see-also"></a>请参阅  
 [SQL Server PowerShell Provider](sql-server-powershell-provider.md)   
 [导航 SQL ServerPowerShell 路径](navigate-sql-server-powershell-paths.md)   
 [将 URN 转换为 SQL Server 提供程序路径](../database-engine/convert-urns-to-sql-server-provider-paths.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  