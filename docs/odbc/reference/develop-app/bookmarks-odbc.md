---
title: 书签 （ODBC） |微软文档
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
ms.openlocfilehash: e8273c82b918024417e613ea44a2d26bafaf7d76
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306318"
---
# <a name="bookmarks-odbc"></a>书签 (ODBC)
书签是用于标识数据行的值。 只有驱动程序或数据源才知道书签值的含义。 例如，书签可能与行号一样简单，也可能与磁盘地址一样复杂。 ODBC 中的书签与真实书籍中的书签略有不同。 在真实书籍中，读者将书签放在特定页面，然后查找该书签以返回到该页。 在 ODBC 中，应用程序为特定行请求书签，存储该书签，并将其传回到游标以返回到该行。 因此，ODBC 中的书签类似于读者写下页码、记住它，然后再次查找页面。  
  
 要确定驱动程序对书签的支持，应用程序使用SQL_BOOKMARK_PERSISTENCE选项调用**SQLGetInfo。** 此值中的位描述书签存活的操作，例如书签在关闭光标后是否仍然有效。  
  
 本部分包含以下主题。  
  
-   [书签类型](../../../odbc/reference/develop-app/bookmark-types.md)  
  
-   [检索书签](../../../odbc/reference/develop-app/retrieving-bookmarks.md)  
  
-   [按书签滚动](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)  
  
-   [按书签更新、删除或提取](../../../odbc/reference/develop-app/updating-deleting-or-fetching-by-bookmark.md)  
  
-   [比较书签](../../../odbc/reference/develop-app/comparing-bookmarks.md)
