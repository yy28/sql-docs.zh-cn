---
title: 检索结果（高级） |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020502"
---
# <a name="retrieving-results-advanced"></a>检索结果（高级）
当调用**SQLBulkOperations**、 **SQLFetch**、 **SQLFetchScroll**或**SQLSetPos**时，应用程序可以指定将偏移量添加到绑定的数据缓冲区地址和相应的长度/指示器缓冲区地址。 这些添加的结果决定了这些操作中使用的地址。  
  
 绑定偏移量允许应用程序更改绑定，而无需为之前绑定的列调用**SQLBindCol** 。 对**SQLBindCol**的调用以重新绑定数据将更改缓冲区地址和长度/指示器指针。 另一方面，使用偏移量重新绑定，只需将偏移量添加到现有绑定数据缓冲区地址和长度/指示器缓冲区地址。 使用偏移量时，绑定是应用程序缓冲区布局方式的 "模板"，应用程序可以通过更改偏移量将此 "模板" 移到不同的内存区域。 可随时指定新偏移量，并且始终会将其添加到最初绑定的值。  
  
 为了指定绑定偏移量，应用程序将 SQL_ATTR_ROW_BIND_OFFSET_PTR 语句特性设置为 SQLINTEGER 缓冲区的地址。 在应用程序调用使用绑定的函数（如**SQLBulkOperations**、 **SQLFetch**、 **SQLFetchScroll**或**SQLSetPos**）之前，它将在此缓冲区中的偏移量（以字节为单位），只要数据缓冲区地址和长度/指示器缓冲区地址均为0，只要绑定列在结果集中。 地址与偏移量之和必须是有效地址。 （这意味着，如果其总和为有效地址，则偏移量和添加到的地址可能会无效。）SQL_ATTR_ROW_BIND_OFFSET_PTR 语句特性是一个指针，以便可以将偏移值应用于多个绑定数据集，所有这些数据都可以通过更改一个偏移值进行更改。 在关闭游标之前，应用程序必须确保指针保持有效。  
  
> [!NOTE]  
>  ODBC 2 不支持绑定偏移量。*x*驱动程序。  
  
 本部分包含下列主题。  
  
-   [块游标](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [可滚动游标](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [ODBC 游标库](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [多个结果](../../../odbc/reference/develop-app/multiple-results.md)
