---
title: "使用 SQLBulkOperations 更新数据 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLBulkOperations function [ODBC], updating data
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: 7645a704-341e-4267-adbe-061a9fda225b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 75e5f954065c0b41935aa231c85c093d5ee10226
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="updating-data-with-sqlbulkoperations"></a>使用 SQLBulkOperations 更新数据
应用程序可以执行大容量更新、 删除、 提取或插入操作上具有对的调用的数据源中的基础表**SQLBulkOperations**。 调用**SQLBulkOperations**是一个便捷替代方式构造和执行 SQL 语句。 它可让 ODBC 驱动程序支持定位的更新，即使数据源不支持定位的 SQL 语句。 它是范例的通过函数调用实现完整的数据库访问的一部分。  
  
 **SQLBulkOperations**当前行集上运行并在调用后才可以使用**SQLFetch**或**SQLFetchScroll**。 应用程序指定要更新、 删除或刷新缓存其书签的行。 该驱动程序检索新行的数据进行更新或要插入到基础表中，从行集缓冲区的新数据。  
  
 要使用的行集大小**SQLBulkOperations**通过调用设置**SQLSetStmtAttr**与*属性*SQL_ATTR_ROW_ARRAY_SIZE 自变量。 与不同**SQLSetPos**，它仅在调用后使用新的行集大小**SQLFetch**或**SQLFetchScroll**， **SQLBulkOperations**使用在调用后的新行集大小**SQLSetStmtAttr**。  
  
 因为大多数与关系数据库的交互通过 SQL， **SQLBulkOperations**不受广泛支持。 但是，驱动程序可以轻松地模拟它方法是构造并执行**更新**，**删除**，或**插入**语句。  
  
 若要确定哪些操作**SQLBulkOperation**支持的功能，应用程序调用**SQLGetInfo**使用 SQL_DYNAMIC_CURSOR_ATTRIBUTES1、 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、 SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 信息选项 （具体取决于游标的类型）。  
  
 本部分包含以下主题。  
  
-   [使用 SQLBulkOperations 更新书签的行](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [删除通过具有 SQLBulkOperations 书签的行](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [与 SQLBulkOperations 插入行](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [获取具有 SQLBulkOperations 行](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)
