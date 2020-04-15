---
title: SQLBindCol（光标库） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1c29909a96f147a0f5ebc2140a68072dfe544255
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305468"
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol（游标库）
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 本主题讨论在游标库中使用**SQLBindCol**函数。 有关**SQLBindCol**的一般信息，请参阅[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
 应用程序为游标库分配一个或多个缓冲区以返回当前行集。 它调用**SQLBindCol**一次或多次将这些缓冲区绑定到结果集。  
  
 应用程序可以调用**SQLBindCol**在调用**SQL 扩展获取****、SQLFetch**或**SQLFetchScroll**后重新绑定结果集列，只要绑定列的 C 数据类型、列大小和十进制数字保持不变。 应用程序不需要关闭光标，将列重新绑定到不同的地址。  
  
 游标库支持将SQL_ATTR_ROW_BIND_OFFSET_PTR语句属性设置为使用绑定偏移量。 **（SQLBindCol**不必调用此重新绑定。如果游标库与 ODBC *3.x*驱动程序一起使用，则在调用**SQLFetch**时不使用绑定偏移量。 如果当游标库与 ODBC *2.x*驱动程序一起使用时调用**SQLFetch，** 则使用绑定偏移，因为**SQLFetch**随后被映射到**SQLExtendedFetch**。  
  
 游标库支持调用**SQLBindCol**来绑定书签列。  
  
 使用 ODBC *2.x*驱动程序时，当调用**SQLBindCol**将书签列的缓冲区长度设置为不等于 4 的值时，光标库将返回 SQLSTATE HY090（无效字符串或缓冲区长度）。 使用 ODBC *3.x*驱动程序时，光标库允许缓冲区具有任何大小。
