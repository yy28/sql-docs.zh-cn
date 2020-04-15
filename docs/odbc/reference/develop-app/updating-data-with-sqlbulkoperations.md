---
title: 使用 SQLBulk 操作更新数据 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9b96e3a43b8385910e4260cf51dea7e4ff508200
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298481"
---
# <a name="updating-data-with-sqlbulkoperations"></a>使用 SQLBulkOperations 更新数据
应用程序可以在数据源的基础表上执行批量更新、删除、提取或插入操作，并调用**SQLBulk 操作**。 调用**SQLBulk 操作**是构造和执行 SQL 语句的便捷替代方法。 它允许 ODBC 驱动程序支持定位更新，即使数据源不支持定位 SQL 语句也是如此。 它是通过函数调用实现完整数据库访问模式的一部分。  
  
 **SQLBulk操作**在当前行集中运行，只能在调用**SQLFetch**或**SQLFetchScroll**后使用。 应用程序通过缓存其书签指定要更新、删除或刷新的行。 驱动程序从行集缓冲区检索要更新的行的新数据，或将新数据插入到基础表中。  
  
 **SQLBulk操作**要使用的行集大小由调用**SQLSetStmtAttr**设置，*属性*参数为 SQL_ATTR_ROW_ARRAY_SIZE。 SQLSetPos （ 仅在调用**SQLFetch**或**SQLFetchScroll**后使用新的行集大小 ） 不同， **SQLBulk 操作**在调用**SQLSetStmtAttr**后使用新的行集大小 。 **SQLSetPos**  
  
 由于与关系数据库的大多数交互都是通过 SQL 完成的，因此**SQLBulk 操作**不受广泛支持。 但是，驱动程序可以通过构造和执行**更新**、**删除**或**INSERT**语句来轻松模拟它。  
  
 要确定**SQLBulk操作**支持的操作，应用程序使用SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1或SQL_STATIC_CURSOR_ATTRIBUTES1信息选项（取决于游标的类型）调用**SQLGetInfo。**  
  
 本部分包含以下主题。  
  
-   [使用 SQLBulkOperations 按书签更新行](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [使用 SQLBulkOperations 按书签删除行](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [使用 SQLBulkOperations 插入行](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [使用 SQLBulkOperations 提取行](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)
