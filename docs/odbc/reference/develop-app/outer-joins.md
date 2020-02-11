---
title: 外部联接 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- outer join escape sequences [ODBC]
- escape sequences [ODBC], outer join
ms.assetid: be1a0203-5da9-4871-9566-4bd3fbc0895c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a4bf875b3afd21f6b8cb211c999401b0ecb80879
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67987812"
---
# <a name="outer-joins"></a>外部联接
ODBC 支持 SQL-92 左、右和完全外部联接语法。 外部联接的转义序列是  
  
 **{oj** _外联接_**}**  
  
 其中*外联接*是  
  
 *表引用*{**LEFT &#124; RIGHT &#124; FULL} 外部联接**{*表引用*&#124;*外*联接} **** _搜索条件_  
  
 *表引用*指定表名称，*搜索条件*指定*表引用*之间的联接条件。  
  
 外部联接请求必须出现在**FROM**关键字之后和**WHERE**子句之前（如果存在）。 有关完整的语法信息，请参阅附录 C： SQL 语法中的[外部联接转义序列](../../../odbc/reference/appendixes/outer-join-escape-sequence.md)。  
  
 例如，下面的 SQL 语句创建了一个相同的结果集，该结果集列出了所有客户，并显示了已打开的订单。 第一条语句使用转义序列语法。 第二个语句使用适用于 Oracle 的本机语法，并且不可互操作。  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 若要确定数据源和驱动程序支持的外部联接的类型，应用程序需要使用 SQL_OJ_CAPABILITIES 标志调用**SQLGetInfo** 。 可能支持的外部联接的类型包括：左、右、完全或嵌套外部联接;外部联接，其中**ON**子句中的列名与**外部联接**子句中的表名的顺序不同;与外部联接结合在一起的内部联接;使用任意 ODBC 比较运算符的外部联接。 如果 SQL_OJ_CAPABILITIES 信息类型返回0，则不支持外部联接子句。
