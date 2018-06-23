---
title: 处理的结果 (ODBC) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- processing results [ODBC]
ms.assetid: 4810fe3f-78ee-4f0d-8bcc-a4659fbcf46f
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fa20ed943be8195eb7719265d3bd2ef0aa26a38c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015454"
---
# <a name="process-results-odbc"></a>处理结果 (ODBC)
    
### <a name="to-process-results"></a>处理结果  
  
1.  检索结果集信息。  
  
2.  如果使用了绑定列，则对每个要绑定的列，调用 [SQLBindCol](../native-client-odbc-api/sqlbindcol.md)，以将程序缓冲区绑定到该列。  
  
3.  对于结果集中的每一行：  
  
    -   调用 [SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401) 以获取下一行。  
  
    -   如果使用绑定列，则在绑定列缓冲区使用现在可用的数据。  
  
    -   如果使用绑定列，在最后一个绑定列后一次或多次调用 [SQLGetData](../native-client-odbc-api/sqlgetdata.md) 以获取未绑定列的数据。 调用`SQLGetData`应该是升序排列的列号。  
  
    -   多次调用 `SQLGetData` 以从 text 或 image 列获取数据。  
  
4.  当 [SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401) 通过返回 SQL_NO_DATA 指示到达结果集末尾时，调用 [SQLMoreResults](../native-client-odbc-api/sqlmoreresults.md) 确定是否有其他可用结果集。  
  
    -   如果返回 SQL_SUCCESS，则其他结果集可用。  
  
    -   如果返回 SQL_NO_DATA，则没有其他结果集可用。  
  
    -   如果返回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR，则调用 [SQLGetDiagRec](http://go.microsoft.com/fwlink/?LinkId=58402) 以确定来自 PRINT 或 RAISERROR 语句的输出是否可用。  
  
         如果将绑定语句参数用于某一存储过程的输出参数或返回值，则使用在绑定参数缓冲区中当前提供的数据。 此外，在使用绑定参数时，对 [SQLExecute](http://go.microsoft.com/fwlink/?LinkId=58400) 或 [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399) 的每个调用都将执行 *S* 次 SQL 语句，其中，*S* 是绑定参数数组中元素的数目。 这意味着，将存在 *S* 组要处理的结果，而其中每组结果都由所有结果集、输出参数以及 SQL 语句的单次执行通常返回的返回代码构成。  
  
    > [!NOTE]  
    >  在某一结果集包含计算行时，每个计算行都可作为单独的结果集提供。 这些计算结果集混杂在普通行内，并且将普通行分为多个结果集。  
  
5.  或者，使用 SQL_UNBIND 调用 [SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md) 以释放任何绑定列缓冲区。  
  
6.  如果其他结果集可用，则转到步骤 1。  
  
> [!NOTE]  
>  若要在 [SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401) 返回 SQL_NO_DATA 之前取消处理结果集，请调用 [SQLCloseCursor](../native-client-odbc-api/sqlclosecursor.md)。  
  
## <a name="see-also"></a>请参阅  
 [处理结果操作指南主题&#40;ODBC&#41;](../../database-engine/dev-guide/processing-results-how-to-topics-odbc.md)  
  
  