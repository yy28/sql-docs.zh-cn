---
title: SQLBindCol （游标库） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocStmt function [ODBC], Cursor Library
ms.assetid: f4dd546a-0a6c-4397-8ee7-fafa6b9da543
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6cd98b39421e95254fcb052db67cbc9f9205b668
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793537"
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol（游标库）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题介绍如何使用**SQLBindCol**游标库中的函数。 有关常规信息**SQLBindCol**，请参阅[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
 应用程序分配游标库，以返回到当前行中的一个或多个缓冲区。 它将调用**SQLBindCol**将这些缓冲区绑定到结果集的一个或多个时间。  
  
 应用程序可以调用**SQLBindCol**重新绑定结果集列后它被称为**SQLExtendedFetch**， **SQLFetch**，或**SQLFetchScroll**，只要 C 数据类型、 列大小和十进制数字的绑定列保持不变。 应用程序不需要关闭游标重新绑定到不同的地址的列。  
  
 游标库支持设置 SQL_ATTR_ROW_BIND_OFFSET_PTR 语句属性来使用绑定偏移量。 (**SQLBindCol**无需进行此重新绑定为其调用。)如果游标库用于 ODBC *3.x*驱动程序，绑定偏移量不使用时**SQLFetch**调用。 如果使用绑定偏移量**SQLFetch**用于 ODBC 游标库时，将调用*2.x*驱动程序由于**SQLFetch**然后映射到**SQLExtendedFetch**。  
  
 游标库支持调用**SQLBindCol**可将书签列绑定。  
  
 当使用 ODBC *2.x*驱动程序，该游标库返回 SQLSTATE HY090 （字符串或缓冲区长度无效） 时**SQLBindCol**调用以不设置为值的缓冲区长度为书签列等于 4。 当使用 ODBC *3.x*驱动程序，该游标库允许要为任意大小的缓冲区。
