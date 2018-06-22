---
title: 滚动和提取行 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c31b5a4d086fec3ac3db6e3eb1bfbd6bf54c8cb3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014528"
---
# <a name="scrolling-and-fetching-rows"></a>滚动和提取行
  若要使用可滚动游标，ODBC 应用程序必须：  
  
-   设置使用的游标功能[SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)。  
  
-   打开光标使用**SQLExecute**或**SQLExecDirect**。  
  
-   使用滚动和提取行**SQLFetch**或[SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md)。  
  
 同时**SQLFetch**和**SQLFetchSroll**可以一次提取的行的块。 使用指定返回的行数**SQLSetStmtAttr**设置 SQL_ATTR_ROW_ARRAY_SIZE 参数。  
  
 ODBC 应用程序可以使用**SQLFetch**通过只进游标提取。  
  
 **SQLFetchScroll**用于解决游标滚动。 **SQLFetchScroll**支持提取下一行，之前，第一个和最后一个行集除了相对提取 (提取行集*n*从开始的当前行集的行) 和绝对提取 （提取行集从行开始*n*)。 如果*n*是中的绝对读取负，行进行计数从结果集的末尾。 绝对提取行 -1 表示提取从结果集中最后一行开始的行集。  
  
 应用程序使用**SQLFetchScroll**仅为其块光标功能，如报表，可能会将结果集通过一次仅选项用于提取下一步的行集。 基于屏幕的应用程序，另一方面，可以充分利用所有功能的**SQLFetchScroll**。 如果应用程序将行集大小设置为在屏幕上显示的行数，并将屏幕缓冲区绑定到结果集，它可以转换滚动栏操作直接调用**SQLFetchScroll**。  
  
|滚动条操作|SQLFetchScroll 滚动选项|  
|--------------------------|-------------------------------------|  
|向上翻页|SQL_FETCH_PRIOR|  
|向下翻页|SQL_FETCH_NEXT|  
|向上移动一行|SQL_FETCH_RELATIVE 与 FetchOffset 等于-1|  
|向下移动一行|SQL_FETCH_RELATIVE，FetchOffset 等于 1|  
|滚动框移到顶部|SQL_FETCH_FIRST|  
|滚动框移到底部|SQL_FETCH_LAST|  
|滚动框位于随机位置|SQL_FETCH_ABSOLUTE|  
  
## <a name="in-this-section"></a>本节内容  
  
-   [在 ODBC 中为行加书签](scrolling-and-fetching-rows-bookmarking-rows-in-odbc.md)  
  
## <a name="see-also"></a>请参阅  
 [使用游标， &#40;ODBC&#41;](using-cursors-odbc.md)  
  
  