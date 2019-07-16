---
title: SQLGetInfo 支持 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLGetInfo
- backward compatibility [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], support
ms.assetid: 57326f57-daba-46b6-b0be-6c97213b9ef1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0f40299dccc0313f662aeadfcb26b71326cdc6d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073906"
---
# <a name="sqlgetinfo-support"></a>SQLGetInfo 支持
当 ODBC 2。*x*应用程序调用**SQLGetInfo**到 ODBC 3 *.x*驱动程序，*信息类型*必须支持下表中的自变量。  
  
|*InfoType*|返回|  
|----------------|-------------|  
|SQL_ALTER_TABLE (ODBC 2.0)**注意：** 不推荐使用此信息类型;在右侧列中的位屏蔽不推荐使用。|枚举中的子句 SQLINTEGER 位掩码**ALTER TABLE**数据源支持的语句。<br /><br /> 以下位掩码用于确定支持的子句：<br /><br /> SQL_AT_DROP_COLUMN = 支持的功能删除的列。 这是导致级联还是限制行为是驱动程序定义的。 (ODBC 2.0)<br /><br /> SQL_AT_ADD_COLUMN = 添加支持单个 ALTER TABLE 语句中的多个列的能力。 此位不能与其他 SQL_AT_ADD_COLUMN_XXX 位或 SQL_AT_CONSTRAINT_XXX 位合并。 (ODBC 2.0)|  
|SQL_FETCH_DIRECTION (ODBC 1.0)<br /><br /> 在 ODBC 1.0; 中引入的信息类型位掩码，每个带有中引入的版本。|枚举的受支持的提取方向选项 SQLINTEGER 位掩码。<br /><br /> 以下的位屏蔽与标志结合使用，以确定哪些选项受支持：<br /><br /> SQL_FD_FETCH_NEXT (ODBC 1.0) SQL_FD_FETCH_FIRST (ODBC 1.0) SQL_FD_FETCH_LAST (ODBC 1.0) SQL_FD_FETCH_PRIOR (ODBC 1.0) SQL_FD_FETCH_ABSOLUTE (ODBC 1.0) SQL_FD_FETCH_RELATIVE (ODBC 1.0) SQL_FD_FETCH_BOOKMARK (ODBC 2.0)|  
|SQL_LOCK_TYPES (ODBC 2.0)|枚举支持的锁定 SQLINTEGER 位掩码类型*纷纷采用*中的参数**SQLSetPos**。<br /><br /> 以下的位屏蔽与标志结合使用，以确定哪些锁类型受支持：<br /><br /> SQL_LCK_NO_CHANGE SQL_LCK_EXCLUSIVE SQL_LCK_UNLOCK|  
|SQL_ODBC_API_CONFORMANCE (ODBC 1.0)|指示 ODBC 一致性级别的 SQLSMALLINT 值。<br /><br /> SQL_OAC_NONE = 无<br /><br /> SQL_OAC_LEVEL1 = 级别 1 支持<br /><br /> SQL_OAC_LEVEL2 = 2 级支持|  
|SQL_ODBC_SQL_CONFORMANCE (ODBC 1.0)|一个指示驱动程序支持的 SQL 语法 SQLSMALLINT 值。 请参阅[附录 c:SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)有关 SQL 一致性级别的定义。<br /><br /> SQL_OSC_MINIMUM = 支持的最小值语法<br /><br /> SQL_OSC_CORE = Core 支持的语法<br /><br /> SQL_OSC_EXTENDED = 支持扩展语法|  
|SQL_POS_OPERATIONS (ODBC 2.0)|枚举中的受支持的操作 SQLINTEGER 位掩码**SQLSetPos**。<br /><br /> 以下的位屏蔽习惯于结合使用的标志以确定哪些选项受支持：<br /><br /> SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)|  
|SQL_POSITIONED_STATEMENTS (ODBC 2.0)|枚举支持 SQLINTEGER 位掩码定位的 SQL 语句。<br /><br /> 以下位掩码用于确定支持哪些语句：<br /><br /> SQL_PS_POSITIONED_DELETE SQL_PS_POSITIONED_UPDATE SQL_PS_SELECT_FOR_UPDATE|  
|SQL_SCROLL_CONCURRENCY (ODBC 1.0)|枚举支持的游标并发控制选项 SQLINTEGER 位掩码。<br /><br /> 以下位掩码用于确定支持的选项：<br /><br /> SQL_SCCO_READ_ONLY = 游标是只读的。 不允许任何更新。<br /><br /> SQL_SCCO_LOCK = 游标使用的锁定足以确保可以更新的行的最低级别。<br /><br /> SQL_SCCO_OPT_ROWVER = 游标使用乐观并发控制，将行版本，如 SQLBase ROWID 或 Sybase 时间戳进行比较。<br /><br /> SQL_SCCO_OPT_VALUES = 游标使用乐观并发控制、 对值进行比较。|  
|SQL_STATIC_SENSITIVITY (ODBC 2.0)|SQLINTEGER 位掩码，枚举通过静态或键集驱动的游标的应用程序进行的更改是否**SQLSetPos**或定位的 update 或 delete 语句可以检测到该应用程序。<br /><br /> SQL_SS_ADDITIONS = 已添加行是可见到光标处;游标可以滚动到这些行。 其中将这些行添加到光标处与驱动程序相关。<br /><br /> SQL_SS_DELETIONS = 已删除行不再可供光标和不要将一个"hole"的结果集中;从已删除行滚动游标后，它不能返回到该行。<br /><br /> SQL_SS_UPDATES = 是到光标处; 可见的行的更新如果将光标从滚动，并返回对已更新行，游标所返回的数据是更新的数据，而不是原始数据。 此选项适用仅为静态游标或更新由键集驱动的游标，不更新的密钥。 对于动态游标或在其中一个密钥更改混合游标中的情况下，此选项不适用于。<br /><br /> 应用程序是否可检测到的结果集由其他用户，在同一应用程序，包括其他游标所做的更改取决于游标类型。|  
  
 ODBC 3 *.x*应用程序使用 ODBC 3 *.x*驱动程序不应调用**SQLGetInfo**与*信息类型*参数中所述前面的表，但应使用 ODBC 3 *.x* *信息类型*以下段落中列出的参数。 不是之间的一一对应关系*信息类型*ODBC 2 中使用的参数。*x*和 ODBC 3 中使用的 *.x*。 ODBC 3 *.x*应用程序使用 ODBC 2。*x*驱动程序，但是，应使用*信息类型*参数前面所述。  
  
 上表中的信息类型的一些已弃用支持游标属性的信息类型。 这些不推荐使用类型为 SQL_FETCH_DIRECTION、 SQL_LOCK_TYPES、 SQL_POS_OPERATIONS、 SQL_POSITIONED_STATEMENTS、 SQL_SCROLL_CONCURRENCY 和 SQL_STATIC_SENSITIVITY 的信息。 新的游标属性类型包括 SQL_XXX_CURSOR_ATTRIBUTES1and SQL_XXX_CURSOR_ATTRIBUTES2，其中 XXX 等于 DYNAMIC、 FORWARD_ONLY、 KEYSET_DRIVEN 或 STATIC。 每个新类型指示单个游标类型的驱动程序功能。 有关这些选项的详细信息，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。
