---
title: 定位更新 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- SQLSetPos function
- SQLSetCursorName function
- ODBC applications, cursors
- cursors [ODBC], positioned updates
- positioned updates [ODBC]
- ODBC cursors, positioned updates
ms.assetid: ff404e02-630f-474d-b5d4-06442b756991
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2336944b583b6077d75bd5155bb4b52c66d9a852
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200521"
---
# <a name="positioned-updates-odbc"></a>定位更新 (ODBC)
  ODBC 支持通过两种方法在游标中执行定位更新：  
  
-   **SQLSetPos**  
  
-   WHERE CURRENT OF 子句  
  
 更常见的方式是使用**SQLSetPos**。 它具有以下选项。  
  
 SQL_POSITION  
 将游标定位到当前行集中的特定行。  
  
 SQL_REFRESH  
 使用游标当前所定位行的值刷新被绑定到结果集列上的程序变量。  
  
 SQL_UPDATE  
 使用绑定到结果集列上的程序变量中所存储的值来更新游标中的当前行。  
  
 SQL_DELETE  
 删除游标中的当前行。  
  
 **SQLSetPos**可以用于任意语句结果集的语句句柄游标属性设置为使用服务器游标时。 结果集列必须绑定到程序变量。 应用程序一旦提取了某行时，就立即调用**SQLSetPos**(SQL_POSTION) 将游标定位在该行上。 随后应用程序可以调用 SQLSetPos(SQL_DELETE) 删除当前行，或者可以将新数据值移入绑定程序变量并调用 SQLSetPos(SQL_UPDATE) 更新当前行。  
  
 应用程序可以更新或删除行集与中的任意一行**SQLSetPos**。 调用**SQLSetPos**是一个便捷替代方式构造和执行 SQL 语句。 **SQLSetPos**对当前行集进行操作并在调用后才可以在[SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md)。  
  
 通过调用设置行集大小[SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)带有属性参数 SQL_ATTR_ROW_ARRAY_SIZE。 **SQLSetPos**使用新的行集大小，但仅在调用**SQLFetch**或**SQLFetchScroll**。 例如，如果行集大小已更改， **SQLSetPos**调用，然后**SQLFetch**或**SQLFetchScroll**调用。 在调用**SQLSetPos**使用旧的行集大小，但**SQLFetch**或**SQLFetchScroll**使用新的行集大小。  
  
 行集中的第一行的行编号为 1。 中的 RowNumber 参数**SQLSetPos**必须标识行集中的行; 即，其值必须介于 1 和最近提取的行数。 这可能小于行集大小。 如果 RowNumber 为 0，将对行集中的所有行应用操作。  
  
 删除操作的**SQLSetPos**使数据源中删除一个或多个所选的表的行。 若要删除的行**SQLSetPos**，应用程序调用**SQLSetPos**与操作设置为 SQL_DELETE，将 RowNumber 设置为的行数，以删除。 如果 RowNumber 为 0，将删除行集中的所有行。  
  
 之后**SQLSetPos**返回时，已删除的行是当前行，其状态为 SQL_ROW_DELETED。 行不能用于任何其他定位操作，如调用[SQLGetData](../native-client-odbc-api/sqlgetdata.md)或**SQLSetPos**。  
  
 应用程序时，删除所有行 （RowNumber 为 0） 的行集，可以删除特定行的更新操作就像使用行操作数组阻止驱动程序**SQLSetPos**。  
  
 每个删除的行都应该是结果集中存在的行。 如果应用程序缓冲区已被提取操作填充，并且保持了行状态数组，则所有这些行位置处的行值都不应为 SQL_ROW_DELETED、SQL_ROW_ERROR 或 SQL_ROW_NOROW。  
  
 通过在 UPDATE、DELETE 和 INSERT 语句中使用 WHERE CURRENT OF 子句，也可以执行定位更新。 WHERE CURRENT OF 要求游标命名该 ODBC 将生成何时[SQLGetCursorName](../native-client-odbc-api/sqlgetcursorname.md)调用函数时，或可以指定通过调用**SQLSetCursorName**。 以下是用于在 ODBC 应用程序中执行 WHERE CURRENT OF 更新的一般步骤：  
  
-   调用**SQLSetCursorName**建立语句句柄的游标名称。  
  
-   生成包含 FOR UPDATE OF 子句的 SELECT 语句，并执行该语句。  
  
-   调用**SQLFetchScroll**检索行集或**SQLFetch**检索行。  
  
-   调用**SQLSetPos** (SQL_POSITION) 将游标定位在该行上。  
  
-   生成并与使用游标名称设置使用 WHERE CURRENT OF 子句执行 UPDATE 语句**SQLSetCursorName**。  
  
 或者，您可以调用**SQLGetCursorName**执行 SELECT 语句而不是调用后**SQLSetCursorName**之前执行 SELECT 语句。 **SQLGetCursorName**返回 odbc 分配，如果未设置游标名称使用的默认游标名称**SQLSetCursorName**。  
  
 **SQLSetPos**优于 WHERE CURRENT OF 时使用服务器游标。 如果使用 ODBC 游标库中的静态、可更新游标，该游标库通过添加一个 WHERE 子句（带有基础表的键值）实现 WHERE CURRENT OF 更新。 如果表中的键不唯一，这可能导致意外更新。  
  
## <a name="see-also"></a>请参阅  
 [使用游标&#40;ODBC&#41;](using-cursors-odbc.md)  
  
  
