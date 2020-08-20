---
description: 行集大小
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d915d6e11fc7678312eab60c3316815cfabab38e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465605"
---
# <a name="rowset-size"></a>行集大小
要使用的行集大小取决于应用程序。 基于屏幕的应用程序通常遵循以下两个策略之一。 第一种是将行集大小设置为屏幕上显示的行数;如果用户调整屏幕的大小，应用程序会相应地更改行集的大小。 第二种方式是将行集大小设置为更大的数字，如100，这会减少对数据源的调用次数。 如果可能，应用程序将在行集内本地滚动，并仅在滚动行集外滚动新行时才提取新行。  
  
 其他应用程序（如报表）倾向于将行集大小设置为应用程序可合理处理的最大行数-对于更大的行集，每行的网络开销有时会降低。 行集的确切大小取决于每行的大小和可用的内存量。  
  
 行集大小通过使用 SQL_ATTR_ROW_ARRAY_SIZE 的*属性*参数对**SQLSetStmtAttr**的调用设置。 应用程序可以更改行集大小、绑定新的行集缓冲区 (通过调用 **SQLBindCol** 或指定绑定偏移量来) ，甚至在提取行后，或同时指定这两者。 更改行集大小的影响取决于函数：  
  
-   **SQLFetch** 和 **SQLFetchScroll** 在调用时使用行集大小来确定要提取的行数。 但是， **SQLFetchScroll** 和 *FetchOrientation* 的 SQL_FETCH_NEXT 会根据上一次提取的行集来递增游标，然后基于当前行集大小获取行集。  
  
-   **SQLSetPos** 使用在前面调用 **SQLFetch** 或 **SQLFetchScroll**时生效的行集大小，因为 **SQLSetPos** 对已设置的行集进行操作。 如果在更改行集大小后调用了**SQLBulkOperations** ， **SQLSetPos**也将选取新的行集大小。  
  
-   **SQLBulkOperations** 在调用时使用有效的行集大小，因为它对独立于任何提取的行集的表执行操作。
