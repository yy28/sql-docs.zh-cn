---
title: "使用块状游标 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 2aad7d6b-216e-47e7-b3cb-f95ad096f21a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 51f02b5b243286a650897fecdcac5d8778bd3f40
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="using-block-cursors"></a>使用块状游标
内置 ODBC 3，还可以为块游标的支持。*x*。 **SQLFetch**可以仅用于多行提取 ODBC 3 中调用时。*x*; 如果要将一个 ODBC 2。*x*应用程序调用**SQLFetch**，它将打开仅的单行更行、 只进游标。 当一个 ODBC 3。*x*应用程序调用**SQLFetch** ODBC 2 中。*x*驱动程序，它可以返回单个行，除非的驱动程序支持**SQLExtendedFetch**。 有关详细信息，请参阅[块状游标可滚动游标，向后兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)为了向后兼容的附录 g： 驱动程序准则中。  
  
 若要使用块状游标，该应用程序将设置行集大小，将绑定行集的缓冲区 （如在上一节中所述）、 （可选） 设置 SQL_ATTR_ROWS_FETCHED_PTR 和 SQL_ATTR_ROW_STATUS_PTR 语句属性，以及调用**SQLFetch**或**SQLFetchScroll**提取块，这些行。 应用程序可以更改的行集大小并将新行集缓冲区绑定 (通过调用**SQLBindCol**或指定绑定的偏移量) 甚至已提取行后。  
  
 本部分包含以下主题。  
  
-   [行集大小](../../../odbc/reference/develop-app/rowset-size.md)  
  
-   [提取的行数和状态](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)  
  
-   [SQLGetData 和块状游标;块 curso](../../../odbc/reference/develop-app/sqlgetdata-and-block-cursors.md)

