---
title: SQLSetPos （光标库） |Microsoft 文档
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
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], Cursor Library
ms.assetid: 574399c3-2bb2-4d19-829c-7c77bd82858d
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ed803dd1663dc663e6badf324edf77d710a8912f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetpos-cursor-library"></a>SQLSetPos （光标库）
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论使用**SQLSetPos**光标库中的函数。 有关常规信息**SQLSetPos**，请参阅[SQLSetPos 函数](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
 游标库支持 SQL_POSITION 操作仅对*操作*中的参数**SQLSetPos**。 它支持的 SQL_LOCK_NO_CHANGE 值仅*LockType*自变量。  
  
 游标库如果驱动程序不支持大容量操作，返回 SQLSTATE HYC00 （驱动程序不可用） 时**SQLSetPos**使用调用*RowNumber*等于 0。 不建议此驱动程序行为。  
  
 游标库不支持对的调用中的 SQL_UPDATE 和 SQL_DELETE 操作**SQLSetPos**。 游标库实现定位的更新或删除 SQL 语句，通过创建搜索更新或删除语句的 WHERE 子句，枚举存储在其缓存为每个绑定的列的值。 有关详细信息，请参阅[处理定位更新和删除语句](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md)。  
  
 如果该驱动程序不支持静态游标，应调用应用程序使用的是光标库**SQLSetPos**通过提取行集上仅**SQLExtendedFetch**或**SQLFetchScroll**，而无法由**SQLFetch**。 游标库实现**SQLExtendedFetch**和**SQLFetchScroll**通过进行的重复的调用来**SQLFetch** （使用 1 的行集大小） 驱动程序中。 游标库将传递到调用**SQLFetch**，而在其他另一方面，通过与驱动程序。 如果**SQLSetPos**通过提取多行的行集上调用**SQLFetch**当驱动程序不支持静态游标，调用将失败，因为**SQLSetPos**不起作用与只进游标。 即使应用程序已成功调用这也会出现**SQLSetStmtAttr**将 SQL_ATTR_CURSOR_TYPE 设置为 SQL_CURSOR_STATIC，即使该驱动程序不支持静态游标，游标库支持。
