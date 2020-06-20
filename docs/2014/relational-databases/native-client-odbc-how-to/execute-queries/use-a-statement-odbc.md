---
title: 使用语句（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- statements [ODBC]
ms.assetid: f7573f8f-6f21-4e03-8dd5-a5f2ea4878cc
author: rothja
ms.author: jroth
ms.openlocfilehash: 5aea14840dd92c0fa6fb571081044e2d84e0f27b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85018705"
---
# <a name="use-a-statement-odbc"></a>使用语句 (ODBC)
    
### <a name="to-use-a-statement"></a>使用语句  
  
1.  调用 [SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396)，同时将 *HandleType* 设置为 SQL_HANDLE_STMT，以分配语句句柄。  
  
2.  （可选）调用 [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) 以设置语句选项，或调用 [SQLGetStmtAttr](../../native-client-odbc-api/sqlgetstmtattr.md) 以获取语句属性。  
  
     若要使用服务器游标，必须将游标属性设置为其默认值之外的值。  
  
3.  （可选）如果要多次执行此语句，可以使用 [SQLPrepare 函数](https://go.microsoft.com/fwlink/?LinkId=59360)准备要执行的语句。  
  
4.  （可选）如果语句具有绑定参数标记，通过使用 [SQLBindParameter](../../native-client-odbc-api/sqlbindparameter.md) 将参数标记绑定到程序变量。 如果是准备的语句，则可以调用 [SQLNumParams](https://go.microsoft.com/fwlink/?LinkId=58404) 和 [SQLDescribeParam](../../native-client-odbc-api/sqldescribeparam.md) 以查找参数的数目和特征。  
  
5.  使用 SQLExecDirect 直接执行语句。  
  
     \- 或 -  
  
     如果是准备的语句，则可以使用 [SQLExecute](https://go.microsoft.com/fwlink/?LinkId=58400) 多次执行该语句。  
  
     \- 或 -  
  
     调用可返回结果的目录函数。  
  
6.  采用以下方法处理结果：将结果集列绑定到程序变量、通过使用 [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) 将数据从结果集列移至程序变量，或是结合使用这两种方法。  
  
     从语句的结果集中提取，每次提取一行。  
  
     \- 或 -  
  
     通过使用块游标从结果集中提取，每次提取多个行。  
  
     \- 或 -  
  
     调用 [SQLRowCount](../../native-client-odbc-api/sqlrowcount.md) 以确定 INSERT、UPDATE 或 DELETE 语句影响的行数。  
  
     如果 SQL 语句可以有多个结果集，在每个结果集的末尾调用 [SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md) 以查看是否还有更多待处理的结果集。  
  
7.  处理完结果后，可能需要执行以下操作，令语句句柄可用于执行新语句：  
  
    -   如果未调用 [SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md)，直到它返回 SQL_NO_DATA，则调用 [SQLCloseCursor](../../native-client-odbc-api/sqlclosecursor.md) 以关闭游标。  
  
    -   如果将参数标记绑定到程序变量，则调用 [SQLFreeStmt](../../native-client-odbc-api/sqlfreestmt.md)（同时将 *Option* 设置为 SQL_RESET_PARAMS）以释放绑定参数。  
  
    -   如果将结果集列绑定到程序变量，则调用 [SQLFreeStmt](../../native-client-odbc-api/sqlfreestmt.md)（同时将 *Option* 设置为 SQL_UNBIND）以释放绑定列。  
  
    -   若要重用语句句柄，请转至步骤 2。  
  
8.  调用 [SQLFreeHandle](../../native-client-odbc-api/sqlfreehandle.md)，同时将 *HandleType* 设置为 SQL_HANDLE_STMT，以释放语句句柄。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;ODBC&#41;执行查询操作指南主题](executing-queries-how-to-topics-odbc.md)  
  
  
