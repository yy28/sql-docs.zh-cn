---
description: 使用块游标
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 67cad7220641e9c3800e89675825cf2c0b1e334d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482860"
---
# <a name="using-block-cursors"></a>使用块游标
对块游标的支持内置于 ODBC 3。*x*。 当在 ODBC 3 中调用时， **SQLFetch**只能用于多行提取。*x*;如果为 ODBC 2，则为。*x*应用程序调用**SQLFetch**，它将只打开一行只进游标。 ODBC 3 时*x* 应用程序调用 ODBC 2 中的 **SQLFetch** 。*x* 驱动程序，除非驱动程序支持 **SQLExtendedFetch**，否则它将返回一行。 有关详细信息，请参阅附录 G：驱动程序准则中的 [块游标、可滚动游标和后向兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 。  
  
 若要使用块游标，应用程序将设置行集大小，并将行集缓冲区绑定 (如上一节) 所述，可以选择设置 SQL_ATTR_ROWS_FETCHED_PTR 和 SQL_ATTR_ROW_STATUS_PTR 语句特性，并调用 **SQLFetch** 或 **SQLFetchScroll** 来提取行块。 应用程序可以通过调用 **SQLBindCol** 来更改行集大小并绑定新的行集缓冲区 (或指定绑定偏移量) ，甚至在提取行后也是如此。  
  
 本部分包含以下主题。  
  
-   [行集大小](../../../odbc/reference/develop-app/rowset-size.md)  
  
-   [提取的行数和状态](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)  
  
-   [SQLGetData 和块游标;阻止 curso](../../../odbc/reference/develop-app/sqlgetdata-and-block-cursors.md)
