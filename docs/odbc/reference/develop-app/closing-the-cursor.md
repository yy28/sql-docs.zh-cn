---
title: 关闭光标 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 723e40e6d83eed84ed93ee1eeab3535622ad5f04
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299137"
---
# <a name="closing-the-cursor"></a>关闭游标
当应用程序使用游标完成时，它将调用**SQLCloseCursor**来关闭游标。 例如：  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 在应用程序关闭游标之前，打开游标的语句不能用于大多数其他操作，例如执行另一个 SQL 语句。 有关打开游标时可以调用的函数的完整列表，请参阅[附录 B：ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
> [!NOTE]  
>  要关闭游标，应用程序应调用**SQLCloseCursor**，而不是**SQLCancel**。  
  
 游标保持打开状态，直到显式关闭，除非提交或回滚事务，在这种情况下，某些数据源将关闭游标。 特别是，当**SQLFetch**返回SQL_NO_DATA时，到达结果集的末尾不会关闭游标。 即使空结果集上的游标（在语句成功执行但未返回任何行时创建的结果集）也必须显式关闭。
