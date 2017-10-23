---
title: "确定性函数和不确定性函数 | Microsoft Docs"
ms.custom: 
ms.date: 08/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-udf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- built-in functions [SQL Server]
- nondeterministic functions
- extended stored procedures [SQL Server], functions that call
- deterministic functions
- user-defined functions [SQL Server], deterministic
ms.assetid: 2f3ce5f5-c81c-4470-8141-8144d4f218dd
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 8cc1fcfdeae8742a93916dfb08c9db1215f88721
ms.openlocfilehash: 2a25a75485ecfb5bae812b01f142a9650ce2933c
ms.contentlocale: zh-cn
ms.lasthandoff: 10/17/2017

---
# <a name="deterministic-and-nondeterministic-functions"></a>确定性函数和不确定性函数
  只要使用特定的输入值集并且数据库具有相同的状态，那么不管何时调用，确定性函数始终都会返回相同的结果。 即使访问的数据库的状态不变，每次使用特定的输入值集调用非确定性函数都可能会返回不同的结果。 例如，函数 AVG 对上述给定的限定条件始终返回相同的值，但返回当前 datetime 值的 GETDATE 函数始终会返回不同的结果。  
  
 有多个用户定义函数的属性通过对调用函数的计算列进行索引或通过引用函数的索引视图确定 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 为函数的结果建立索引的功能。 函数的确定性是一个属性。 例如，如果一个视图引用了任何不确定性函数，则无法对该视图创建聚集索引。 有关函数属性（包括函数确定性）的详细信息，请参阅 [用户定义函数](../../relational-databases/user-defined-functions/user-defined-functions.md)。  
  
 本主题介绍了内置系统函数的确定性，以及在包含对扩展存储过程的调用时对用户定义函数的确定性的影响。  
  
## <a name="built-in-function-determinism"></a>内置函数的确定性  
 用户无法影响任何内置函数的确定性。 每个内置函数都根据 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实现该函数的方式而分为确定性函数或非确定性函数。 例如，在查询中指定 ORDER BY 子句不会更改查询中使用的函数的决定机制。  
  
 所有字符串内置函数都具有确定性。 有关这些函数的列表，请参阅[字符串函数 (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)。  
  
 内置函数类别中除字符串函数以外的下列内置函数始终具有确定性。  
  
||||  
|-|-|-|  
|ABS|DATEDIFF|POWER|  
|ACOS|DAY|RADIANS|  
|ASIN|DEGREES|ROUND|  
|ATAN|EXP|SIGN|  
|ATN2|FLOOR|SIN|  
|CEILING|ISNULL|SQUARE|  
|COALESCE|ISNUMERIC|SQRT|  
|COS|LOG|TAN|  
|COT|LOG10|YEAR|  
|DATALENGTH|MONTH||  
|DATEADD|NULLIF||  
  
 下列函数并非始终是确定性函数，但是在以确定性方式指定后，可用于索引视图或计算列的索引。  
  
|函数|注释|  
|--------------|--------------|  
|所有聚合函数|除非用 OVER 和 ORDER BY 子句指定聚合函数，否则所有聚合函数都具有确定性。 有关这些函数的列表，请参阅[聚合函数 (Transact-SQL)](../../t-sql/functions/aggregate-functions-transact-sql.md)。|  
|CAST|除非与 **datetime**、 **smalldatetime**或 **sql_variant**一起使用，否则其他时候都是确定性的。|  
|CONVERT|除非存在下列条件，否则为确定性函数：<br /><br /> <br /><br /> 源类型是 **sql_variant**。<br /><br /> 目标类型是 **sql_variant** ，其源类型不是确定性的。<br /><br /> 源类型或目标类型是 **datetime** 或 **smalldatetime**，其他源类型或目标类型是字符串，并且指定了不确定的样式。 若要为确定样式，则样式参数必须是常量。 此外，除了样式 20 和 21，小于或等于 100 的样式都具有不确定性。 大于 100 的样式具有确定性，但样式 106、107、109 和 113 除外。|  
|CHECKSUM|确定性函数，CHECKSUM(*) 除外。|  
|ISDATE|只有与 CONVERT 函数一起使用、指定 CONVERT 样式参数并且样式不等于 0、100、9 或 109 时，才是确定性函数。|  
|RAND|仅当指定 *seed* 参数时，RAND 才是确定性函数。|  
  
 所有配置、游标、元数据、安全和系统统计函数都是非确定性函数。 有关这些函数的列表，请参阅[配置函数 (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)、[游标函数 (Transact-SQL)](../../t-sql/functions/cursor-functions-transact-sql.md)、[元数据函数 (Transact-SQL)](../../t-sql/functions/metadata-functions-transact-sql.md)、[安全函数 (Transact-SQL)](../../t-sql/functions/security-functions-transact-sql.md) 和[系统统计函数 (Transact-SQL)](../../t-sql/functions/system-statistical-functions-transact-sql.md)。  
  
 其他类别中的下列内置函数始终为非确定性函数。  
  
|||  
|-|-|  
|@@CONNECTIONS |GETDATE|  
|@@CPU_BUSY |GETUTCDATE|  
|@@DBTS |GET_TRANSMISSION_STATUS|  
|@@IDLE |LAG|  
|@@IO_BUSY |LAST_VALUE|  
|@@MAX_CONNECTIONS |LEAD|  
|@@PACK_RECEIVED |MIN_ACTIVE_ROWVERSION|  
|@@PACK_SENT |NEWID|  
|@@PACKET_ERRORS |NEWSEQUENTIALID|  
|@@TIMETICKS |NEXT VALUE FOR|  
|@@TOTAL_ERRORS |NTILE|  
|@@TOTAL_READ |PARSENAME|  
|@@TOTAL_WRITE |PERCENTILE_CONT|  
|AT TIME ZONE|PERCENTILE_DISC|
|CUME_DIST|PERCENT_RANK|  
|CURRENT_TIMESTAMP|RAND|  
|DENSE_RANK|RANK|  
|FIRST_VALUE|ROW_NUMBER|   
|FORMAT|TEXTPTR|  
  
## <a name="calling-extended-stored-procedures-from-functions"></a>从函数中调用扩展存储过程  
 由于扩展存储过程会对数据库产生副面影响，因此调用扩展存储过程的函数为不确定性函数。 负面影响为对数据库全局状态的更改，如更新表、更新文件或网络等外部资源；例如，修改文件或发送电子邮件。 从用户定义函数中执行扩展存储过程时，不要依赖于返回一致的结果集。 建议不要使用对数据库产生负面影响的用户定义函数。  
  
 从函数内部调用扩展存储过程时，该扩展存储过程不能向客户端返回结果集。 任何向客户端返回结果集的开放式数据服务 API 都具有返回代码 FAIL。  
  
 扩展存储过程可以连接回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 但是，该过程不能与调用扩展存储过程的原始函数联接同一事务。  
  
 类似于从批处理或存储过程中调用，扩展存储过程在运行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 安全帐户的上下文中执行。 扩展存储过程的所有者在授予其他用户执行该过程的权限时，应该考虑此安全性上下文的权限。  
  
  

