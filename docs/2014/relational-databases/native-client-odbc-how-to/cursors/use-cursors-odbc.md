---
title: 使用游标（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], how to topics
ms.assetid: c502736f-bca0-45c3-ae25-d2ad52d296bf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fb3662bbd1bff6c7c7deb3a8eac61108ea93074a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63200483"
---
# <a name="use-cursors-odbc"></a>使用游标 (ODBC)
    
### <a name="to-use-cursors"></a>使用游标  
  
1.  调用 [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) 以设置所需的游标属性：  
  
     设置 SQL_ATTR_CURSOR_TYPE 和 SQL_ATTR_CONCURRENCY 属性（这是首选选项）。  
  
     或  
  
     设置 SQL_CURSOR_SCROLLABLE 和 SQL_CURSOR_SENSITIVITY 属性。  
  
2.  调用 [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) 以便通过使用 SQL_ATTR_ROW_ARRAY_SIZE 属性设置行集大小。  
  
3.  或者，如果将通过使用 WHERE CURRENT OF 子句完成定位更新，则调用 [SQLSetCursorName](https://go.microsoft.com/fwlink/?LinkId=58406) 以便设置游标名称。  
  
4.  执行 SQL 语句。  
  
5.  或者，如果将通过使用 WHERE CURRENT OF 子句完成定位更新并且游标名称没有在第 3 步中随 [SQLSetCursorName](https://go.microsoft.com/fwlink/?LinkId=58406) 提供，则调用 [SQLGetCursorName](../../native-client-odbc-api/sqlgetcursorname.md) 以获取游标名称。  
  
6.  调用 [SQLNumResultCols](../../native-client-odbc-api/sqlnumresultcols.md) 以获取行集中的列数 (C)。  
  
     使用按列绑定。  
  
     \- 或 -  
  
     使用按行绑定。  
  
7.  根据需要从游标提取行集。  
  
8.  调用 [SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md) 以确定其他结果集是否可用。  
  
    -   如果返回 SQL_SUCCESS，则其他结果集可用。  
  
    -   如果返回 SQL_NO_DATA，则没有其他结果集可用。  
  
    -   如果返回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR，则调用 [SQLGetDiagRec](https://go.microsoft.com/fwlink/?LinkId=58402) 以确定来自 PRINT 或 RAISERROR 语句的输出是否可用。  
  
     如果将绑定语句参数用于某一存储过程的输出参数或返回值，则使用在绑定参数缓冲区中当前提供的数据。  
  
     在使用绑定参数时，对 [SQLExecute](https://go.microsoft.com/fwlink/?LinkId=58400) 或 [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) 的每个调用都将执行 SQL 语句 S 次，其中，S 是绑定参数数组中元素的数目。 这意味着，将存在 S 组要处理的结果，而其中每组结果都由所有结果集、输出参数以及 SQL 语句的单次执行通常返回的返回代码构成。  
  
     请注意，在某一结果集包含计算行时，每个计算行都可作为单独的结果集生成。 这些计算结果集混杂在普通行内，并且将普通行分为多个结果集。  
  
9. 或者，使用 SQL_UNBIND 调用 [SQLFreeStmt](../../native-client-odbc-api/sqlfreestmt.md) 以释放任何绑定列缓冲区。  
  
10. 如果其他结果集可用，则转到步骤 6。  
  
     在步骤 9 中，对部分处理的结果集调用 [SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md) 将清除其余的结果集。 清除部分处理的结果集的另一个方法是调用 [SQLCloseCursor](../../native-client-odbc-api/sqlclosecursor.md)。  
  
     通过设置 SQL_ATTR_CURSOR_TYPE 和 SQL_ATTR_CONCURRENCY，或通过设置 SQL_ATTR_CURSOR_SENSITIVITY 和 SQL_ATTR_CURSOR_SCROLLABLE，可以控制所使用的游标类型。 不应将指定游标行为的两种方法混用。  
  
## <a name="see-also"></a>另请参阅  
 [使用游标操作指南主题 &#40;ODBC&#41;](using-cursors-how-to-topics-odbc.md)  
  
  
