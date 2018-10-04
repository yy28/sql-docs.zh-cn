---
title: 使用 SQLBulkOperations 更新数据 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBulkOperations function [ODBC], updating data
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: 7645a704-341e-4267-adbe-061a9fda225b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 958514adc02452cdc75a05e7ad28cd31f4e8e0e6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47723405"
---
# <a name="updating-data-with-sqlbulkoperations"></a>使用 SQLBulkOperations 更新数据
应用程序可以执行时数据源通过调用基础表上的大容量更新、 删除、 提取时或插入操作**SQLBulkOperations**。 调用**SQLBulkOperations**是一个便捷替代方式构造和执行 SQL 语句。 它使 ODBC 驱动程序支持定位的更新，即使数据源不支持定位的 SQL 语句。 它是通过函数调用实现完整的数据库访问模式的一部分。  
  
 **SQLBulkOperations**对当前行集进行操作并在调用后才可以在**SQLFetch**或**SQLFetchScroll**。 应用程序指定要更新、 删除或刷新通过缓存其书签的行。 该驱动程序检索新数据的行要更新或插入到基础表中，从行集缓冲区的新数据。  
  
 行集大小，以供**SQLBulkOperations**通过调用设置**SQLSetStmtAttr**与*特性*SQL_ATTR_ROW_ARRAY_SIZE 参数。 与不同**SQLSetPos**，它仅在调用后使用新的行集大小**SQLFetch**或**SQLFetchScroll**， **SQLBulkOperations**使用在调用的新行集大小**SQLSetStmtAttr**。  
  
 与关系数据库的大部分交互通过 SQL，因为**SQLBulkOperations**并未得到广泛支持。 但是，驱动程序可以轻松地模拟它的构造和执行**更新**，**删除**，或**插入**语句。  
  
 若要确定哪些操作**SQLBulkOperation**支持，应用程序调用**SQLGetInfo**使用 SQL_DYNAMIC_CURSOR_ATTRIBUTES1、 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、 SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 信息选项 （具体取决于游标的类型）。  
  
 本部分包含以下主题。  
  
-   [使用 SQLBulkOperations 按书签更新行](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [使用 SQLBulkOperations 按书签删除行](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [使用 SQLBulkOperations 插入行](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [使用 SQLBulkOperations 提取行](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)
