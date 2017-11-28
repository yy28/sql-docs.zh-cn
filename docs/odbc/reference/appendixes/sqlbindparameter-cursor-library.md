---
title: "SQLBindParameter （光标库） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLBindParameter function [ODBC], Cursor Library
ms.assetid: 04c53e4c-cd1d-40b2-9997-684ebe43499f
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6011240bb5c69cda4d21005e9cefd20888a9f6d5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter （光标库）
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论使用**SQLBindParameter**光标库中的函数。 有关常规信息**SQLBindParameter**，请参阅[SQLBindParameter 函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)。  
  
 应用程序可以调用**SQLBindParameter**重新绑定参数，只要 C 数据类型、 列大小和十进制数字的绑定的列保持不变。  
  
 游标库支持设置要使用绑定偏移量的 SQL_ATTR_ROW_BIND_OFFSET_PTR 语句属性。 (**SQLBindParameter**不必为进行此重新绑定调用。)  
  
 游标库支持绑定执行中的数据参数。
