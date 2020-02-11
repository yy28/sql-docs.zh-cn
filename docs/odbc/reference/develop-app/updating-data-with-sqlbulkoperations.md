---
title: 用 SQLBulkOperations 更新数据 |Microsoft Docs
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
ms.openlocfilehash: 4d1aa9b3300cba78f34e876a8501dbaaa421390a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68091666"
---
# <a name="updating-data-with-sqlbulkoperations"></a>使用 SQLBulkOperations 更新数据
应用程序可以通过调用**SQLBulkOperations**在数据源的基础表上执行大容量更新、删除、提取或插入操作。 调用**SQLBulkOperations**是构造和执行 SQL 语句的一种简便方法。 即使数据源不支持定位 SQL 语句，它也允许 ODBC 驱动程序支持定位更新。 这是通过函数调用实现数据库完全访问权限的一种模式。  
  
 **SQLBulkOperations**对当前行集进行操作，并且只能在调用**SQLFetch**或**SQLFetchScroll**后使用。 应用程序通过缓存书签来指定要更新、删除或刷新的行。 驱动程序将从行集缓冲区中检索要更新的行的新数据或要插入基础表中的新数据。  
  
 **SQLBulkOperations**所使用的行集大小是通过调用**SQLSetStmtAttr** SQL_ATTR_ROW_ARRAY_SIZE 的*属性*参数设置的。 不同于**SQLSetPos**，它仅在调用**SQLFetch**或**SQLFetchScroll**后使用新的行集大小， **SQLBulkOperations**在调用**SQLSetStmtAttr**后使用新的行集大小。  
  
 由于与关系数据库的大多数交互是通过 SQL 来完成的，因此**SQLBulkOperations**不受广泛支持。 但是，驱动程序可以通过构造并执行**UPDATE**、 **DELETE**或**INSERT**语句来轻松地对其进行模拟。  
  
 若要确定**SQLBulkOperation**支持的操作，应用程序需要使用 SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 信息选项（具体取决于游标的类型）调用**SQLGetInfo** 。  
  
 本部分包含下列主题。  
  
-   [使用 SQLBulkOperations 按书签更新行](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [使用 SQLBulkOperations 按书签删除行](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [使用 SQLBulkOperations 插入行](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [使用 SQLBulkOperations 提取行](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)
