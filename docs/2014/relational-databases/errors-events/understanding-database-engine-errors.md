---
title: 了解数据库引擎错误 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- errors [SQL Server], about errors
- errors [SQL Server], Database Engine
- errors [SQL Server]
- Database Engine [SQL Server], errors
ms.assetid: ddaca9d3-956f-46a5-8cd3-a7a15ec75878
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2f8f7264b63417d9dc337aec62ee5734dcf8ad98
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62761683"
---
# <a name="understanding-database-engine-errors"></a>了解数据库引擎错误
  由 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 引起的错误具有下表所述的属性。  
  
|特性|Description|  
|---------------|-----------------|  
|错误号|每个错误消息具有唯一的错误号。|  
|错误消息字符串|错误消息包含关于错误原因的诊断信息。 许多错误消息都有替换变量，其中插入了一些信息，如生成错误的对象名称。|  
|Severity|严重性指示错误的严重程度。 严重性较低的错误，如 1 级或 2 级，为信息性消息或低级警告。 严重性较高的错误指示需要尽快解决的问题。 有关错误严重性的详细信息，请参阅 [数据库引擎错误严重性](database-engine-error-severities.md)。|  
|State|某些错误消息可能在 [!INCLUDE[ssDE](../../includes/ssde-md.md)]代码中多处出现。 例如，几种不同情况下都可能引发 1105 错误。 每个引发错误的特定情况都分配唯一的状态代码。<br /><br /> 查看包含已知问题信息的数据库时，如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 知识库，可以使用状态号确定所记录的问题是否与曾遇到的错误相同。 例如，如果一篇知识库文章说明状态为 2 的 1105 错误，而接收到的 1105 错误消息状态为 3，则错误原因可能不同于文章所报告的原因。<br /><br /> [!INCLUDE[msCoName](../../includes/msconame-md.md)] 支持工程师也可以用错误中的状态代码在源代码中查找产生错误的位置。 此信息可能会获取诊断问题所需的更多信息。|  
|过程名称|出现错误的存储过程或触发器的名称。|  
|行号|指示在批处理、存储过程、触发器或函数中生成错误的语句。|  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例中所有系统和用户定义的错误消息都包含在 **sys.messages** 目录视图中。 可以使用 RAISERROR 语句将用户定义的错误返回到应用程序。  
  
 所有数据库 API，如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] **SQLClient** 命名空间、ActiveX 数据对象 (ADO)、OLE DB 和开放式数据库连接 (ODBC)，都会报告基本错误属性。 此信息包括错误号和消息字符串。 但是，并非所有 API 都报告所有其他错误属性。  
  
 可以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码中使用一些函数（如相关 CATCH 块作用域内的 ERROR_LINE、ERROR_MESSAGE、ERROR_NUMBER、ERROR_PROCEDURE、ERROR_SEVERITY 和 ERROR_STATE），来获得关于发生在 TRY…CATCH 结构的 TRY 块作用域内的错误信息。 有关详细信息，请参阅 [TRY...CATCH (Transact-SQL)](/sql/t-sql/language-elements/try-catch-transact-sql)。  
  
## <a name="examples"></a>示例  
 下面的示例将查询 `sys.messages` 目录视图以返回具有英文文本 ( [!INCLUDE[ssDE](../../includes/ssde-md.md)] ) 的`1033`中所有系统和用户定义错误消息的列表。  
  
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
  
 有关详细信息，请参阅 [sys.messages (Transact-SQL)](/sql/relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages)。  
  
## <a name="see-also"></a>请参阅  
 [sys.messages (Transact-SQL)](/sql/relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages)   
 [RAISERROR (Transact-SQL)](/sql/t-sql/language-elements/raiserror-transact-sql)   
 [@@ERROR (Transact-SQL)](/sql/t-sql/functions/error-transact-sql)   
 [TRY...CATCH (Transact-SQL)](/sql/t-sql/language-elements/try-catch-transact-sql)   
 [ERROR_LINE (Transact-SQL)](/sql/t-sql/functions/error-line-transact-sql)   
 [ERROR_MESSAGE (Transact-SQL)](/sql/t-sql/functions/error-message-transact-sql)   
 [ERROR_NUMBER (Transact-SQL)](/sql/t-sql/functions/error-number-transact-sql)   
 [ERROR_PROCEDURE (Transact-SQL)](/sql/t-sql/functions/error-procedure-transact-sql)   
 [ERROR_SEVERITY (Transact-SQL)](/sql/t-sql/functions/error-severity-transact-sql)   
 [ERROR_STATE (Transact-SQL)](/sql/t-sql/functions/error-state-transact-sql)  
  
  
