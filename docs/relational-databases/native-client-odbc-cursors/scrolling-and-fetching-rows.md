---
title: 滚动和提取行 |微软文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- scrollable cursors [SQL Server]
- SQL Server Native Client ODBC driver, cursors
- SQLFetchScroll function
- ODBC applications, cursors
- cursors [ODBC], fetching rows
- ODBC cursors, fetching rows
- cursors [ODBC], scrolling rows
- fetching [ODBC]
- ODBC cursors, scrolling rows
ms.assetid: 9109f10d-326b-4a6d-8c97-831f60da8c4c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0ae9f1079f329951045d4b3f61b39c12efc153fb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302483"
---
# <a name="scrolling-and-fetching-rows"></a>滚动和提取行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  若要使用可滚动游标，ODBC 应用程序必须：  
  
-   使用[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)设置游标功能。  
  
-   使用**SQLExecute**或**SQLExecDirect**打开光标。  
  
-   使用**SQLFetch**或[SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)滚动和提取行。  
  
 **SQLFetch**和**SQLFetchSroll**可以一次获取行块。 返回的行数通过使用**SQLSetStmtAttr**设置SQL_ATTR_ROW_ARRAY_SIZE参数来指定。  
  
 ODBC 应用程序可以使用**SQLFetch**通过仅转发游标进行获取。  
  
 **SQLFetchScroll**用于滚动光标。 **SQLFetchScroll**支持提取下一个、先行、第一行和最后一个行集，除了相对提取（从当前行集的开头提取行 *）* 和绝对提取（从行*n*开始提取行集）。 如果*n*在绝对提取中为负数，则行将从结果集的末尾计数。 绝对提取行 -1 表示提取从结果集中最后一行开始的行集。  
  
 仅对其块游标功能（如报表）使用**SQLFetchScroll**的应用程序可能会通过结果集一次，仅使用该选项获取下一个行集。 另一方面，基于屏幕的应用程序可以利用**SQLFetchScroll**的所有功能。 如果应用程序将行集大小设置为屏幕上显示的行数，并将屏幕缓冲区绑定到结果集，则可以将滚动条操作直接转换为对**SQLFetchScroll**的调用。  
  
|滚动条操作|SQLFetchScroll 滚动选项|  
|--------------------------|-------------------------------------|  
|向上翻页|SQL_FETCH_PRIOR|  
|向下翻页|SQL_FETCH_NEXT|  
|向上移动一行|SQL_FETCH_RELATIVE提取偏移量等于 -1|  
|向下移动一行|SQL_FETCH_RELATIVE，FetchOffset 等于 1|  
|滚动框移到顶部|SQL_FETCH_FIRST|  
|滚动框移到底部|SQL_FETCH_LAST|  
|滚动框位于随机位置|SQL_FETCH_ABSOLUTE|  
  
## <a name="in-this-section"></a>本节内容  
  
-   [在 ODBC 中为行加书签](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows-bookmarking-rows-in-odbc.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用光标&#40;ODBC&#41;](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
