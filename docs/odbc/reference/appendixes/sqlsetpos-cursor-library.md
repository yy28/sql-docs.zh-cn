---
title: SQLSetPos（光标库） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], Cursor Library
ms.assetid: 574399c3-2bb2-4d19-829c-7c77bd82858d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4c46ef88075a5adbd96138d7d1f03c26712f7ea1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300507"
---
# <a name="sqlsetpos-cursor-library"></a>SQLSetPos（游标库）
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 本主题讨论在游标库中使用**SQLSetPos**函数。 有关**SQLSetPos**的一般信息，请参阅[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
 游标库仅支持**SQLSetPos**中的*操作*参数的操作SQL_POSITION操作。 它仅支持*LockType*参数的SQL_LOCK_NO_CHANGE值。  
  
 如果驱动程序不支持批量操作，则当调用**SQLSetPos**时，*使用行号*等于 0 时，游标库将返回 SQLSTATE HYC00（驱动程序无法启用）。 不建议使用此驱动程序行为。  
  
 游标库不支持对**SQLSetPos**的调用中SQL_UPDATE和SQL_DELETE操作。 游标库通过创建搜索的更新或删除语句实现定位更新或删除 SQL 语句，该语句具有 WHERE 子句，该语句枚举存储在其缓存中为每个绑定列的值。 有关详细信息，请参阅[处理定位更新和删除语句](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)。  
  
 如果驱动程序不支持静态游标，则使用游标库的应用程序应仅在**SQLExtendedFetch**或**SQLFetchScroll**获取的行集上调用**SQLSetPos，** 而不是**SQLFetch**调用 。 游标库通过在驱动程序中重复调用**SQLFetch（** 行集大小为 1）实现**SQL 扩展获取**和**SQLFetchScroll。** 另一方面，游标库将调用传递到**驱动程序**。 如果在驱动程序不支持静态游标时**SQLFetch**获取的多行行集上调用**SQLSetPos，** 则调用将失败，因为**SQLSetPos**不适用于仅转发游标。 即使应用程序已成功调用**SQLSetStmtAttr**将SQL_ATTR_CURSOR_TYPE设置为SQL_CURSOR_STATIC，即使驱动程序不支持静态游标，也会发生这种情况。
