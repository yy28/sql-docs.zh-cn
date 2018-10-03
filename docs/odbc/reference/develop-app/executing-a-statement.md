---
title: 执行语句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], executing
ms.assetid: e5f0d2ee-0453-4faf-b007-12978dd300a1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5660cfe2f264e0971d30cd2eaf1aadf68581321e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792965"
---
# <a name="executing-a-statement"></a>执行语句
有四种方法执行语句，具体取决于在编译 （准备） 数据库引擎和用户定义它们时：  
  
-   **直接执行**应用程序定义的 SQL 语句。 它已准备且在运行时单步执行。  
  
-   **准备好执行**应用程序定义的 SQL 语句。 它已准备且在运行时在单独的步骤中执行。 可以准备一次，多个多次执行该语句。  
  
-   **过程**应用程序可以定义和编译一个或多个 SQL 语句在开发时间并将这些语句存储在过程中对数据源。 在运行时的一个或多个时间执行该过程。 应用程序可以枚举可用的存储的过程使用目录函数。  
  
-   **目录函数**驱动程序编写器创建一个函数，返回预定义的结果集。 通常情况下，此函数将提交一个预定义的 SQL 语句，或调用实现此目的而创建的过程。 在运行时的一个或多个时间执行函数。  
  
 特定语句 （如由其语句句柄标识） 可以是执行任意次数。 可以使用各种不同的 SQL 语句，执行该语句，或可以使用相同的 SQL 语句重复执行。 例如，以下代码使用相同的语句句柄 (*hstmt1*) 来检索并显示在 Sales 数据库中的表。 然后，它重用此句柄来检索用户选定的表中的列。  
  
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
  
 和下面的代码演示如何使用的一个句柄来重复执行相同的语句，若要从表中删除行。  
  
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
  
 许多驱动程序，请分配语句是代价高昂的任务，以便重复使用相同的语句以这种方式是通常比让现有语句和分配新的效率更高。 必须注意结果集中重新执行该语句; 之前通过关闭游标的语句创建结果集的应用程序有关详细信息，请参阅[关闭游标](../../../odbc/reference/develop-app/closing-the-cursor.md)。  
  
 重用语句还会强制应用程序以避免某些驱动程序的一次可处于活动状态的语句数的限制。 "活动"的精确定义是特定于驱动程序，但它通常是指已准备或执行的任何语句并且仍具有可用的结果。 例如后,**插入**准备语句，则通常视为处于活动状态; 后**选择**执行语句和光标仍处于打开状态，它通常被认为是到处于活动状态;后**CREATE TABLE**执行语句，它不通常被视为处于活动状态。  
  
 应用程序确定多少语句可以通过调用一次在单个连接上处于活动状态**SQLGetInfo** SQL_MAX_CONCURRENT_ACTIVITIES 选项。 应用程序可以通过打开多个连接到数据源，则使用超过此限制的更多的活动语句由于连接可能很昂贵，但是，应考虑对性能的影响。  
  
 应用程序可以限制为一个语句来执行与 SQL_ATTR_QUERY_TIMEOUT 语句属性分配的时间量。 如果超时期限过期之前的数据源返回的结果集，执行 SQL 语句的函数将返回 SQLSTATE HYT00 （超时已过期）。 默认情况下，没有任何超时。  
  
 本部分包含以下主题。  
  
-   [直接执行](../../../odbc/reference/develop-app/direct-execution-odbc.md)  
  
-   [准备好的执行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)  
  
-   [过程](../../../odbc/reference/develop-app/procedures-odbc.md)  
  
-   [SQL 语句的批处理](../../../odbc/reference/develop-app/batches-of-sql-statements.md)  
  
-   [执行目录函数](../../../odbc/reference/develop-app/executing-catalog-functions.md)
