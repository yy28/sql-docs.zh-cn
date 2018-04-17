---
title: SQLSetStmtAttr （光标库） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLSetStmtAttr function [ODBC], Cursor Library
ms.assetid: 6018a733-c2c8-4047-92ec-92cf85031767
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8dd285982ff1483a38673a6e06ecb3293e503782
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sqlsetstmtattr-cursor-library"></a>SQLSetStmtAttr （光标库）
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论使用**SQLSetStmtAttr**光标库中的函数。 有关常规信息**SQLSetStmtAttr**，请参阅[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
 游标库支持使用以下语句属性**SQLSetStmtAttr**:  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROWSET_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_SIMULATE_CURSOR|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_USE_BOOKMARKS|  
  
 游标库支持仅 SQL_CURSOR_FORWARD_ONLY 和 SQL_CURSOR_STATIC 属性的值 SQL_ATTR_CURSOR_TYPE 语句。  
  
 对于只进游标，游标库支持 SQL_ATTR_CONCURRENCY 语句属性的 SQL_CONCUR_READ_ONLY 值。 为静态游标，游标库支持 SQL_ATTR_CONCURRENCY 语句属性的 SQL_CONCUR_READ_ONLY 和 SQL_CONCUR_VALUES 值。  
  
 游标库支持仅 SQL_ATTR_SIMULATE_CURSOR 语句属性的 SQL_SC_NON_UNIQUE 值。  
  
 尽管 ODBC 规范支持对调用**SQLSetStmtAttr**具有 SQL_ATTR_PARAM_BIND_TYPE 或 SQL_ATTR_ROW_BIND_TYPE 属性后**SQLFetch**或**SQLFetchScroll**已调用，光标库没有。 它可以更改的是光标库中的绑定类型之前，应用程序必须关闭游标。 游标库支持更改 SQL_ATTR_ROW_BIND_OFFSET_PTR SQL_ATTR_PARAM_BIND_OFFSET_PTR、 SQL_ATTR_ROWS_FETCHED_PTR，且 SQL_ATTR_PARAMS_PROCESSED_PTR 语句特性时游标处于打开状态。  
  
 应用程序可以调用**SQLSetStmtAttr**与**属性**的 SQL_ATTR_ROW_ARRAY_SIZE 游标处于打开状态时更改的行集大小。 新的行集大小将会生效的下一步时间**SQLFetchScroll**或**SQLFetch**调用。  
  
 游标库支持设置的 SQL_ATTR_PARAM_BIND_OFFSET_PTR 或 SQL_ATTR_ROW_BIND_OFFSET_PTR 语句特性，以启用绑定偏移量。 绑定偏移量将不用于调用**SQLFetch** ODBC 2 使用的是光标库时。*x*驱动程序。  
  
 游标库支持 SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_VARIABLE。
