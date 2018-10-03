---
title: SQLSetStmtAttr （游标库） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7d4e5bd6ec27891e80933dfcc42beec9056d2d3a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47619785"
---
# <a name="sqlsetstmtattr-cursor-library"></a>SQLSetStmtAttr（游标库）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题介绍如何使用**SQLSetStmtAttr**游标库中的函数。 有关常规信息**SQLSetStmtAttr**，请参阅[SQLSetStmtAttr 函数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
 游标库支持使用以下语句属性**SQLSetStmtAttr**:  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROWSET_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_SIMULATE_CURSOR|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_USE_BOOKMARKS|  
  
 游标库仅支持 SQL_CURSOR_FORWARD_ONLY 和 SQL_CURSOR_STATIC 值的 SQL_ATTR_CURSOR_TYPE 语句属性。  
  
 对于只进游标，游标库支持语句属性 SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY 的值。 对于静态游标，游标库支持 SQL_CONCUR_READ_ONLY 和 SQL_CONCUR_VALUES sql_attr_concurrency 设置语句属性的值。  
  
 游标库支持仅 SQL_SC_NON_UNIQUE 的 SQL_ATTR_SIMULATE_CURSOR 语句属性的值。  
  
 虽然在 ODBC 规范中支持对的调用，但是**SQLSetStmtAttr**后 SQL_ATTR_PARAM_BIND_TYPE 或 SQL_ATTR_ROW_BIND_TYPE 属性**SQLFetch**或**SQLFetchScroll**已调用，该游标库没有。 它可以更改该游标库中的绑定类型之前，应用程序必须关闭游标。 游标库支持更改 SQL_ATTR_ROW_BIND_OFFSET_PTR、 SQL_ATTR_PARAM_BIND_OFFSET_PTR、 SQL_ATTR_ROWS_FETCHED_PTR，并且 SQL_ATTR_PARAMS_PROCESSED_PTR 语句属性的游标处于打开状态。  
  
 应用程序可以调用**SQLSetStmtAttr**与**属性**的 SQL_ATTR_ROW_ARRAY_SIZE 游标处于打开状态时更改的行集大小。 新的行集大小将会生效下次**SQLFetchScroll**或**SQLFetch**调用。  
  
 游标库支持设置 SQL_ATTR_PARAM_BIND_OFFSET_PTR 或 SQL_ATTR_ROW_BIND_OFFSET_PTR 语句属性，以启用绑定的偏移量。 绑定偏移量不会用于调用**SQLFetch** ODBC 2 使用游标库时。*x*驱动程序。  
  
 游标库支持 SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_VARIABLE。
