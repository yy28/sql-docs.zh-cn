---
title: 执行语句 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c3ce09809c896a4d1d9333da00367f972655f96b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305738"
---
# <a name="executing-a-statement"></a>执行语句
执行语句有四种方法，具体取决于数据库引擎编译（准备）报表以及定义语句的人员：  
  
-   **直接执行**应用程序定义 SQL 语句。 它在运行时以单个步骤准备和执行。  
  
-   **已准备好的执行**应用程序定义 SQL 语句。 它在运行时以单独的步骤准备和执行。 语句可以准备一次，并多次执行。  
  
-   **程序**应用程序可以在开发时定义和编译一个或多个 SQL 语句，并将这些语句存储到数据源中作为过程。 该过程在运行时执行一次或多次。 应用程序可以使用目录函数枚举可用的存储过程。  
  
-   **目录功能**驱动程序编写器创建返回预定义结果集的函数。 通常，此函数提交预定义的 SQL 语句或调用为此目的创建的过程。 该函数在运行时执行一次或多次。  
  
 特定语句（由其语句句柄标识）可以执行任意次数。 语句可以使用各种不同的 SQL 语句执行，也可以使用相同的 SQL 语句重复执行。 例如，以下代码使用相同的语句句柄 （*hstmt1*） 来检索和显示 Sales 数据库中的表。 然后，它重用此句柄以检索用户选择的表中的列。  
  
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
  
 以下代码显示了如何使用单个句柄重复执行同一语句以从表中删除行。  
  
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
  
 对于许多驱动程序来说，分配语句是一项昂贵的任务，因此以这种方式重用同一语句通常比释放现有语句和分配新语句更有效。 在语句上创建结果集的应用程序在重新执行语句之前必须小心关闭结果集上的游标;有关详细信息，请参阅[关闭光标](../../../odbc/reference/develop-app/closing-the-cursor.md)。  
  
 重用语句还强制应用程序避免某些驱动程序中一次处于活动状态的语句数的限制。 "活动"的确切定义特定于驱动程序，但它通常是指已准备或执行但仍具有可用结果的任何语句。 例如，在编写**INSERT**语句后，通常认为它处于活动状态;因此，它通常被视为处于活动状态。执行**SELECT**语句且游标仍处于打开状态后，通常将其视为处于活动状态;因此，该语句通常被视为处于活动状态。在执行**CREATE TABLE**语句后，通常不将其视为活动。  
  
 应用程序通过使用SQL_MAX_CONCURRENT_ACTIVITIES选项调用**SQLGetInfo，** 确定一次在单个连接上可以处于活动状态的语句数。 应用程序可以通过打开到数据源的多个连接来使用比此限制更活跃的语句;但是，由于连接可能非常昂贵，因此应考虑对性能的影响。  
  
 应用程序可以限制为语句分配的时间量，以便使用 SQL_ATTR_QUERY_TIMEOUT 语句属性执行。 如果超时期限在数据源返回结果集之前过期，则执行 SQL 语句的函数将返回 SQLSTATE HYT00（超时已过期）。 默认情况下没有任何超时。  
  
 本部分包含以下主题。  
  
-   [直接执行](../../../odbc/reference/develop-app/direct-execution-odbc.md)  
  
-   [准备好的执行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)  
  
-   [过程](../../../odbc/reference/develop-app/procedures-odbc.md)  
  
-   [SQL 语句的批处理](../../../odbc/reference/develop-app/batches-of-sql-statements.md)  
  
-   [执行目录函数](../../../odbc/reference/develop-app/executing-catalog-functions.md)
