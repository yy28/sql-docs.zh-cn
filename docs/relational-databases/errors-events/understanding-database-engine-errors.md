---
title: "了解数据库引擎错误 | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "错误 [SQL Server], 关于错误"
  - "错误 [SQL Server], 数据库引擎"
  - "错误 [SQL Server]"
  - "数据库引擎 [SQL Server], 错误"
ms.assetid: ddaca9d3-956f-46a5-8cd3-a7a15ec75878
caps.latest.revision: 27
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 27
---
# 了解数据库引擎错误
  由 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 引起的错误具有下表所述的属性。  
  
|Attribute|说明|  
|---------------|-----------------|  
|错误号|每个错误消息具有唯一的错误号。|  
|错误消息字符串|错误消息包含关于错误原因的诊断信息。 许多错误消息都有替换变量，其中插入了一些信息，如生成错误的对象名称。|  
|Severity|严重性指示错误的严重程度。 严重性较低的错误，如 1 级或 2 级，为信息性消息或低级警告。 严重性较高的错误指示需要尽快解决的问题。 有关错误严重性的详细信息，请参阅[数据库引擎错误严重性](../../relational-databases/errors-events/database-engine-error-severities.md)。|  
|State|某些错误消息可能在 [!INCLUDE[ssDE](../../includes/ssde-md.md)]代码中多处出现。 例如，几种不同情况下都可能引发 1105 错误。 每个引发错误的特定情况都分配唯一的状态代码。<br /><br /> 查看包含已知问题信息的数据库时，如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 知识库，可以使用状态号确定所记录的问题是否与曾遇到的错误相同。 例如，如果一篇知识库文章说明状态为 2 的 1105 错误，而接收到的 1105 错误消息状态为 3，则错误原因可能不同于文章所报告的原因。<br /><br /> [!INCLUDE[msCoName](../../includes/msconame-md.md)] 支持工程师也可以用错误中的状态代码在源代码中查找产生错误的位置。 此信息可能会获取诊断问题所需的更多信息。|  
|过程名称|出现错误的存储过程或触发器的名称。|  
|行号|指示在批处理、存储过程、触发器或函数中生成错误的语句。|  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例中所有系统和用户定义的错误消息都包含在 **sys.messages** 目录视图中。 可以使用 RAISERROR 语句将用户定义的错误返回到应用程序。  
  
 所有数据库 API，如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] **SQLClient** 命名空间、ActiveX 数据对象 (ADO)、OLE DB 和开放式数据库连接 (ODBC)，都会报告基本错误属性。 此信息包括错误号和消息字符串。 但是，并非所有 API 都报告所有其他错误属性。  
  
 可以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码中使用一些函数（如相关 CATCH 块作用域内的 ERROR_LINE、ERROR_MESSAGE、ERROR_NUMBER、ERROR_PROCEDURE、ERROR_SEVERITY 和 ERROR_STATE），来获得关于发生在 TRY…CATCH 结构的 TRY 块作用域内的错误信息。 有关详细信息，请参阅 [TRY...CATCH (Transact-SQL)](../../t-sql/language-elements/try-catch-transact-sql.md)。  
  
## 示例  
 下面的示例将查询 `sys.messages` 目录视图以返回具有英文文本 (`1033`) 的[!INCLUDE[ssDE](../../includes/ssde-md.md)]中所有系统和用户定义错误消息的列表。  
  
```  
SELECT  
    message_id,  
    language_id,  
    severity,  
    is_event_logged,  
    text  
  FROM sys.messages  
  WHERE language_id = 1033;  
```  
  
 有关详细信息，请参阅 [sys.messages (Transact-SQL)](../Topic/sys.messages%20\(Transact-SQL\).md)。  
  
## 另请参阅  
 [sys.messages (Transact-SQL)](../Topic/sys.messages%20\(Transact-SQL\).md)   
 [RAISERROR (Transact-SQL)](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR (Transact-SQL)](../../t-sql/functions/error-transact-sql.md)   
 [TRY...CATCH (Transact-SQL)](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE (Transact-SQL)](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE (Transact-SQL)](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER (Transact-SQL)](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE (Transact-SQL)](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY (Transact-SQL)](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE (Transact-SQL)](../../t-sql/functions/error-state-transact-sql.md)  
  
  