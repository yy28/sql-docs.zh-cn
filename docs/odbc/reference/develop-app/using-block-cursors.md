---
title: 使用块游标 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 2aad7d6b-216e-47e7-b3cb-f95ad096f21a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 388995cd5cb8a711d72533685c14088a7e908475
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47758935"
---
# <a name="using-block-cursors"></a>使用块游标
块状游标的支持已内置到 ODBC 3。*x*。 **SQLFetch**可以仅用于在 ODBC 3 中调用时提取多行的操作。*x*; 如果 ODBC 2。*x*应用程序调用**SQLFetch**，它将打开仅的单行、 只进游标。 当 ODBC 3。*x*应用程序调用**SQLFetch** ODBC 2 中。*x*驱动程序，它可以返回单个行，除非该驱动程序支持**SQLExtendedFetch**。 有关详细信息，请参阅[块状游标、 可滚动游标和向后兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)中向后兼容性的附录 g： 驱动程序指南。  
  
 若要使用块状游标，该应用程序将设置行集大小，将绑定的行集缓冲区 （如在上一部分中所述），可以选择集 SQL_ATTR_ROWS_FETCHED_PTR 和 SQL_ATTR_ROW_STATUS_PTR 语句属性和调用**SQLFetch**或**SQLFetchScroll**提取行块。 应用程序可以更改的行集大小并将绑定新行集缓冲区 (通过调用**SQLBindCol**或指定绑定偏移量) 甚至已提取的行之后。  
  
 本部分包含以下主题。  
  
-   [行集大小](../../../odbc/reference/develop-app/rowset-size.md)  
  
-   [提取的行数和状态](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)  
  
-   [SQLGetData 和块游标;块 curso](../../../odbc/reference/develop-app/sqlgetdata-and-block-cursors.md)
