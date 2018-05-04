---
title: 执行语句 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], executing
ms.assetid: e5f0d2ee-0453-4faf-b007-12978dd300a1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c111620b2f06e7b2eacb159d7cf1c8817bd27c59
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="executing-a-statement"></a>执行语句
有四种方法执行语句，具体取决于时对它们进行编译 （准备） 的数据库引擎和用户定义它们：  
  
-   **指示执行**应用程序定义的 SQL 语句。 它准备并在运行时在单步执行。  
  
-   **准备好执行**应用程序定义的 SQL 语句。 它准备并执行运行时在单独的步骤。 可以一次准备的语句，并执行多次。  
  
-   **过程**应用程序可以定义和编译的一个或多个 SQL 语句在开发时间和存储这些语句，在过程中对数据源。 在运行时的一个或多个时间执行过程。 应用程序可以枚举使用目录函数的可用存储的过程。  
  
-   **目录函数**驱动程序编写器创建返回预定义的结果集的函数。 通常情况下，此函数将提交的预定义的 SQL 语句，或调用为此目的创建的过程。 在运行时的一个或多个时间执行函数。  
  
 某一特定语句 （如标识由其语句句柄） 可以是执行任意次数。 可以使用各种不同的 SQL 语句执行的语句或可使用相同的 SQL 语句重复执行。 例如，下面的代码使用相同的语句句柄 (*hstmt1*) 以检索并显示在 Sales 数据库的表。 然后，它会重用此句柄来检索用户选定的表中的列。  
  
```  
SQLHSTMT    hstmt1;  
SQLCHAR *   Table;  
  
// Create a result set of all tables in the Sales database.  
SQLTables(hstmt1, "Sales", SQL_NTS, "sysadmin", SQL_NTS, NULL, 0, NULL, 0);  
  
// Fetch and display the table names; then close the cursor.  
// Code not shown.  
  
// Have the user select a particular table.  
SelectTable(Table);  
  
// Reuse hstmt1 to create a result set of all columns in Table.  
SQLColumns(hstmt1, "Sales", SQL_NTS, "sysadmin", SQL_NTS, Table, SQL_NTS, NULL, 0);  
  
// Fetch and display the column names in Table; then close the cursor.  
// Code not shown.  
```  
  
 和下面的代码演示如何使用的一个句柄以重复执行相同的语句，以从表中删除行。  
  
```  
SQLHSTMT      hstmt1;  
SQLUINTEGER   OrderID;  
SQLINTEGER    OrderIDInd = 0;  
  
// Prepare a statement to delete orders from the Orders table.  
SQLPrepare(hstmt1, "DELETE FROM Orders WHERE OrderID = ?", SQL_NTS);  
  
// Bind OrderID to the parameter for the OrderID column.  
SQLBindParameter(hstmt1, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &OrderID, 0, &OrderIDInd);  
  
// Repeatedly execute hstmt1 with different values of OrderID.  
while ((OrderID = GetOrderID()) != 0) {  
   SQLExecute(hstmt1);  
}  
```  
  
 对于许多驱动程序，分配语句是一个昂贵的任务、，以便重复使用相同的语句，以这种方式是通常比释放现有语句和正在分配新的效率更高。 一条语句创建结果集的应用程序必须小心地将其通过设置 reexecuting 语句; 之前的结果时关闭游标有关详细信息，请参阅[关闭光标](../../../odbc/reference/develop-app/closing-the-cursor.md)。  
  
 重用语句还会强制应用程序中以免中一次可以处于活动状态的语句数的某些驱动程序的限制。 "活动"的确切定义特定于驱动程序，但它通常是指已准备或执行的任何语句和仍然具有可用的结果。 例如之后,**插入**准备语句，它通常被视为处于活动状态; 后**选择**执行语句和光标是仍处于打开状态，通常被视为到处于活动状态;后**CREATE TABLE**执行语句，则它不通常被视为处于活动状态。  
  
 应用程序确定多少语句可通过调用一次在单个连接上处于活动状态**SQLGetInfo** SQL_MAX_CONCURRENT_ACTIVITIES 选项。 应用程序可以通过打开多个连接到数据源，则使用超过此限制的更多活动语句因为连接是昂贵，但是，应考虑对性能的影响。  
  
 应用程序可以为一个语句来执行与 SQL_ATTR_QUERY_TIMEOUT 语句属性分配的时间量限制。 如果在超时期限过期之前的数据源返回的结果集，执行 SQL 语句函数将返回 SQLSTATE HYT00 （超时）。 默认情况下，没有任何超时。  
  
 本部分包含以下主题。  
  
-   [直接执行](../../../odbc/reference/develop-app/direct-execution-odbc.md)  
  
-   [准备好的执行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)  
  
-   [过程](../../../odbc/reference/develop-app/procedures-odbc.md)  
  
-   [SQL 语句的批处理](../../../odbc/reference/develop-app/batches-of-sql-statements.md)  
  
-   [执行目录函数](../../../odbc/reference/develop-app/executing-catalog-functions.md)
