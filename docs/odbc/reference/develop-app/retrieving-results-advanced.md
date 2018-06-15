---
title: 检索结果 （高级） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- offsets [ODBC]
- result sets [ODBC], about result sets
- bind offsets [ODBC]
ms.assetid: bc00c379-71a7-407a-975c-898243f39bb6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9d3b5bb68849991e0fe7c2af3b538140008a85e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32912192"
---
# <a name="retrieving-results-advanced"></a>检索结果 （高级）
应用程序可以指定添加偏移量，以绑定数据缓冲区的地址和相应的长度/指示器缓冲区地址时**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**调用。 这些添加的结果确定这些操作中使用的地址。  
  
 绑定偏移量允许应用程序更改而不调用绑定**SQLBindCol**对于以前绑定列。 调用**SQLBindCol**重新绑定数据更改的缓冲区地址和长度/指示器指针。 重新绑定相对的偏移量，另一方面，只需将偏移量添加到现有的绑定的数据缓冲区地址和长度/指示器缓冲区地址。 偏移量使用时，提供的绑定是如何布局应用程序缓冲区的"模板"和应用程序可以通过将移动此"模板"到不同区域的内存更改偏移量。 新的偏移量可以在任何时指定，并且始终会将其添加到最初绑定值。  
  
 若要指定绑定偏移量，应用程序 SQL_ATTR_ROW_BIND_OFFSET_PTR 语句将该属性设置 SQLINTEGER 缓冲区的地址。 应用程序调用一个函数，使用绑定，如之前**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**，它需要将偏移量放置在此缓冲区中的字节，只要数据缓冲区地址和长度/指示器缓冲区地址都不为 0，并且只要绑定的列在结果集中。 地址和偏移量之和必须是有效的地址。 （这意味着，一个或两个偏移量和偏移量添加到的地址可以是无效的只要其总和是有效的地址。）SQL_ATTR_ROW_BIND_OFFSET_PTR 语句属性是一个指针，以便偏移量的值可以应用于多个集的绑定的数据，它们都可以通过更改一个偏移量的值更改。 应用程序必须确保光标关闭之前，指针保持有效。  
  
> [!NOTE]  
>  绑定偏移量不受 ODBC 2。*x*驱动程序。  
  
 本部分包含以下主题。  
  
-   [块游标](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [可滚动游标](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [ODBC 游标库](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [多个结果](../../../odbc/reference/develop-app/multiple-results.md)
