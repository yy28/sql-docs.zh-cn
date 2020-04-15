---
title: SQLGetInfo 支持 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a21c035a14814f51d4344894ef253b2cc844f4c2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307798"
---
# <a name="sqlgetinfo-support"></a>SQLGetInfo 支持
当一个ODBC 2。*x*应用程序将**SQLGetInfo**调用 ODBC 3 *.x*驱动程序，必须支持下表中的*InfoType*参数。  
  
|*信息类型*|返回|  
|----------------|-------------|  
|SQL_ALTER_TABLE （ODBC 2.0）**注意：** 此信息类型不会弃用;右侧列中的位掩码被弃用。|SQLINTEGER 位掩码，枚举数据源支持的**ALTER TABLE**语句中子句。<br /><br /> 以下位掩码用于确定哪些子句受支持：<br /><br /> SQL_AT_DROP_COLUMN = 支持删除列的功能。 这是否导致级联或限制行为是驱动程序定义的。 （ODBC 2.0）<br /><br /> SQL_AT_ADD_COLUMN = 支持在单个 ALTER TABLE 语句中添加多列的功能。 此位不与其他SQL_AT_ADD_COLUMN_XXX位或SQL_AT_CONSTRAINT_XXX位组合。 （ODBC 2.0）|  
|SQL_FETCH_DIRECTION （ODBC 1.0）<br /><br /> ODBC 1.0 中引入了信息类型;每个位掩码都标有引入它的版本。|SQLINTEGER 位掩码枚举了支持的提取方向选项。<br /><br /> 以下位掩码与标志结合使用，以确定支持哪些选项：<br /><br /> SQL_FD_FETCH_NEXT （ODBC 1.0） SQL_FD_FETCH_FIRST （ODBC 1.0） SQL_FD_FETCH_LAST （ODBC 1.0） SQL_FD_FETCH_PRIOR （ODBC 1.0） SQL_FD_FETCH_ABSOLUTE （ODBC 1.0） SQL_FD_FETCH_RELATIVE （ODBC 1.0） SQL_FD_FETCH_BOOKMARK （ODBC 2.0）|  
|SQL_LOCK_TYPES （ODBC 2.0）|SQLINTEGER 位掩码，枚举**SQLSetPos**中*fLock*参数支持的锁类型。<br /><br /> 以下位掩码与标志结合使用，以确定支持哪些锁类型：<br /><br /> SQL_LCK_NO_CHANGESQL_LCK_EXCLUSIVESQL_LCK_UNLOCK|  
|SQL_ODBC_API_CONFORMANCE （ODBC 1.0）|指示 ODBC 符合性级别的 SQLSMALLINT 值。<br /><br /> SQL_OAC_NONE = 无<br /><br /> SQL_OAC_LEVEL1 = 支持级别 1<br /><br /> SQL_OAC_LEVEL2 = 支持 2 级|  
|SQL_ODBC_SQL_CONFORMANCE （ODBC 1.0）|指示驱动程序支持的 SQL 语法的 SQLSMALLINT 值。 有关 SQL 符合性级别的定义，请参阅[附录 C：SQL 语法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。<br /><br /> SQL_OSC_MINIMUM = 支持最小语法<br /><br /> SQL_OSC_CORE = 支持核心语法<br /><br /> SQL_OSC_EXTENDED = 支持扩展语法|  
|SQL_POS_OPERATIONS （ODBC 2.0）|在**SQLSetPos**中枚举受支持的操作的 SQLINTEGER 位掩码。<br /><br /> 以下位掩码用于与标志结合，以确定支持哪些选项：<br /><br /> SQL_POS_POSITION （ODBC 2.0） SQL_POS_REFRESH （ODBC 2.0） SQL_POS_UPDATE （ODBC 2.0） SQL_POS_DELETE （ODBC 2.0） SQL_POS_ADD （ODBC 2.0）|  
|SQL_POSITIONED_STATEMENTS （ODBC 2.0）|枚举支持的 SQL 语句的 SQLINTEGER 位掩码。<br /><br /> 以下位掩码用于确定支持哪些语句：<br /><br /> SQL_PS_POSITIONED_DELETE SQL_PS_POSITIONED_UPDATE SQL_PS_SELECT_FOR_UPDATE|  
|SQL_SCROLL_CONCURRENCY （ODBC 1.0）|一个 SQLINTEGER 位掩码，枚举游标支持的并发控制选项。<br /><br /> 以下位掩码用于确定哪些选项受支持：<br /><br /> SQL_SCCO_READ_ONLY = 光标是只读的。 不允许更新。<br /><br /> SQL_SCCO_LOCK = Cursor 使用尽可能低的锁定级别来确保可以更新行。<br /><br /> SQL_SCCO_OPT_ROWVER = 光标使用乐观并发控制，比较行版本，如 SQLBase ROWID 或 Sybase TIMESTAMP。<br /><br /> SQL_SCCO_OPT_VALUES = 光标使用乐观并发控制，比较值。|  
|SQL_STATIC_SENSITIVITY （ODBC 2.0）|SQLINTEGER 位掩码枚举，该应用程序是否可以检测到应用程序通过**SQLSetPos**对静态或按键集驱动的游标所做的更改，或者该应用程序是否可以检测到定位的更新或删除语句。<br /><br /> SQL_SS_ADDITIONS = 添加的行对游标可见;光标可以滚动到这些行。 将这些行添加到游标的位置与驱动程序相关。<br /><br /> SQL_SS_DELETIONS = 删除的行不再可用于游标，也不会在结果集中留下"孔";光标从已删除的行滚动后，无法返回到该行。<br /><br /> SQL_SS_UPDATES = 对行的更新对游标可见;如果游标从中滚动并返回到更新的行，则游标返回的数据是更新的数据，而不是原始数据。 此选项仅适用于不更新密钥的键集驱动的游标上的静态游标或更新。 此选项不适用于动态游标，也不适用于在混合游标中更改键的情况。<br /><br /> 应用程序是否可以检测其他用户（包括同一应用程序中的其他游标）对结果集所做的更改，取决于游标类型。|  
  
 使用 ODBC 3 *.x*驱动程序的 ODBC 3 *.x*应用程序不应使用上表中描述的*InfoType*参数调用**SQLGetInfo，** 而应使用下一段中列出的 ODBC 3 *.x* *InfoType*参数。 ODBC 2 中使用的*InfoType*参数之间没有一对一的对应关系。*x*和 ODBC 3 *.x*中使用的。 与 ODBC 2 配合使用的 ODBC 3 *.x*应用程序。*另一方面，x*驱动程序应使用前面介绍*的 InfoType*参数。  
  
 上表中的某些信息类型被弃用，而倾向于游标属性信息类型。 这些弃用的信息类型SQL_FETCH_DIRECTION、SQL_LOCK_TYPES、SQL_POS_OPERATIONS、SQL_POSITIONED_STATEMENTS、SQL_SCROLL_CONCURRENCY和SQL_STATIC_SENSITIVITY。 新的游标属性类型SQL_XXX_CURSOR_ATTRIBUTES1andSQL_XXX_CURSOR_ATTRIBUTES2，其中 XXX 等于 DYNAMIC、FORWARD_ONLY、KEYSET_DRIVEN 或 STATIC。 每种新类型都表示单个游标类型的驱动程序功能。 有关这些选项的详细信息，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。
