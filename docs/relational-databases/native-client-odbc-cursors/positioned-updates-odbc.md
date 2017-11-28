---
title: "定位更新 (ODBC) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
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
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a77f61ebd66cf6bda10d8c59c61e5364208a66e9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="positioned-updates-odbc"></a>定位更新 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC 支持通过两种方法在游标中执行定位更新：  
  
-   **SQLSetPos**  
  
-   WHERE CURRENT OF 子句  
  
 更为常见的方法是使用**SQLSetPos**。 它具有以下选项。  
  
 SQL_POSITION  
 将游标定位到当前行集中的特定行。  
  
 SQL_REFRESH  
 使用游标当前所定位行的值刷新被绑定到结果集列上的程序变量。  
  
 SQL_UPDATE  
 使用绑定到结果集列上的程序变量中所存储的值来更新游标中的当前行。  
  
 SQL_DELETE  
 删除游标中的当前行。  
  
 **SQLSetPos**可以与任何语句结果集语句句柄游标特性设置为使用服务器游标时使用。 结果集列必须绑定到程序变量。 应用程序提取行时，就会立即调用**SQLSetPos**(SQL_POSTION)，将光标定位在该行上。 随后应用程序可以调用 SQLSetPos(SQL_DELETE) 删除当前行，或者可以将新数据值移入绑定程序变量并调用 SQLSetPos(SQL_UPDATE) 更新当前行。  
  
 应用程序可以更新或删除任何行集中的行与**SQLSetPos**。 调用**SQLSetPos**是一个便捷替代方式构造和执行 SQL 语句。 **SQLSetPos**当前行集上运行并在调用后才可以使用[SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)。  
  
 通过调用设置行集大小[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)用 SQL_ATTR_ROW_ARRAY_SIZE 特性自变量。 **SQLSetPos**使用新的行集大小，但仅在调用**SQLFetch**或**SQLFetchScroll**。 例如，如果更改的行集大小， **SQLSetPos**调用，然后**SQLFetch**或**SQLFetchScroll**调用。 调用**SQLSetPos**使用旧的行集大小，但**SQLFetch**或**SQLFetchScroll**使用新的行集大小。  
  
 行集中的第一行的行编号为 1。 中的 RowNumber 参数**SQLSetPos**必须标识行集中的行; 即，其值必须介于 1 和最近提取的行数。 这可能小于行集大小。 如果 RowNumber 为 0，将对行集中的所有行应用操作。  
  
 删除操作的**SQLSetPos**使删除一个或多个选定的行的表的数据源。 若要删除的行**SQLSetPos**，应用程序调用**SQLSetPos**操作设置为 SQL_DELETE 与设置为的行数，以删除 RowNumber。 如果 RowNumber 为 0，将删除行集中的所有行。  
  
 后**SQLSetPos**返回时，已删除的行是当前行，并且其状态为 SQL_ROW_DELETED。 行不能在任何其他的定位操作，例如调用[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)或**SQLSetPos**。  
  
 当你删除所有行的行集 （RowNumber 等于 0） 时，应用程序可以防止驱动程序的更新操作就像使用行操作数组中删除某些行**SQLSetPos**。  
  
 每个删除的行都应该是结果集中存在的行。 如果应用程序缓冲区已被提取操作填充，并且保持了行状态数组，则所有这些行位置处的行值都不应为 SQL_ROW_DELETED、SQL_ROW_ERROR 或 SQL_ROW_NOROW。  
  
 通过在 UPDATE、DELETE 和 INSERT 语句中使用 WHERE CURRENT OF 子句，也可以执行定位更新。 当前的要求的位置游标命名该 ODBC 将生成时[SQLGetCursorName](../../relational-databases/native-client-odbc-api/sqlgetcursorname.md)调用函数时，或可以指定通过调用**SQLSetCursorName**。 以下是用于在 ODBC 应用程序中执行 WHERE CURRENT OF 更新的一般步骤：  
  
-   调用**SQLSetCursorName**建立语句句柄的游标名称。  
  
-   生成包含 FOR UPDATE OF 子句的 SELECT 语句，并执行该语句。  
  
-   调用**SQLFetchScroll**检索行集或**SQLFetch**来检索行。  
  
-   调用**SQLSetPos** (SQL_POSITION)，将光标定位在该行上。  
  
-   生成并带有 WHERE CURRENT OF 子句使用设置与该游标名称执行 UPDATE 语句**SQLSetCursorName**。  
  
 或者，可以调用**SQLGetCursorName**执行 SELECT 语句而不是调用后**SQLSetCursorName**执行 SELECT 语句之前。 **SQLGetCursorName**返回分配由 ODBC，如果你未设置游标名称使用的默认游标名称**SQLSetCursorName**。  
  
 **SQLSetPos**优于 WHERE CURRENT OF 当你使用服务器游标。 如果使用 ODBC 游标库中的静态、可更新游标，该游标库通过添加一个 WHERE 子句（带有基础表的键值）实现 WHERE CURRENT OF 更新。 如果表中的键不唯一，这可能导致意外更新。  
  
## <a name="see-also"></a>另请参阅  
 [使用游标 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
