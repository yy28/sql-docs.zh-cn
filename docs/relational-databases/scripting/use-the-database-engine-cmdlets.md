---
title: "使用数据库引擎 cmdlet | Microsoft Docs"
ms.custom: 
ms.date: 08/04/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Cmdlets [SQL Server], Encode-Sqlname
- Encode-Sqlname cmdlet
- PowerShell [SQL Server], Encode-Sqlname
- Convert-UrnToPath cmdlet
- PowerShell [SQL Server], cmdlets
- Cmdlets [SQL Server]
- PowerShell [SQL Server], Convert-UrnToPath
- Cmdlets [SQL Server], Convert-UrnToPath
- Decode-Sqlname cmdlet
- PowerShell [SQL Server], Decode-Sqlname
- Cmdlets [SQL Server], Decode-Sqlname
ms.assetid: 720aa982-09ae-41a3-b603-a91004cfbe3e
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f73610b00bc4c7dd6e68128f841a3c7a1e6ed691
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="use-the-database-engine-cmdlets"></a>使用数据库引擎 cmdlet
  Windows PowerShell cmdlet 是单函数命令，通常采用“动词-名词”形式的命名约定，如 **Get-Help** 或 **Set-MachineName**。 用于 Windows PowerShell 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供程序提供特定于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的 cmdlet。  
  
## <a name="database-engine-cmdlets"></a>数据库引擎 cmdlet  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实现了一小部分用于 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的 cmdlet。 这些 cmdlet 主要用于从新的 PowerShell 脚本运行现有的 Transact-SQL 脚本，评估基于策略的管理策略并帮助在 SQL Server 提供程序路径中指定 SQL Server 标识符。  
  
 用于 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的大多数 Windows PowerShell 脚本通过使用 SQL Server PowerShell 提供程序和 SQL Server 可管理性对象模型。 有关详细信息，请参阅 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)。  
  
### <a name="get-cmdlet-help"></a>获取 Cmdlet 帮助  
 在 Windows PowerShell 环境中， **Get-Help** cmdlet 提供了每个 cmdlet 的帮助信息。 **Get-Help** 返回各种信息，如语法、参数定义、输入和输出类型以及 cmdlet 所执行操作的说明。 有关详细信息，请参阅 [Get Help SQL Server PowerShell](../../relational-databases/scripting/get-help-sql-server-powershell.md)。  
  
### <a name="partial-parameter-names"></a>部分参数名称  
 不需要指定 cmdlet 参数的完整名称。 您只需指定该名称的一部分，以便能够将其与 cmdlet 支持的其他参数区分开。 例如，这些示例说明指定 **Invoke-Sqlcmd -QueryTimeout** 参数的三种方式：  
  
```  
Invoke-Sqlcmd -Query "SELECT @@VERSION;" -QueryTimeout 3  
Invoke-Sqlcmd -Query "SELECT @@VERSION;" -QueryTime 3  
Invoke-Sqlcmd -Query "SELECT @@VERSION;" -QueryT 3  
```  
  
## <a name="database-engine-cmdlet-tasks"></a>数据库引擎 cmdlet 任务  
  
|任务说明|主题|  
|----------------------|-----------|  
|介绍使用 **Invoke-Sqlcmd** 运行包含 **或 XQuery 语句的** sqlcmd [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本或命令。 它可以接受 **sqlcmd** 输入作为字符串输入参数或要打开的脚本文件的文件名。|[Invoke-Sqlcmd cmdlet](../../powershell/invoke-sqlcmd-cmdlet.md)|  
|介绍使用 **Invoke-PolicyEvaluation** 报告 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象的目标集是否符合基于策略的管理策略中定义的条件。 可以选择使用 cmdlet 对不符合策略条件的目标对象中的任何可设置选项进行重新配置。|[Invoke-PolicyEvaluation cmdlet](../../powershell/invoke-policyevaluation-cmdlet.md)|  
|介绍使用 **Encode-Sqlname** 和 **Decode-Sqlname** 处理包含 Windows PowerShell 路径中不支持的字符的 SQL Server 标识符。|[对 SQL Server 标识符进行编码和解码](../../relational-databases/scripting/encode-and-decode-sql-server-identifiers.md)|  
|介绍使用 **Convert-UrnToPath** 将 SQL Server 可管理性对象统一资源名称 (URN) 转换为等价的 SQL Server 提供程序路径。|[将 URN 转换为 SQL Server 提供程序路径](../../relational-databases/scripting/convert-urns-to-sql-server-provider-paths.md)|  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server PowerShell 提供程序](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)   
[Always On 可用性组的 PowerShell Cmdlet 概述 (SQL Server)](../../database-engine/availability-groups/windows/overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)
  
  
