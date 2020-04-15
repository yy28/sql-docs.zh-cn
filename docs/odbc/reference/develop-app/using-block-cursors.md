---
title: 使用块光标 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f5c487bd8b60a83c709399cb9673dc0b015bd79d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306788"
---
# <a name="using-block-cursors"></a>使用块游标
对块游标的支持内置于 ODBC 3 中。*x*. . **SQLFetch**只能在 ODBC 3 中调用时用于多行提取。*x;* 如果 ODBC 2.*x*应用程序调用**SQLFetch，** 它将只打开一个单行、仅转发的游标。 当一个ODBC 3。*x*应用程序在 ODBC 2 中调用**SQLFetch。***x*驱动程序，它返回一行，除非驱动程序支持**SQLExtendedFetch**。 有关详细信息，请参阅附录 G 中的[块光标、可滚动光标和向后兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)：向后兼容性的驱动程序指南。  
  
 要使用块游标，应用程序设置行集大小，绑定行集缓冲区（如上一节所述），可以选择设置SQL_ATTR_ROWS_FETCHED_PTR和SQL_ATTR_ROW_STATUS_PTR语句属性，并调用**SQLFetch**或**SQLFetchScroll**来获取行块。 应用程序可以更改行集大小并绑定新的行集缓冲区（通过调用**SQLBindCol**或指定绑定偏移），即使在获取行之后也是如此。  
  
 本部分包含以下主题。  
  
-   [行集大小](../../../odbc/reference/develop-app/rowset-size.md)  
  
-   [提取的行数和状态](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)  
  
-   [SQLGet数据和块光标;块库尔索](../../../odbc/reference/develop-app/sqlgetdata-and-block-cursors.md)
