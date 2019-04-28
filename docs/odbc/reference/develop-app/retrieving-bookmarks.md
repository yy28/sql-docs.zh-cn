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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9d7d4bd52a5f6e5b03a084cef4402e0a9044f97d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62861397"
---
# <a name="retrieving-bookmarks"></a>检索书签
如果应用程序将使用书签，它必须设置为 SQL_UB_VARIABLE 之前准备或执行该语句的 SQL_ATTR_USE_BOOKMARKS 语句属性。 这是必要的因为它们使用构建和维护的书签可能代价高昂的操作，因此仅当应用程序可以进行良好时，才应启用书签。  
  
 作为结果集的第 0 列返回的书签。 有三种应用程序可以检索它们的方法：  
  
-   绑定结果集的第 0 列。 **SQLFetch**或**SQLFetchScroll**返回列绑定以及其他数据行集中的每个行的书签。  
  
-   调用**SQLSetPos**定位到行集中的行，然后调用**SQLGetData**列 0。 如果驱动程序支持书签，它必须始终支持调用的能力**SQLGetData**列 0，即使它不允许应用程序可以调用**SQLGetData**之前最后一个绑定的其他列列。  
  
-   调用**SQLBulkOperations**与*操作*参数设置为 SQL_ADD 和绑定的列 0。 光标将插入行，并返回绑定的缓冲区中的行的书签。
