---
title: 关闭游标 |Microsoft 文档
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
- cursors [ODBC], closing
- closing cursors [ODBC]
ms.assetid: 4f19bf5e-6d8c-40ae-a975-cfd62a0790ec
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 794180396f9b233d32283f46264a696c80559d21
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32907712"
---
# <a name="closing-the-cursor"></a>关闭游标
当应用程序已完成使用游标时，它将调用**SQLCloseCursor**要关闭游标。 例如：  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 直到应用程序将关闭光标，在其打开游标的语句不能针对大多数其他操作，如执行另一个 SQL 语句。 可以在打开游标时调用的函数的完整列表，请参阅[附录 b: ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
> [!NOTE]  
>  若要关闭游标，应用程序应调用**SQLCloseCursor**，而不**SQLCancel**。  
  
 游标保持打开状态直到被显式关闭，但当提交或回滚事务，在这种情况下某些数据源时关闭游标。 具体而言，结果结束设置，当**SQLFetch**返回 SQL_NO_DATA，不会关闭游标。 必须显式关闭甚至游标空结果集 （语句成功执行但其没有返回任何行时创建的结果集）。
