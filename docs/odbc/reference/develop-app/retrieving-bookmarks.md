---
title: "检索书签 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- retrieving bookmarks [ODBC]
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: a34c8f09-b786-4835-a44b-b7294c970aff
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bb71f5ce4b60a133d600367086cdf73c02a61461
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="retrieving-bookmarks"></a>检索书签
如果应用程序将使用书签，必须设置为之前准备或执行该语句的 SQL_UB_VARIABLE SQL_ATTR_USE_BOOKMARKS 语句属性。 这是必要的因为它们使用构建和维护书签可以代价高昂的操作，因此仅当应用程序可以进行良好时，才应启用书签。  
  
 作为结果集的第 0 列返回书签。 有三种应用程序可以检索它们的方法：  
  
-   将列 0 的结果集的绑定。 **SQLFetch**或**SQLFetchScroll**返回书签，对于每个行集中的行以及其他数据绑定列。  
  
-   调用**SQLSetPos**以定位到行集中的行，然后调用**SQLGetData**列 0。 如果驱动程序支持书签，它必须始终支持调用的能力**SQLGetData**列 0，即使它不允许应用程序调用**SQLGetData**之前的最后一个绑定的其他列列。  
  
-   调用**SQLBulkOperations**与*操作*自变量设置为 SQL_ADD，并且绑定列 0。 光标插入行，并返回绑定的缓冲区中的行的书签。
