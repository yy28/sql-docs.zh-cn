---
title: 本机编译存储过程和执行的 Set 选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c1869cf7-9030-4d18-85d6-0e419a4e9af7
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 264a2b3ab1e6f3f0bda97bfe89a4438aa641577d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85025848"
---
# <a name="natively-compiled-stored-procedures-and-execution-set-options"></a>本机编译存储过程和执行的 Set 选项
  会话选项在原子块中是固定的。 存储过程的执行不会受到会话的 SET 选项的影响。 但是，某些 SET 选项（例如 SET NOEXEC 和 SET SHOWPLAN_XML）会导致存储过程（包括本机编译存储过程）不执行。  
  
 在任意 STATISTICS 选项开启的情况下执行本机编译的存储过程时，系统将该过程作为整体（而非针对每条语句）收集统计数据。 有关详细信息，请参阅 [SET STATISTICS IO (Transact-SQL)](/sql/t-sql/statements/set-statistics-io-transact-sql)、[SET STATISTICS PROFILE (Transact-SQL)](/sql/t-sql/statements/set-statistics-profile-transact-sql)、[SET STATISTICS TIME (Transact-SQL)](/sql/t-sql/statements/set-statistics-time-transact-sql) 和 [SET STATISTICS XML (Transact-SQL)](/sql/t-sql/statements/set-statistics-xml-transact-sql)。 若要在本机编译的存储过程中获取针对每条语句的执行统计信息，请使用 sp_statement_completed 事件上的扩展事件会话，该会话将会在某一存储过程执行中的每个单独查询完成时启动。 有关创建扩展事件会话的详细信息，请参阅 [CREATE EVENT SESSION (Transact-SQL)](/sql/t-sql/statements/create-event-session-transact-sql)。  
  
 本机编译存储过程支持 `SHOWPLAN_XML`。 本机编译的存储过程不支持 `SHOWPLAN_ALL` 和 `SHOWPLAN_TEXT`。  
  
 本机编译的存储过程不支持 `SET FMTONLY`。 请改为使用 [sp_describe_first_result_set (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql)。  
  
## <a name="see-also"></a>另请参阅  
 [本机编译的存储过程](natively-compiled-stored-procedures.md)  
  
  
