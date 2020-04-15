---
title: 检索结果（高级） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca02b4ff911c8edff06b38d5341eeaa288cc194c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294637"
---
# <a name="retrieving-results-advanced"></a>检索结果（高级）
应用程序可以指定在调用**SQLBulk 操作****、SQLFetch、SQLFetchScroll**或**SQLSetPos**时，将偏移量添加到绑定的数据**SQLFetchScroll**缓冲区地址和相应的长度/指示器缓冲区地址。 这些添加的结果确定这些操作中使用的地址。  
  
 绑定偏移允许应用程序更改绑定，而无需为以前绑定的列调用**SQLBindCol。** 调用**SQLBindCol**以重新绑定数据会更改缓冲区地址和长度/指示器指针。 另一方面，使用偏移重新绑定只需向现有绑定数据缓冲区地址和长度/指示器缓冲区地址添加偏移。 使用偏移时，绑定是应用程序缓冲区布局方式的"模板"，应用程序可以通过更改偏移量将此"模板"移动到不同的内存区域。 可以随时指定新的偏移量，并且始终添加到最初绑定的值。  
  
 要指定绑定偏移量，应用程序将SQL_ATTR_ROW_BIND_OFFSET_PTR语句属性设置到 SQLINTEGER 缓冲区的地址。 在应用程序调用使用绑定的函数（如**SQLBulk 操作****、SQLFetch、SQLFetchScroll**或**SQLSetPos）** 之前，它会在此缓冲区中的字节中放置偏移量，只要数据缓冲区地址和长度/指示器缓冲区地址都不是 0，只要绑定列位于结果集中。 **SQLFetchScroll** 地址和偏移量的总和必须为有效地址。 （这意味着偏移量和添加到偏移的地址都无效，只要其总和是有效的地址。SQL_ATTR_ROW_BIND_OFFSET_PTR语句属性是一个指针，因此偏移值可以应用于多组绑定数据，所有这些数据都可以通过更改一个偏移值来更改。 应用程序必须确保指针保持有效，直到光标关闭。  
  
> [!NOTE]  
>  ODBC 2 不支持绑定偏移。*x*驱动程序。  
  
 本部分包含以下主题。  
  
-   [块游标](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [可滚动光标](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [ODBC 游标库](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [多个结果](../../../odbc/reference/develop-app/multiple-results.md)
