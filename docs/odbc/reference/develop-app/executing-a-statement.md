---
description: 执行语句
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ce060c91e2500b016e824e733d8189c99334e1b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461469"
---
# <a name="executing-a-statement"></a>执行语句
有四种方法可以执行语句，具体取决于编译语句 (由数据库引擎准备) 并定义这些语句：  
  
-   **直接执行** 应用程序定义 SQL 语句。 它在运行时通过单个步骤来准备并执行。  
  
-   **准备好的执行** 应用程序定义 SQL 语句。 它在运行时通过单独的步骤来准备并执行。 语句可准备一次，并可执行多次。  
  
-   **过程** 应用程序可以在开发时定义并编译一个或多个 SQL 语句，并将这些语句以过程的形式存储在数据源中。 在运行时一次或多次执行该过程。 应用程序可以使用目录函数枚举可用的存储过程。  
  
-   **目录函数** 驱动程序编写器创建一个返回预定义结果集的函数。 通常，此函数会提交预定义的 SQL 语句，或调用为此目的而创建的过程。 函数在运行时在一次或多次执行。  
  
 特定语句 (由其语句句柄标识) 可以执行任意多次。 语句可以使用各种不同的 SQL 语句执行，也可以使用相同的 SQL 语句重复执行。 例如，下面的代码使用 (*hstmt1*) 的相同语句句柄来检索和显示 Sales 数据库中的表。 然后重新使用此句柄来检索用户选择的表中的列。  
  
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
  
 下面的代码演示如何使用单个句柄重复执行相同的语句，以删除表中的行。  
  
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
  
 对于许多驱动程序，分配语句是一项昂贵的任务，因此以这种方式重用相同的语句通常比释放现有语句和分配新语句更有效。 在语句上创建结果集的应用程序必须在 reexecuting 语句之前，小心地在结果集上关闭游标;有关详细信息，请参阅 [关闭光标](../../../odbc/reference/develop-app/closing-the-cursor.md)。  
  
 重复使用语句还会强制应用程序避免在一次可以处于活动状态的语句数的某些驱动程序中出现限制。 "活动" 的确切定义是特定于驱动程序的，但它通常是指已准备好或执行并且仍具有可用结果的所有语句。 例如，在准备好 **INSERT** 语句后，该语句通常被视为处于活动状态;执行 **SELECT** 语句并使游标仍处于打开状态后，该语句通常被视为处于活动状态;执行 **CREATE TABLE** 语句后，通常不会将其视为处于活动状态。  
  
 应用程序通过使用 SQL_MAX_CONCURRENT_ACTIVITIES 选项调用 **SQLGetInfo** 来确定单个连接上可以同时处于活动状态的语句数。 通过打开到数据源的多个连接，应用程序可以使用比此限制更多的活动语句;不过，连接可能会消耗大量资源，因此应考虑对性能的影响。  
  
 应用程序可以使用 SQL_ATTR_QUERY_TIMEOUT 语句特性来限制为语句分配的时间量。 如果超时时间已过，则在数据源返回结果集之前，执行 SQL 语句的函数将返回 SQLSTATE HYT00 (超时过期时间) 。 默认情况下没有任何超时。  
  
 本部分包含以下主题。  
  
-   [直接执行](../../../odbc/reference/develop-app/direct-execution-odbc.md)  
  
-   [准备好的执行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)  
  
-   [过程](../../../odbc/reference/develop-app/procedures-odbc.md)  
  
-   [SQL 语句的批处理](../../../odbc/reference/develop-app/batches-of-sql-statements.md)  
  
-   [执行目录函数](../../../odbc/reference/develop-app/executing-catalog-functions.md)
