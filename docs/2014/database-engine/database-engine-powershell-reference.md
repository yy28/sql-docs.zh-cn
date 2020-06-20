---
title: 数据库引擎 PowerShell 参考 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3c379a43-c497-47dd-8e7d-2b015c068bb7
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 5412b8a96f79f0c33206c794090916732ef016a8
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934460"
---
# <a name="database-engine-powershell-reference"></a>数据库引擎 PowerShell 参考
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 包含一组 Windows PowerShell 2.0 cmdlet，用于在[!INCLUDE[ssDE](../includes/ssde-md.md)]中执行常见操作。 此外，查询表达式和统一资源名称 (URN) 可以转换为 SQL Server PowerShell 路径，或用于指定 [!INCLUDE[ssDE](../includes/ssde-md.md)]中的一个或多个对象。  
  
## <a name="database-engine-cmdlets"></a>数据库引擎 Cmdlet  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 包含相对较少的用于 [!INCLUDE[ssDE](../includes/ssde-md.md)]的 cmdlet。 大多数用于 [!INCLUDE[ssDE](../includes/ssde-md.md)] 的 PowerShell 脚本使用 SQL Server PowerShell 提供程序和可管理性对象模型。 有关详细信息，请参阅 [SQL Server PowerShell Provider](../powershell/sql-server-powershell-provider.md)。  
  
 要了解如何获取有关 Windows PowerShell 环境中的 SQL Server cmdlet 的帮助，请参阅 [Get Help SQL Server PowerShell](../powershell/sql-server-powershell.md)。  
  
### <a name="in-this-section"></a>本节内容  
 本节包含有关这些 cmdlet 的信息。  
  
|说明|Cmdlet|  
|-----------------|------------|  
|运行 Transact-SQL 和 XQuery 脚本，如可以使用 `sqlcmd` 实用工具运行的脚本。|[Invoke-Sqlcmd cmdlet](../../2014/database-engine/invoke-sqlcmd-cmdlet.md)|  
|评估数据库引擎对象是否符合基于策略的管理策略。|[Invoke-PolicyEvaluation cmdlet](../../2014/database-engine/invoke-policyevaluation-cmdlet.md)|  
  
### <a name="information-about-other-cmdlets"></a>有关其他 Cmdlet 的信息  
 `Encode-Sqlname` 和 `Decode-Sqlname` cmdlet 帮助您指定包含 PowerShell 路径中不支持的字符的 SQL Server 标识符。 有关详细信息，请参阅 [SQL Server Identifiers in PowerShell](../powershell/sql-server-identifiers-in-powershell.md)。  
  
 使用 `Convert-UrnToPath` cmdlet 将[!INCLUDE[ssDE](../includes/ssde-md.md)]对象的统一资源名称转换为 SQL Server PowerShell 提供程序的路径。 有关详细信息，请参阅 [Convert URNs to SQL Server Provider Paths](../../2014/database-engine/convert-urns-to-sql-server-provider-paths.md)。  
  
## <a name="query-expressions-and-unique-resource-names"></a>查询表达式和唯一资源名称  
 查询表达式是使用与 XPath 类似的语法指定一组条件的字符串，用于枚举对象模型层次结构中的一个或多个对象。 唯一资源名称 (URN) 是一种特定类型的查询表达式字符串，用于唯一标识单个对象。 有关详细信息，请参阅 [Query Expressions and Uniform Resource Names](../powershell/query-expressions-and-uniform-resource-names.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)  
  
  
