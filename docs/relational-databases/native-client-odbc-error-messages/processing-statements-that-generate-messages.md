---
title: 处理生成消息的语句 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-error-messages
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- PRINT statement
- messages [ODBC], statements generating messages
- statements [ODBC], message generation
- errors [ODBC], statements generating messages
- SQL Server Native Client ODBC driver, errors
- STATISTICS IO option
- STATISTICS TIME option
- DBCC statements
- SQLExecute function
- RAISERROR statement
- SQLGetDiagRec function
- ODBC error handling, statements generating messages
- SQLExecDirect function
ms.assetid: 672ebdc5-7fa1-4ceb-8d52-fd25ef646654
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c1f7e84dc79bce17ffe1764ea2e9aa972d0e6eaf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="processing-statements-that-generate-messages"></a>处理生成消息的语句
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] SET 语句选项 STATISTICS TIME 和 STATISTICS IO 用于获取有助于诊断长时间运行的查询的信息。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本还支持用于分析查询计划的 SHOWPLAN 选项。 ODBC 应用程序可通过执行以下语句设置这些选项：  
  
```  
SQLExecDirect(hstmt, "SET SHOWPLAN ON", SQL_NTS);  
SQLExecDirect(hstmt, "SET STATISTICS TIME ON", SQL_NTS90  
);  
SQLExecDirect(hstmt, "SET STATISTICS IO ON", SQL_NTS);  
```  
  
 在 SET STATISTICS TIME 或 SET SHOWPLAN 都 ON， **SQLExecute**和**SQLExecDirect**返回 SQL_SUCCESS_WITH_INFO，并，此时，应用程序可以检索 SHOWPLAN 或统计信息时间输出通过调用**SQLGetDiagRec**直到它返回 SQL_NO_DATA。 SHOWPLAN 数据的每一行均按以下格式返回：  
  
```  
szSqlState="01000", *pfNativeError=6223,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]   
              Table Scan"  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 版将 SHOWPLAN 选项替换为 SHOWPLAN_ALL 和 SHOWPLAN_TEXT，后两个选项均将输出作为结果集（而不是一组消息）返回。  
  
 STATISTICS TIME 的每一行均按以下格式返回：  
  
```  
szSqlState="01000", *pfNativeError= 3613,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]  
   SQL Server Parse and Compile Time: cpu time = 0 ms."  
```  
  
 在到达结果集的末尾之前，SET STATISTICS IO 的输出不可用。 若要获取 STATISTICS IO 输出，应用程序调用**SQLGetDiagRec**时**SQLFetch**或[SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)返回 SQL_NO_DATA。 STATISTICS IO 的输出按以下格式返回：  
  
```  
szSqlState="01000", *pfNativeError= 3615,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Table: testshow  scan count 1,  logical reads: 1,  
   physical reads: 0."  
```  
  
## <a name="using-dbcc-statements"></a>使用 DBCC 语句  
 DBCC 语句将其数据作为消息（而不是结果集）返回。 **SQLExecDirect**或**SQLExecute**返回 SQL_SUCCESS_WITH_INFO 和应用程序通过调用检索输出**SQLGetDiagRec**直到它返回 SQL_NO_DATA。  
  
 例如，下面的语句返回 SQL_SUCCESS_WITH_INFO：  
  
```  
SQLExecDirect(hstmt, "DBCC CHECKTABLE(Authors)", SQL_NTS);  
```  
  
 调用**SQLGetDiagRec**返回：  
  
```  
szSqlState = "01000", *pfNativeError = 2536,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Checking authors"  
szSqlState = "01000", *pfNativeError = 2579,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   The total number of data pages in this table is 1."  
szSqlState = "01000", *pfNativeError = 7929,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Table has 23 data rows."  
szSqlState = "01000", *pfNativeError = 2528  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   DBCC execution completed. If DBCC printed error messages,  
   see your System Administrator."  
```  
  
## <a name="using-print-and-raiserror-statements"></a>使用 PRINT 和 RAISERROR 语句  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] PRINT 和 RAISERROR 语句还通过调用返回数据**SQLGetDiagRec**。 打印语句会导致 SQL 语句执行返回 SQL_SUCCESS_WITH_INFO 和的后续调用**SQLGetDiagRec**返回*SQLState* 01000。 严重性为 10 或更低的 RAISERROR 在行为上与 PRINT 相同。 严重级别为 11 或更高版本 RAISERROR 导致执行返回 SQL_ERROR 和的后续调用**SQLGetDiagRec**返回*SQLState* 42000。 例如，下面的语句返回 SQL_SUCCESS_WITH_INFO：  
  
```  
SQLExecDirect (hstmt, "PRINT  'Some message' ", SQL_NTS);  
```  
  
 调用**SQLGetDiagRec**返回：  
  
```  
szSQLState = "01000", *pfNative Error = 0,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Some message"  
```  
  
 下面的语句返回 SQL_SUCCESS_WITH_INFO：  
  
```  
SQLExecDirect (hstmt, "RAISERROR ('Sample error 1.', 10, -1)",  
   SQL_NTS)  
```  
  
 调用**SQLGetDiagRec**返回：  
  
```  
szSQLState = "01000", *pfNative Error = 50000,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Sample error 1."  
```  
  
 下面的语句返回 SQL_ERROR：  
  
```  
SQLExecDirect (hstmt, "RAISERROR ('Sample error 2.', 11, -1)", SQL_NTS)  
```  
  
 调用**SQLGetDiagRec**返回：  
  
```  
szSQLState = "42000", *pfNative Error = 50000,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Sample error 2."  
```  
  
 调用的计时**SQLGetDiagRec**是关键，从打印或 RAISERROR 语句的输出包含在结果集时。 调用**SQLGetDiagRec**要检索的打印或 RAISERROR 输出必须进行紧跟接收 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 的语句。 当仅执行一个 SQL 语句时（如上述示例中所示），这非常简单。 在这些情况下，调用**SQLExecDirect**或**SQLExecute**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 和**SQLGetDiagRec**然后，可以调用。 当编写循环代码以处理一批 SQL 语句的输出或者当执行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储过程时，这要复杂一些。  
  
 在这种情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 为在批处理或存储过程中执行的每个 SELECT 语句返回一个结果集。 如果批处理或过程包含 PRINT 或 RAISERROR 语句，它们的输出将与 SELECT 语句结果集交叉。 如果在批处理或过程的第一个语句是打印或 RAISERROR， **SQLExecute**或**SQLExecDirect**返回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR 和应用程序需要调用**SQLGetDiagRec**直到它返回 SQL_NO_DATA 检索的打印或 RAISERROR 信息。  
  
 如果打印或 RAISERROR 语句之后的 SQL 语句 （如 SELECT 语句），则时返回的打印或 RAISERROR 信息[SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)结果的位置设置包含错误。 **SQLMoreResults**返回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR，具体取决于消息的严重性。 通过调用中检索消息时**SQLGetDiagRec**直到它返回 SQL_NO_DATA。  
  
## <a name="see-also"></a>另请参阅  
 [处理错误和消息](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
