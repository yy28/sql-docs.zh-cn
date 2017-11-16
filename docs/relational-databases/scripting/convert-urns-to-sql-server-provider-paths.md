---
title: "将 URN 转换为 SQL Server 提供程序路径 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c9b1b8f1-b117-4e87-9704-2170f62c5c8b
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: faef6d3756049ae24d2c48e5c7cbd1e73a267565
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="convert-urns-to-sql-server-provider-paths"></a>将 URN 转换为 SQL Server 提供程序路径
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理对象模型 (SMO) 为其对象生成统一资源名称 (URN)。 每个 URN 都唯一标识一个 SMO 对象，并且可通过使用 **Convert-UrnToPath** cmdlet 转换为 SQL Server PowerShell 提供程序路径。  
  
## <a name="converting-urns-to-paths"></a>将 URN 转换为路径  
 每个对象的 URN 都有与其路径相同的信息，但是它们的格式有所不同。 例如，下面是一个表的路径：  
  
 SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012\Tables\Person.Address  
  
 下面是同一个对象的 URN：  
  
 Server[@Name='MyComputer']\Database[@Name='AdventureWorks2012']\Table[@Name='Address' and @Schema='Person']  
  
 如果你已在 PowerShell 脚本中创建了一个 SMO 对象，则可以引用 **Urn** 属性以便获取该对象的 URN，然后使用 **Convert-UrnToPath** cmdlet 将 SMO URN 字符串转换为 Windows PowerShell 路径。 您然后可以使用该提供程序导航到路径上的不同位置。  
  
 如果节点名称中包含 Windows PowerShell 路径名称中不支持的扩展字符， **Convert-UrnToPath** 会用这些字符的十六进制表示形式来对它们进行编码。 例如，“My:Table”以“My%3ATable”形式返回。  
  
 有关在 Windows PowerShell 中使用 cmdlet 的示例，请运行：  
  
```  
Get-Help Convert-UrnToPath -Examples  
```  
  
## <a name="see-also"></a>另请参阅  
 [查询表达式和统一资源名称](../../powershell/query-expressions-and-uniform-resource-names.md)   
 [SQL Server PowerShell 提供程序](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
