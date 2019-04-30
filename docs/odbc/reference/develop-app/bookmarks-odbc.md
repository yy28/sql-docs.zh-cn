---
title: 书签 (ODBC) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9eecd202a17a0a08e8607ebec0caaa31b7b3ca9c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199209"
---
# <a name="bookmarks-odbc"></a>书签 (ODBC)
书签是用于标识数据行的值。 只有驱动程序或数据源才知道书签值的含义。 例如，书签可能与行号一样简单，也可能与磁盘地址一样复杂。 在 ODBC 中的书签是有点不同于实际丛书中的书签。 在实际的书中，读取器放置于特定页面的书签，并将查找该书签以返回到页。 在 ODBC 中，应用程序为特定行请求书签，存储该书签，并将其传回到游标以返回到该行。 因此，在 ODBC 中的书签是类似于一个读取器写下页码，记住，，然后再次查看的页面。  
  
 若要确定驱动程序的支持的书签，应用程序调用**SQLGetInfo** SQL_BOOKMARK_PERSISTENCE 选项。 此值中的位描述了什么操作书签会幸存，例如书签是否仍有效之后关闭游标。  
  
 本部分包含以下主题。  
  
-   [书签类型](../../../odbc/reference/develop-app/bookmark-types.md)  
  
-   [检索书签](../../../odbc/reference/develop-app/retrieving-bookmarks.md)  
  
-   [按书签滚动](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)  
  
-   [按书签更新、删除或提取](../../../odbc/reference/develop-app/updating-deleting-or-fetching-by-bookmark.md)  
  
-   [比较书签](../../../odbc/reference/develop-app/comparing-bookmarks.md)
