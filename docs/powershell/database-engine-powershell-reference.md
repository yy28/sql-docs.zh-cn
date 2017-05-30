---
title: "数据库引擎 PowerShell 参考 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3c379a43-c497-47dd-8e7d-2b015c068bb7
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dc3df1d697b05201ac48520c1e344c28648cdfaf
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="database-engine-powershell-reference"></a>数据库引擎 PowerShell 参考
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 包含一组 Windows PowerShell cmdlet，用于在 [!INCLUDE[ssDE](../includes/ssde-md.md)]中执行常见操作。 此外，查询表达式和统一资源名称 (URN) 可以转换为 SQL Server PowerShell 路径，或用于指定 [!INCLUDE[ssDE](../includes/ssde-md.md)]中的一个或多个对象。  
  
## <a name="database-engine-cmdlets"></a>数据库引擎 Cmdlet  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 包含相对较少的用于 [!INCLUDE[ssDE](../includes/ssde-md.md)]的 cmdlet。 大多数用于 [!INCLUDE[ssDE](../includes/ssde-md.md)] 的 PowerShell 脚本使用 SQL Server PowerShell 提供程序和可管理性对象模型。 有关详细信息，请参阅 [SQL Server PowerShell Provider](../relational-databases/scripting/sql-server-powershell-provider.md)。  
  
 要了解如何获取有关 Windows PowerShell 环境中的 SQL Server cmdlet 的帮助，请参阅 [Get Help SQL Server PowerShell](../relational-databases/scripting/get-help-sql-server-powershell.md)。  
  
### <a name="in-this-section"></a>本节内容  
 本节包含有关这些 cmdlet 的信息。  
  
|说明|Cmdlet|  
|-----------------|------------|  
|运行 Transact-SQL 和 XQuery 脚本，如可以使用 **sqlcmd** 实用工具运行的脚本。|[Invoke-Sqlcmd cmdlet](../powershell/invoke-sqlcmd-cmdlet.md)|  
|评估数据库引擎对象是否符合基于策略的管理策略。|[Invoke-PolicyEvaluation cmdlet](../powershell/invoke-policyevaluation-cmdlet.md)|  
  
### <a name="information-about-other-cmdlets"></a>有关其他 Cmdlet 的信息  
 **Encode-Sqlname** 和 **Decode-Sqlname** cmdlet 帮助你指定包含 PowerShell 路径中不支持的字符的 SQL Server 标识符。 有关详细信息，请参阅 [SQL Server Identifiers in PowerShell](../relational-databases/scripting/sql-server-identifiers-in-powershell.md)。  
  
 使用 **Convert-UrnToPath** cmdlet 将 [!INCLUDE[ssDE](../includes/ssde-md.md)] 对象的统一资源名称转换为 SQL Server PowerShell 提供程序的路径。 有关详细信息，请参阅 [Convert URNs to SQL Server Provider Paths](../relational-databases/scripting/convert-urns-to-sql-server-provider-paths.md)。  
  
## <a name="query-expressions-and-unique-resource-names"></a>查询表达式和唯一资源名称  
 查询表达式是使用与 XPath 类似的语法指定一组条件的字符串，用于枚举对象模型层次结构中的一个或多个对象。 唯一资源名称 (URN) 是一种特定类型的查询表达式字符串，用于唯一标识单个对象。 有关详细信息，请参阅 [Query Expressions and Uniform Resource Names](../powershell/query-expressions-and-uniform-resource-names.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)  
  
  
