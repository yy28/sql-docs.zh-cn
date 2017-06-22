---
title: "数据库引擎错误严重性 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- user-defined error messages [SQL Server]
- severity levels [SQL Server]
- retrieving error severity
- errors [SQL Server], severity
- TRY...CATCH [SQL Server]
ms.assetid: 3e7f5925-6edd-42e1-bf17-f7deb03993a7
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f5b2b6fbe1d6d46c045452430067a542a99623bd
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="database-engine-error-severities"></a>数据库引擎错误严重性
  当错误是由 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]引起时，此错误的严重性可说明 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所遇到问题的类型。  
  
## <a name="levels-of-severity"></a>严重性级别  
 下表列出并说明 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]所引起错误的严重级别。  
  
|严重级别|说明|  
|--------------------|-----------------|  
|0-9|返回不太严重的状态信息或报表错误的信息性消息。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 不会引起严重级别为 0 到 9 的系统错误。|  
|10|返回不太严重的状态信息或报表错误的信息性消息。 由于兼容性原因， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 在将错误信息返回到调用应用程序前将严重性级别从 10 转换为 0。|  
|11-16|指示可由用户纠正的错误。|  
|11|指示给定的对象或实体不存在。|  
|12|特殊严重性，用于因特殊查询提示而不使用锁定的查询。 在某些情况下，因为没有用锁保证一致性，由这些语句所执行的读取操作会产生不一致的数据。|  
|13|指示事务死锁错误。|  
|14|指示安全性相关错误，如权限被拒绝。|  
|15|指示 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令中的语法错误。|  
|16|指示可由用户纠正的常规错误。|  
|17-19|指示无法由用户纠正的软件错误。 请将问题通知系统管理员。|  
|17|指示语句导致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用尽资源（如数据库的内存、锁或磁盘空间）或超出了系统管理员设置的某些限制。|  
|18|指示 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 软件中有问题，但可完成执行语句，并且可维护到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例的连接。 每当出现严重级别为 18 的消息时均应通知系统管理员。|  
|19|指示超出了不可配置的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 限制并且当前批处理已终止。 严重级别为 19 或更高的错误消息将停止执行当前的批处理。 严重级别为 19 的错误很少，必须由系统管理员或主要支持提供商更正。 当引发严重级别为 19 的消息时，请与系统管理员联系。 严重级别从 19 到 25 的错误消息均写入错误日志。|  
|20-24|指示系统问题并且是致命错误，这意味着正在执行某语句或批处理的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 任务已停止运行。 此任务记录了所发生事件的有关信息，然后终止。 在大多数情况下，应用程序与 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例的连接也可能终止。 如果发生这种情况，该问题可能使应用程序无法重新连接。<br /><br /> 此范围内的错误消息可以影响同一数据库中所有正在访问数据的进程，并可能指示数据库或对象已损坏。 严重级别从 19 到 24 的错误消息均写入错误日志。|  
|20|指示语句遇到了问题。 由于该问题只影响了当前任务，数据库本身未必已经损坏。|  
|21|指示遇到了影响当前数据库中所有任务的问题，但数据库本身未必已经损坏。|  
|22|指示消息中所指定的表或索引因软件或硬件问题而损坏。<br /><br /> 很少发生严重级别为 22 的错误。 如果发生这种错误，请运行 DBCC CHECKDB 以确定数据库中的其他对象是否也已损坏。 这种问题可能只是出现在缓存中而不存在于磁盘本身。 如果发生此错误，请重新启动 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例更正此问题。 若要继续工作，则必须重新连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例；否则，请使用 DBCC 修复该问题。 在某些情况下，可能需要还原数据库。<br /><br /> 如果重新启动 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例不能解决此问题，那么问题就是出在磁盘上。 有时，销毁错误消息中指定的对象可以解决此问题。 例如，如果消息报告 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例在非聚集索引中发现了长度为 0 的行，则请删除该索引并重建。|  
|23|指示整个数据库的完整性因硬件或软件问题而出现问题。<br /><br /> 很少发生严重级别为 23 的错误。 如果发生这种错误，请运行 DBCC CHECKDB 以确定损坏的程度。 这种问题可能只是出现在缓存中而未出现在磁盘本身。 如果发生此错误，请重新启动 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例更正此问题。 若要继续工作，则必须重新连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例；否则，请使用 DBCC 修复该问题。 在某些情况下，可能需要还原数据库。|  
|24|指示介质故障。 系统管理员可能需要还原数据库。 您可能还需要致电硬件供应商。|  
  
## <a name="user-defined-error-message-severity"></a>用户定义的错误消息严重性  
 可以使用 **sp_addmessage** 将严重级别为 1 到 25 的用户定义错误消息添加到 **sys.messages** 目录视图中。 这些用户定义的错误消息可供 RAISERROR 使用。 有关详细信息，请参阅 [sp_addmessage (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)。  
  
 可用 RAISERROR 生成严重性级别为 1 到 25 的用户定义错误消息。 RAISERROR 可以引用 **sys.messages** 目录视图中存储的用户定义错误消息，也可以动态地生成消息。 生成错误时如果使用 **sys.messages** 中的用户定义错误消息，则 RAISERROR 指定的严重级别将覆盖 **sys.messages** 中指定的严重级别。 有关详细信息，请参阅 [RAISERROR (Transact-SQL)](../../t-sql/language-elements/raiserror-transact-sql.md)。  
  
## <a name="error-severity-and-trycatch"></a>错误严重性和 TRY...CATCH  
 TRY...CATCH 构造可捕捉所有严重级别大于 10 但不终止数据库连接的错误。  
  
 严重级别从 0 到 10 的错误是信息性消息，并不导致执行从 TRY...CATCH 构造的 CATCH 块中跳转。  
  
 终止数据库连接的错误（通常严重级别为 20 到 25）不由 CATCH 块处理，因为连接终止后执行也中止了。  
  
 有关详细信息，请参阅 [TRY...CATCH (Transact-SQL)](../../t-sql/language-elements/try-catch-transact-sql.md)所遇到问题的类型。  
  
## <a name="retrieving-error-severity"></a>检索错误严重性  
 系统函数 ERROR_SEVERITY 可用来检索导致 TRY...CATCH 构造的 CATCH 块运行的错误的严重性。 如果是在 CATCH 块的作用域之外调用 ERROR_SEVERITY，则 ERROR_SEVERITY 返回空值。 有关详细信息，请参阅 [ERROR_SEVERITY (Transact-SQL)](../../t-sql/functions/error-severity-transact-sql.md)。  
  
## <a name="see-also"></a>另请参阅  
 [了解数据库引擎错误](../../relational-databases/errors-events/understanding-database-engine-errors.md)   
 [sys.messages (Transact-SQL)](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [System Functions (Transact-SQL)](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [TRY...CATCH (Transact-SQL)](../../t-sql/language-elements/try-catch-transact-sql.md)  
  
  
