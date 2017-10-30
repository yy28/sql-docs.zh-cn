---
title: "SQLGetInfo 支持 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- compatibility [ODBC], SQLGetInfo
- backward compatibility [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], support
ms.assetid: 57326f57-daba-46b6-b0be-6c97213b9ef1
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fb9afa5b40ffa7628e04ee85e5ddc4f752e98935
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetinfo-support"></a>SQLGetInfo 支持
当一个 ODBC 2。*x*应用程序调用**SQLGetInfo**为 ODBC 3*.x*驱动程序，*信息类型*必须支持下表中的自变量。  
  
|*信息类型*|返回|  
|----------------|-------------|  
|SQL_ALTER_TABLE (ODBC 2.0)**注意：**不推荐使用此信息类型; 右侧列中的位掩码已弃用。|枚举中的子句 SQLINTEGER 位掩码**ALTER TABLE**数据源所支持的语句。<br /><br /> 以下的位掩码用于确定支持哪些子句：<br /><br /> SQL_AT_DROP_COLUMN = 支持删除列的功能。 这是导致 cascade 还是限制行为是驱动程序定义的。 (ODBC 2.0)<br /><br /> SQL_AT_ADD_COLUMN = 添加支持在单个的 ALTER TABLE 语句中的多个列的能力。 此位不能与其他 SQL_AT_ADD_COLUMN_XXX bits 或 SQL_AT_CONSTRAINT_XXX bits 合并。 (ODBC 2.0)|  
|SQL_FETCH_DIRECTION (ODBC 1.0)<br /><br /> ODBC 1.0; 中引入的信息类型每个位掩码都标有在其中引入的版本。|枚举支持的提取方向选项 SQLINTEGER 位掩码。<br /><br /> 以下的位掩码与标志结合使用，以确定支持哪些选项：<br /><br /> SQL_FD_FETCH_NEXT (ODBC 1.0) SQL_FD_FETCH_FIRST (ODBC 1.0) SQL_FD_FETCH_LAST (ODBC 1.0) SQL_FD_FETCH_PRIOR (ODBC 1.0) SQL_FD_FETCH_ABSOLUTE (ODBC 1.0) SQL_FD_FETCH_RELATIVE (ODBC 1.0) SQL_FD_FETCH_BOOKMARK (ODBC 2.0)|  
|SQL_LOCK_TYPES (ODBC 2.0)|枚举支持的锁定 SQLINTEGER 位掩码类型*fLock*中的参数**SQLSetPos**。<br /><br /> 以下的位掩码与标志结合使用，以确定哪些锁类型受支持：<br /><br /> SQL_LCK_NO_CHANGE SQL_LCK_EXCLUSIVE SQL_LCK_UNLOCK|  
|SQL_ODBC_API_CONFORMANCE (ODBC 1.0)|一个指示的 ODBC 一致性级别 SQLSMALLINT 值。<br /><br /> SQL_OAC_NONE = None<br /><br /> SQL_OAC_LEVEL1 = 级别 1 支持<br /><br /> SQL_OAC_LEVEL2 = 支持级别 2|  
|SQL_ODBC_SQL_CONFORMANCE (ODBC 1.0)|一个指示驱动程序支持的 SQL 语法 SQLSMALLINT 值。 请参阅[附录 c: SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)有关 SQL 一致性级别的定义。<br /><br /> SQL_OSC_MINIMUM = 支持的最小值语法<br /><br /> SQL_OSC_CORE = 核心语法支持<br /><br /> SQL_OSC_EXTENDED = 扩展语法支持|  
|SQL_POS_OPERATIONS (ODBC 2.0)|枚举中的受支持的操作 SQLINTEGER 位掩码**SQLSetPos**。<br /><br /> 以下的位掩码习惯于结合标志以确定支持哪些选项：<br /><br /> SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)|  
|SQL_POSITIONED_STATEMENTS (ODBC 2.0)|枚举支持 SQLINTEGER 位掩码定位 SQL 语句。<br /><br /> 以下的位掩码用于确定支持哪些语句：<br /><br /> SQL_PS_POSITIONED_DELETE SQL_PS_POSITIONED_UPDATE SQL_PS_SELECT_FOR_UPDATE|  
|SQL_SCROLL_CONCURRENCY (ODBC 1.0)|枚举支持光标的并发控制选项 SQLINTEGER 位掩码。<br /><br /> 以下的位掩码用于确定支持哪些选项：<br /><br /> SQL_SCCO_READ_ONLY = 游标是只读的。 不允许任何更新。<br /><br /> SQL_SCCO_LOCK = 光标使用锁定不足以确保可以更新的行的最低级别。<br /><br /> SQL_SCCO_OPT_ROWVER = 光标使用乐观并发控制，比较行版本，如 SQLBase ROWID 或 Sybase 时间戳。<br /><br /> SQL_SCCO_OPT_VALUES = 光标使用乐观并发控制，对值进行比较。|  
|SQL_STATIC_SENSITIVITY (ODBC 2.0)|SQLINTEGER 位掩码枚举无论应用程序对通过静态或键集驱动游标所做的更改**SQLSetPos**或定位的 update 或 delete 语句可以检测通过该应用程序。<br /><br /> SQL_SS_ADDITIONS = Added 行是否可见到光标处;光标可以滚动到这些行。 这些行添加到光标处下与驱动程序相关。<br /><br /> SQL_SS_DELETIONS = 已删除行不再可供光标，而没有留下的结果集; 的"漏洞"从已删除的行滚动光标后，它不能返回到该行。<br /><br /> SQL_SS_UPDATES = 到光标处; 可见的行更新如果将光标从滚动，并返回对已更新行，光标所返回的数据是更新的数据，而不是原始数据。 此选项适用仅为静态游标或更新上未更新的密钥的键集驱动游标。 对于动态游标或在其中一个密钥更改混合游标中的情况下，此选项不适用于。<br /><br /> 应用程序是否可以检测到的结果集由其他用户，在同一应用程序，包括其他游标所做的更改取决于游标类型。|  
  
 ODBC 3*.x*应用程序使用 ODBC 3*.x*驱动程序不应调用**SQLGetInfo**与*信息类型*中所述的自变量前面的表，但应使用 ODBC 3*.x* *信息类型*参数列在下一段落中。 没有之间的一一对应关系*信息类型*ODBC 2 中使用的参数。*x*和 ODBC 3 中所使用*.x*。 ODBC 3*.x*应用程序使用 ODBC 2。*x*驱动程序，另一方面，应使用*信息类型*自变量前面所述。  
  
 支持游标属性的信息类型情况下上, 表中的信息类型的某些选项已弃用。 这些不推荐使用类型为 SQL_FETCH_DIRECTION、 SQL_LOCK_TYPES、 SQL_POS_OPERATIONS、 SQL_POSITIONED_STATEMENTS、 SQL_SCROLL_CONCURRENCY 和 SQL_STATIC_SENSITIVITY 的信息。 新的游标属性类型是 SQL_XXX_CURSOR_ATTRIBUTES1and SQL_XXX_CURSOR_ATTRIBUTES2，其中 XXX 等于动态、 FORWARD_ONLY、 KEYSET_DRIVEN 或静态。 每个新的类型表示单个游标类型的驱动程序功能。 有关这些选项的详细信息，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。

