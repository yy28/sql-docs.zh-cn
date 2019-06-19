---
title: SQLSetPos （游标库） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b41fad0f609b16640bfa28ab36f29f364e067b73
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63297417"
---
# <a name="sqlsetpos-cursor-library"></a>SQLSetPos（游标库）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题介绍如何使用**SQLSetPos**游标库中的函数。 有关常规信息**SQLSetPos**，请参阅[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
 游标库支持 SQL_POSITION 操作仅对*操作*中的参数**SQLSetPos**。 它支持 SQL_LOCK_NO_CHANGE 值仅对于*LockType*参数。  
  
 如果该驱动程序不支持大容量操作，该游标库将返回 SQLSTATE HYC00 （驱动程序不支持） 时**SQLSetPos**使用调用*RowNumber*等于 0。 不建议此驱动程序行为。  
  
 游标库不支持对的调用中的 SQL_UPDATE 和 SQL_DELETE operations **SQLSetPos**。 游标库实现定位的 update 或 delete SQL 语句，通过创建搜索更新或删除语句的 WHERE 子句，枚举存储在其缓存中的每个绑定列的值。 有关详细信息，请参阅[处理定位更新和删除语句](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)。  
  
 该驱动程序不支持静态游标，如果使用游标库的应用程序应调用**SQLSetPos**提取的行集上仅**SQLExtendedFetch**或**SQLFetchScroll**，而无法由**SQLFetch**。 游标库实现**SQLExtendedFetch**并**SQLFetchScroll**的重复的调用，从而**SQLFetch** （具有 1 行集大小） 驱动程序中。 游标库传递到调用**SQLFetch**，而在其他另一方面，通过向驱动程序。 如果**SQLSetPos**提取的一个多行的行集合上调用**SQLFetch**时，驱动程序不支持静态游标，该调用将失败，因为**SQLSetPos**不起作用与只进游标。 即使应用程序已成功调用这也会出现**SQLSetStmtAttr**以设置 SQL_ATTR_CURSOR_TYPE 为 SQL_CURSOR_STATIC，即使该驱动程序不支持静态游标，游标库支持。
