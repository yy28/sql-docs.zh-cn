---
title: 行集大小 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fda38811fa876c9a0fad55e7f2ee7566ad3026d2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67943761"
---
# <a name="rowset-size"></a>行集大小
若要使用的行集大小取决于应用程序。 基于屏幕的应用程序通常遵循以下两个策略之一。 第一种是将行集大小设置为在屏幕上显示的行数如果在用户调整屏幕，该应用程序做相应更改的行集大小。 第二个是行集大小设置为一个更大数字，如 100，从而减少了对数据源的调用数。 应用程序内的行集时可能本地滚动，并仅当外部行集将滚动时提取新行。  
  
 其他应用程序，如报表，往往会将行集大小设置为最大数量的行可以合理地处理应用程序-具有更大的行集，有时会减少网络开销每行。 完全大行集可以是取决于每个行和可用内存量的大小。  
  
 通过调用设置行集大小**SQLSetStmtAttr**与*属性*SQL_ATTR_ROW_ARRAY_SIZE 参数。 该应用程序可以更改的行集大小，将绑定新行集缓冲区 (通过调用**SQLBindCol**或指定绑定偏移量) 甚至已提取的行后，或两者。 更改的行集大小的影响取决于该函数：  
  
-   **SQLFetch**并**SQLFetchScroll**在调用时使用的行集大小，以确定要提取的行数。 但是， **SQLFetchScroll**与*FetchOrientation* SQL_FETCH_NEXT 递增，增量为基于游标的上一个提取，然后提取行集上基于当前的行集大小的行集。  
  
-   **SQLSetPos**使用从前面的调用开始实际上是行集大小**SQLFetch**或**SQLFetchScroll**，这是因为**SQLSetPos**对行集已设置的。 **SQLSetPos**还会选取新的行集大小如果**SQLBulkOperations**行集大小已发生更改后调用。  
  
-   **SQLBulkOperations**行集大小实际上在时使用的调用，因为它执行独立于任何提取的行集的表操作。
