---
title: 本机编译存储过程和执行的 Set 选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c1869cf7-9030-4d18-85d6-0e419a4e9af7
caps.latest.revision: 5
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: baf4de1df4bdd64b32182e6fbb72fbbd0ed110b6
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394837"
---
# <a name="natively-compiled-stored-procedures-and-execution-set-options"></a>本机编译存储过程和执行的 Set 选项
  会话选项在原子块中是固定的。 存储过程的执行不会受到会话的 SET 选项的影响。 但是，某些 SET 选项（例如 SET NOEXEC 和 SET SHOWPLAN_XML）会导致存储过程（包括本机编译存储过程）不执行。  
  
 在任意 STATISTICS 选项开启的情况下执行本机编译的存储过程时，系统将该过程作为整体（而非针对每条语句）收集统计数据。 有关详细信息，请参阅 [SET STATISTICS IO (Transact-SQL)](/sql/t-sql/statements/set-statistics-io-transact-sql)、[SET STATISTICS PROFILE (Transact-SQL)](/sql/t-sql/statements/set-statistics-profile-transact-sql)、[SET STATISTICS TIME (Transact-SQL)](/sql/t-sql/statements/set-statistics-time-transact-sql) 和 [SET STATISTICS XML (Transact-SQL)](/sql/t-sql/statements/set-statistics-xml-transact-sql)。 若要在本机编译的存储过程中获取针对每条语句的执行统计信息，请使用 sp_statement_completed 事件上的扩展事件会话，该会话将会在某一存储过程执行中的每个单独查询完成时启动。 有关创建扩展事件会话的详细信息，请参阅 [CREATE EVENT SESSION (Transact-SQL)](/sql/t-sql/statements/create-event-session-transact-sql)。  
  
 `SHOWPLAN_XML` 支持本机编译存储过程。 本机编译的存储过程不支持 `SHOWPLAN_ALL` 和 `SHOWPLAN_TEXT`。  
  
 本机编译的存储过程不支持 `SET FMTONLY`。 请改为使用 [sp_describe_first_result_set (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql)。  
  
## <a name="see-also"></a>请参阅  
 [本机编译的存储过程](natively-compiled-stored-procedures.md)  
  
  
