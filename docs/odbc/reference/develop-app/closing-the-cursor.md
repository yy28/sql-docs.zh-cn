---
title: 关闭游标 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], closing
- closing cursors [ODBC]
ms.assetid: 4f19bf5e-6d8c-40ae-a975-cfd62a0790ec
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 632a922abb544a379892dfa168f55efd605304c8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63125433"
---
# <a name="closing-the-cursor"></a>关闭游标
当应用程序完成后使用游标时，它将调用**SQLCloseCursor**以关闭游标。 例如：  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 直到应用程序关闭游标，在其打开游标的语句不能用于大多数其他操作，如执行另一个 SQL 语句。 打开游标时可调用的函数的完整列表，请参阅[附录 b:状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
> [!NOTE]  
>  若要关闭游标，应用程序应调用**SQLCloseCursor**，而非**SQLCancel**。  
  
 游标保持打开状态直到被显式关闭，但当提交或回滚事务，在这种情况下某些数据源时关闭游标。 具体而言，结果结束设置，当**SQLFetch**返回 SQL_NO_DATA，则不会关闭游标。 甚至对空结果集 （创建语句成功执行但其不返回任何行时的结果集） 游标，必须显式关闭。
