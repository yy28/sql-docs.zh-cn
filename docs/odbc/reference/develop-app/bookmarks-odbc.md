---
description: 书签 (ODBC)
title: ODBC)  (书签 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: 1d7cccc5-f847-4321-b240-28570854ee5c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3f162fc317f2651549a1a2e80af03c9942dc64bb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461609"
---
# <a name="bookmarks-odbc"></a>书签 (ODBC)
书签是用于标识数据行的值。 只有驱动程序或数据源才知道书签值的含义。 例如，书签可能与行号一样简单，也可能与磁盘地址一样复杂。 ODBC 中的书签与真实书籍中的书签有点不同。 在真实的书籍中，读者将书签置于特定页面，然后查找该书签以返回到页面。 在 ODBC 中，应用程序为特定行请求书签，存储该书签，并将其传回到游标以返回到该行。 因此，ODBC 中的书签类似于读者记下页码、记录页码，然后再次查找页面。  
  
 若要确定驱动程序是否支持书签，应用程序需要使用 SQL_BOOKMARK_PERSISTENCE 选项调用 **SQLGetInfo** 。 此值中的位描述书签保留的操作，例如，在关闭光标后书签是否仍然有效。  
  
 本部分包含以下主题。  
  
-   [书签类型](../../../odbc/reference/develop-app/bookmark-types.md)  
  
-   [检索书签](../../../odbc/reference/develop-app/retrieving-bookmarks.md)  
  
-   [按书签滚动](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)  
  
-   [按书签更新、删除或提取](../../../odbc/reference/develop-app/updating-deleting-or-fetching-by-bookmark.md)  
  
-   [比较书签](../../../odbc/reference/develop-app/comparing-bookmarks.md)
