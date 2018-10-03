---
title: 滚动和提取行 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a0c0f7f2cad7eaecc212e2283fab7fc7d69f2ee7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48228737"
---
# <a name="scrolling-and-fetching-rows"></a>滚动和提取行
  若要使用可滚动游标，ODBC 应用程序必须：  
  
-   设置使用的游标功能[SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)。  
  
-   打开游标使用**SQLExecute**或**SQLExecDirect**。  
  
-   使用滚动和提取行**SQLFetch**或[SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md)。  
  
 这两**SQLFetch**并**SQLFetchSroll**可以一次提取行块。 使用指定返回的行数**SQLSetStmtAttr**设置 SQL_ATTR_ROW_ARRAY_SIZE 参数。  
  
 ODBC 应用程序可以使用**SQLFetch**通过只进游标提取。  
  
 **SQLFetchScroll**用于围绕游标滚动。 **SQLFetchScroll**支持提取下一步，以前版本中，第一个和最后一个行集除了相对提取 (提取行集*n*中当前行集的开始的行) 和绝对提取 （提取行集行开始*n*)。 如果*n*是负绝对提取中，行计数从结果集的末尾。 绝对提取行 -1 表示提取从结果集中最后一行开始的行集。  
  
 使用的应用程序**SQLFetchScroll**仅对其块游标功能，如报表，有可能通过结果集一次，仅使用此选项提取下一步的行集。 基于屏幕的应用程序，但是，可以充分利用所有的功能**SQLFetchScroll**。 如果应用程序将行集大小设置为在屏幕上显示的行数，并将屏幕缓冲区绑定到结果集，它可以将滚动条操作直接向调用转换**SQLFetchScroll**。  
  
|滚动条操作|SQLFetchScroll 滚动选项|  
|--------------------------|-------------------------------------|  
|向上翻页|SQL_FETCH_PRIOR|  
|向下翻页|SQL_FETCH_NEXT|  
|向上移动一行|SQL_FETCH_RELATIVE，FetchOffset 等于-1|  
|向下移动一行|SQL_FETCH_RELATIVE，FetchOffset 等于 1|  
|滚动框移到顶部|SQL_FETCH_FIRST|  
|滚动框移到底部|SQL_FETCH_LAST|  
|滚动框位于随机位置|SQL_FETCH_ABSOLUTE|  
  
## <a name="in-this-section"></a>本节内容  
  
-   [在 ODBC 中为行加书签](scrolling-and-fetching-rows-bookmarking-rows-in-odbc.md)  
  
## <a name="see-also"></a>请参阅  
 [使用游标&#40;ODBC&#41;](using-cursors-odbc.md)  
  
  
