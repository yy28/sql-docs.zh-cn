---
title: SQLSetStmtAttr（光标库） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtAttr function [ODBC], Cursor Library
ms.assetid: 6018a733-c2c8-4047-92ec-92cf85031767
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1bdd9b3b559d5cc78a0d44f5280aae347bc8996a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300487"
---
# <a name="sqlsetstmtattr-cursor-library"></a>SQLSetStmtAttr（游标库）
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 本主题讨论在游标库中使用**SQLSetStmtAttr**函数。 有关**SQLSetStmtAttr**的一般信息，请参阅[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
 游标库支持以下语句属性与**SQLSetStmtAttr**：  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROWSET_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_SIMULATE_CURSOR|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_USE_BOOKMARKS|  
  
 游标库仅支持SQL_ATTR_CURSOR_TYPE语句属性SQL_CURSOR_FORWARD_ONLY和SQL_CURSOR_STATIC值。  
  
 对于仅转发游标，游标库支持SQL_ATTR_CONCURRENCY语句属性SQL_CONCUR_READ_ONLY值。 对于静态游标，游标库支持SQL_ATTR_CONCURRENCY语句属性SQL_CONCUR_READ_ONLY和SQL_CONCUR_VALUES值。  
  
 游标库仅支持SQL_ATTR_SIMULATE_CURSOR语句属性SQL_SC_NON_UNIQUE值。  
  
 尽管 ODBC 规范支持在调用**SQLFetch**或**SQLFetchScroll**后使用SQL_ATTR_PARAM_BIND_TYPE或SQL_ATTR_ROW_BIND_TYPE属性调用**SQLSetStmtAttr，** 但游标库不支持。 在更改游标库中的绑定类型之前，应用程序必须关闭游标。 游标库支持在游标打开时更改SQL_ATTR_ROW_BIND_OFFSET_PTR、SQL_ATTR_PARAM_BIND_OFFSET_PTR、SQL_ATTR_ROWS_FETCHED_PTR和SQL_ATTR_PARAMS_PROCESSED_PTR语句属性。  
  
 应用程序可以使用SQL_ATTR_ROW_ARRAY_SIZE**属性**调用**SQLSetStmtAttr，** 以在游标打开时更改行集大小。 下次调用**SQLFetchScroll 或** **SQLFetch**时，新的行集大小将生效。  
  
 游标库支持设置SQL_ATTR_PARAM_BIND_OFFSET_PTR或SQL_ATTR_ROW_BIND_OFFSET_PTR语句属性以启用绑定偏移。 当游标库与 ODBC 2 一起使用时，绑定偏移量将不用于对**SQLFetch**的调用。*x*驱动程序。  
  
 游标库支持将SQL_ATTR_USE_BOOKMARKS语句属性设置为SQL_UB_VARIABLE。
