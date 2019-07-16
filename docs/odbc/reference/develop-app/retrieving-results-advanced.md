---
title: 检索结果 （高级） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- offsets [ODBC]
- result sets [ODBC], about result sets
- bind offsets [ODBC]
ms.assetid: bc00c379-71a7-407a-975c-898243f39bb6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22a88a96b856ba0976dcb8600d26f78b772654bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020502"
---
# <a name="retrieving-results-advanced"></a>检索结果（高级）
应用程序可以指定偏移量添加以绑定到数据缓冲区地址和相应的长度/指示器缓冲区地址何时**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**调用。 这些新增功能的结果确定这些操作中使用的地址。  
  
 绑定的偏移量允许应用程序更改而无需调用绑定**SQLBindCol**对于以前绑定列。 调用**SQLBindCol**重新绑定数据更改的缓冲区地址和长度/指示器指针。 重新绑定带有偏移量，另一方面，只需将偏移量添加到现有的绑定的数据缓冲区地址和长度/指示器缓冲区地址。 当使用偏移量时，绑定是一个"模板"的应用程序缓冲区的布局方式和应用程序可此"模板"通过移动到不同区域的内存更改偏移量。 新的偏移量可以指定在任何时间，并且始终添加到最初绑定值。  
  
 若要指定绑定偏移量，该应用程序设置为 SQLINTEGER 缓冲区的地址的 SQL_ATTR_ROW_BIND_OFFSET_PTR 语句属性。 应用程序调用一个函数，使用绑定，如之前**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**，它在此缓冲区中的字节将偏移量，只要数据缓冲区地址和长度/指示器缓冲区地址都不为 0，并且只要绑定的列结果集中。 地址和偏移量的总和必须为有效的地址。 （这意味着，一个或两个偏移量和偏移量添加到的地址可以是无效的其总和为有效的地址。）SQL_ATTR_ROW_BIND_OFFSET_PTR 语句属性是一个指针，以便偏移量的值可以应用于多个集的数据，可以通过更改一个偏移量的值更改所有这些绑定。 应用程序必须确保指针一直有效，直到关闭游标。  
  
> [!NOTE]  
>  绑定的偏移量不受 ODBC 2。*x*驱动程序。  
  
 本部分包含以下主题。  
  
-   [块游标](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [可滚动游标](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [ODBC 游标库](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [多个结果](../../../odbc/reference/develop-app/multiple-results.md)
