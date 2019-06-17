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
manager: craigg
ms.openlocfilehash: 827dd531eda338f4fd297a4420ed144d46a613ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62998936"
---
# <a name="outer-joins"></a>外部联接
ODBC 支持 SQL-92 左、 右和完全外部联接语法。 外部联接转义序列  
  
 **{oj** _outer-join_ **}**  
  
 其中*外部联接*是  
  
 *表引用*{**LEFT&#124;右&#124;完整} 外部联接**{*表引用* &#124; *外部联接*} **ON** _搜索条件_  
  
 *表引用*指定表名，并*搜索条件*指定之间的联接条件*表引用*。  
  
 外部联接请求必须出现的后面**FROM**关键字和之前**其中**子句 （如果存在）。 有关完整语法的信息，请参阅[外部联接转义序列](../../../odbc/reference/appendixes/outer-join-escape-sequence.md)附录 c： 驱动器中SQL 语法。  
  
 例如，以下 SQL 语句创建列出所有客户，并显示具有未结订单的相同结果集。 第一个语句使用转义序列语法。 第二个语句使用用于 Oracle 的本机语法并不是可互操作。  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 若要确定数据源和驱动程序支持的外部联接的类型，应用程序调用**SQLGetInfo** SQL_OJ_CAPABILITIES 标志。 类型的可能支持的外部联接左、 右、 完全处理或嵌套外部联接;外部联接中的列名称中的这**ON**子句不具有在其相应的表名称的顺序相同**OUTER JOIN**子句; 与外部联接; 和使用的外部联接结合使用的内部联接任何 ODBC 比较运算符。 如果 SQL_OJ_CAPABILITIES 信息类型返回 0，则支持没有外部联接子句。
