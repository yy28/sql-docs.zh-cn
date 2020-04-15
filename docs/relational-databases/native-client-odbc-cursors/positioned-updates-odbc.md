---
title: 定位更新 （ODBC） |微软文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 52495f670986638cac02661240e349713424256e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305319"
---
# <a name="positioned-updates-odbc"></a>定位更新 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC 支持通过两种方法在游标中执行定位更新：  
  
-   **SQLSetPos**  
  
-   WHERE CURRENT OF 子句  
  
 更常见的方法是使用**SQLSetPos**。 它具有以下选项。  
  
 SQL_POSITION  
 将游标定位到当前行集中的特定行。  
  
 SQL_REFRESH  
 使用游标当前所定位行的值刷新被绑定到结果集列上的程序变量。  
  
 SQL_UPDATE  
 使用绑定到结果集列上的程序变量中所存储的值来更新游标中的当前行。  
  
 SQL_DELETE  
 删除游标中的当前行。  
  
 当语句句柄游标属性设置为使用服务器游标时 **，SQLSetPos**可与任何语句结果集一起使用。 结果集列必须绑定到程序变量。 一旦应用程序获取了一行，它调用**SQLSetPos**（SQL_POSTION） 将光标定位在行上。 随后应用程序可以调用 SQLSetPos(SQL_DELETE) 删除当前行，或者可以将新数据值移入绑定程序变量并调用 SQLSetPos(SQL_UPDATE) 更新当前行。  
  
 应用程序可以使用**SQLSetPos**更新或删除行集中的任何行。 调用**SQLSetPos**是构造和执行 SQL 语句的便捷替代方法。 **SQLSetPos**在当前行集中运行，只能在调用[SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)后使用。  
  
 行集大小由对[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)的调用设置，属性参数为SQL_ATTR_ROW_ARRAY_SIZE。 **SQLSetPos**使用新的行集大小，但仅在调用**SQLFetch**或**SQLFetchScroll**后。 例如，如果更改了行集大小，则调用**SQLSetPos，** 然后调用**SQLFetch**或**SQLFetchScroll。** 对**SQLSetPos 的**调用使用旧的行集大小，但**SQLFetch**或**SQLFetchScroll**使用新的行集大小。  
  
 行集中的第一行的行编号为 1。 **SQLSetPos**中的行编号参数必须标识行集中的行;因此，在行集中，必须标识行数。也就是说，其值必须介于 1 和最近提取的行数之间。 这可能小于行集大小。 如果 RowNumber 为 0，将对行集中的所有行应用操作。  
  
 **SQLSetPos**的删除操作使数据源删除表的一个或多个选定行。 要删除**SQLSetPos 的**行，应用程序调用**SQLSetPos，** 操作设置为 SQL_DELETE，行号设置为要删除的行数。 如果 RowNumber 为 0，将删除行集中的所有行。  
  
 **SQLSetPos**返回后，已删除的行是当前行，其状态为SQL_ROW_DELETED。 该行不能用于任何其他定位操作，例如对[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)或**SQLSetPos**的调用。  
  
 当您删除行集的所有行（RowNumber 等于 0）时，应用程序可以阻止驱动程序使用行操作数组删除某些行，就像**SQLSetPos**的更新操作一样。  
  
 每个删除的行都应该是结果集中存在的行。 如果应用程序缓冲区已被提取操作填充，并且保持了行状态数组，则所有这些行位置处的行值都不应为 SQL_ROW_DELETED、SQL_ROW_ERROR 或 SQL_ROW_NOROW。  
  
 通过在 UPDATE、DELETE 和 INSERT 语句中使用 WHERE CURRENT OF 子句，也可以执行定位更新。 WHERE CURRENT OF 需要一个游标名称，在调用[SQLGetCursorName](../../relational-databases/native-client-odbc-api/sqlgetcursorname.md)函数时将生成 ODBC，或者可以通过调用**SQLSetCursorName**来指定该名称。 以下是用于在 ODBC 应用程序中执行 WHERE CURRENT OF 更新的一般步骤：  
  
-   调用**SQLSetCursorName**为语句句柄建立游标名称。  
  
-   生成包含 FOR UPDATE OF 子句的 SELECT 语句，并执行该语句。  
  
-   调用**SQLFetchScroll**以检索行集或**SQLFetch**以检索行。  
  
-   调用**SQLSetPos** （SQL_POSITION） 将光标放置在行上。  
  
-   使用带有**SQLSetCursorName**的游标名称集生成并执行具有 WHERE CURRENT OF 子句的更新语句。  
  
 或者，您可以在执行 SELECT 语句后调用**SQLGetCursorName，** 而不是在执行 SELECT 语句之前调用**SQLSetCursorName。** 如果不使用**SQLSetCursorName**设置游标名称 **，SQLGetCursorName**将返回由 ODBC 分配的默认游标名称。  
  
 当您使用服务器游标时 **，SQLSetPos**优先于 WHERE。 如果使用 ODBC 游标库中的静态、可更新游标，该游标库通过添加一个 WHERE 子句（带有基础表的键值）实现 WHERE CURRENT OF 更新。 如果表中的键不唯一，这可能导致意外更新。  
  
## <a name="see-also"></a>另请参阅  
 [使用光标&#40;ODBC&#41;](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
