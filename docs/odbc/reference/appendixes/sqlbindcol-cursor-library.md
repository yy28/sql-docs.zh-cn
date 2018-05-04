---
title: SQLBindCol （光标库） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocStmt function [ODBC], Cursor Library
ms.assetid: f4dd546a-0a6c-4397-8ee7-fafa6b9da543
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0d18bcb0c437dacb3d9584b50c30179a36a000b3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol （光标库）
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论使用**SQLBindCol**光标库中的函数。 有关常规信息**SQLBindCol**，请参阅[SQLBindCol 函数](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
 应用程序分配的是光标库返回在当前行集的一个或多个缓冲区。 它调用**SQLBindCol**将这些缓冲区绑定到结果集的一个或多个时间。  
  
 应用程序可以调用**SQLBindCol**重新绑定结果集列后该维度被称为**SQLExtendedFetch**， **SQLFetch**，或**SQLFetchScroll**，只要 C 数据类型、 列大小和十进制数字的绑定的列保持不变。 应用程序不需要关闭游标重新绑定到不同的地址的列。  
  
 游标库支持设置要使用绑定偏移量的 SQL_ATTR_ROW_BIND_OFFSET_PTR 语句属性。 (**SQLBindCol**不必为进行此重新绑定调用。)游标库用于 ODBC 3 *.x*驱动程序，该绑定偏移量是不使用时**SQLFetch**调用。 如果使用绑定偏移量**SQLFetch**与 ODBC 2 一起使用的是光标库时调用。*x*驱动程序因为**SQLFetch**然后映射到**SQLExtendedFetch**。  
  
 游标库支持调用**SQLBindCol**可将书签列绑定。  
  
 当使用 ODBC 2。*x*驱动程序，光标库返回 SQLSTATE HY090 （无效字符串或缓冲区长度） 时**SQLBindCol**调用将书签列的缓冲区长度设置为值不等于 4。 使用 ODBC 3 时 *.x*驱动程序，光标库允许要是任意大小的缓冲区。
