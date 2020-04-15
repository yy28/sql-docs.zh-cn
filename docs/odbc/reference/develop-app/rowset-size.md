---
title: 行集大小 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rowset size [ODBC]
- cursors [ODBC], block
- result sets [ODBC], rowset size
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 60366ae8-175c-456a-ae5e-bdd860786911
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 11b95768934f96e1587b3c570b2510f3c2849239
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304238"
---
# <a name="rowset-size"></a>行集大小
要使用的行集大小取决于应用程序。 基于屏幕的应用程序通常遵循两种策略之一。 第一种是将排组大小设置为屏幕上显示的行数;第二种是将行集大小设置为屏幕上显示的行数。如果用户调整屏幕大小，应用程序将相应地更改行集大小。 第二种是将排组大小设置为较大的数字，如 100，从而减少对数据源的调用数。 应用程序尽可能在行集中内本地滚动，并且仅在在行集外滚动时提取新行。  
  
 其他应用程序（如报表）倾向于将行集大小设置为应用程序可以合理处理的最大行数 - 如果行集越大，每行的网络开销有时会降低。 行集的确切大小取决于每行的大小和可用的内存量。  
  
 行集大小由对**SQLSetStmtAttr**的调用设置，*属性*参数为SQL_ATTR_ROW_ARRAY_SIZE。 应用程序可以更改行集大小、绑定新的行集缓冲区（通过调用**SQLBindCol**或指定绑定偏移），即使在已提取行后，也可以同时同时获取两者。 更改行集大小的含义取决于函数：  
  
-   **SQLFetch**和**SQLFetchScroll**在调用时使用行集大小来确定要提取的行数。 但是，具有SQL_FETCH_NEXT*提取方向*的**SQLFetchScroll**会根据上一个提取的行集增加游标，然后根据当前行集大小获取行集。  
  
-   **SQLSetPos**使用上述对**SQLFetch**或**SQLFetchScroll**调用时有效的行集大小，因为**SQLSetPos**对已设置的行集进行了操作。 如果在更改行集大小后调用**了 SQLBulk 操作****，SQLSetPos**也将拾取新的行集大小。  
  
-   **SQLBulk操作**在调用时使用有效的行集大小，因为它对表执行操作，而独立于任何提取的行集。
