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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 723e40e6d83eed84ed93ee1eeab3535622ad5f04
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299137"
---
# <a name="closing-the-cursor"></a>关闭游标
当应用程序完成使用游标时，它将调用**SQLCloseCursor**以关闭游标。 例如：  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 在应用程序关闭游标之前，打开游标的语句不能用于大多数其他操作，如执行其他 SQL 语句。 有关在游标打开时可以调用的函数的完整列表，请参阅[附录 B： ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
> [!NOTE]  
>  若要关闭游标，应用程序应调用**SQLCloseCursor**，而不是**SQLCancel**。  
  
 游标将保持打开状态，直到它们被显式关闭，除非提交或回滚事务，在这种情况下，某些数据源会关闭游标。 特别是，如果**SQLFetch**返回 SQL_NO_DATA，则不会关闭游标。 还必须显式关闭空结果集上的游标（当语句成功执行但未返回任何行时创建的结果集）。
