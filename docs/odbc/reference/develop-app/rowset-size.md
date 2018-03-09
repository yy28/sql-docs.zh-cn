---
title: "行集大小 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rowset size [ODBC]
- cursors [ODBC], block
- result sets [ODBC], rowset size
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 60366ae8-175c-456a-ae5e-bdd860786911
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0eb3e03c3fd2cad60b8f4a0e6c65aaaebbda03bb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="rowset-size"></a>行集大小
要使用哪些行集大小取决于应用程序。 基于屏幕的应用程序通常按照两个策略之一。 第一种是将行集大小设置为显示在屏幕; 上的行数如果用户调整屏幕的大小，应用程序做相应更改的行集大小。 第二个是行集的大小设置为一个更大数字，如 100，从而减少了对数据源的调用数。 应用程序内的行集尽可能本地滚动，并仅在它滚动外部行集时提取新行。  
  
 其他应用程序，如报表，往往会将行集大小设置为最大的应用程序可以合理地处理的行数-具有更大的行集，有时减少网络开销每行。 恰好一个行集可以设置为多大取决于每个行和可用内存量的大小。  
  
 通过调用设置行集大小**SQLSetStmtAttr**与*属性*SQL_ATTR_ROW_ARRAY_SIZE 自变量。 应用程序可以更改的行集大小，将新行集缓冲区 (通过调用**SQLBindCol**或指定绑定的偏移量) 甚至已提取行后，和/或文件名。 更改的行集大小的含义取决于该函数：  
  
-   **SQLFetch**和**SQLFetchScroll**在调用时使用的行集大小，以确定要提取的行数。 但是， **SQLFetchScroll**与*FetchOrientation*的 SQL_FETCH_NEXT 增量光标基于上次读取和然后提取行集上基于当前的行集大小的行集。  
  
-   **SQLSetPos**使用实际上是从前面调用开始的行集大小**SQLFetch**或**SQLFetchScroll**，这是因为**SQLSetPos**进行操作已设置的行集。 **SQLSetPos**还将可以选取最新的行集大小如果**SQLBulkOperations**后已更改的行集大小已调用。  
  
-   **SQLBulkOperations**使用行集的大小实际上在时调用，因为它执行独立于任何提取的行集表的操作。
