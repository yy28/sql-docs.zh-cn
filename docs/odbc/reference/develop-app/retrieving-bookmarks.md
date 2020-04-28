---
title: 检索书签 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving bookmarks [ODBC]
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: a34c8f09-b786-4835-a44b-b7294c970aff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d146b2fb9bfc0e7294709e971f1b6752dc99ab3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300067"
---
# <a name="retrieving-bookmarks"></a>检索书签
如果应用程序将使用书签，则在准备或执行该语句前，它必须将 SQL_ATTR_USE_BOOKMARKS 语句特性设置为 SQL_UB_VARIABLE。 这是必需的，因为生成和维护书签是一种昂贵的操作，因此，只有当应用程序可以充分利用书签时，才应启用书签。  
  
 书签将作为结果集的第0列返回。 应用程序可以使用三种方法来检索它们：  
  
-   绑定结果集的列0。 **SQLFetch**或**SQLFetchScroll**将返回行集中每一行的书签以及其他绑定列的数据。  
  
-   调用**SQLSetPos**以定位到行集中的行，然后对列0调用**SQLGetData** 。 如果驱动程序支持书签，则它必须始终支持对列0调用**SQLGetData**的能力，即使它不允许应用程序在最后一个绑定列之前为其他列调用**SQLGetData** 。  
  
-   调用**SQLBulkOperations** ，并将*操作*参数设置为 SQL_ADD 和列0绑定。 光标插入行并返回绑定缓冲区中的行的书签。
