---
title: 外部联接 |Microsoft 文档
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
- outer join escape sequences [ODBC]
- escape sequences [ODBC], outer join
ms.assetid: be1a0203-5da9-4871-9566-4bd3fbc0895c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 15ab82f5623bad7d3c82729dfd9077ac967301e5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32914352"
---
# <a name="outer-joins"></a>外部联接
ODBC 支持 sql-92 左、 右和完全外部联接语法。 外部联接的转义序列是  
  
 **{oj** *外部-联接 * * *}**  
  
 其中*外部联接*是  
  
 *表引用*{**左&#124;右&#124;完整} 外部联接**{*表引用* &#124; *外部联接*} **ON** *搜索条件*  
  
 *表引用*指定表名，和*搜索条件*指定之间的联接条件*表引用*。  
  
 外部联接请求必须显示之后**FROM**关键字和之前**其中**子句 （如果存在）。 有关完整语法信息，请参阅[外部联接转义序列](../../../odbc/reference/appendixes/outer-join-escape-sequence.md)附录 c: SQL 语法中。  
  
 例如，以下 SQL 语句创建列出所有客户，并显示具有未结订单的相同结果集。 第一个语句中使用转义序列语法。 第二个语句用于 Oracle 的本机语法，并不是可互操作。  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 若要确定数据源和驱动程序支持的外部联接的类型，应用程序调用**SQLGetInfo**带有 SQL_OJ_CAPABILITIES 标志。 可能支持的外部联接的类型左、 右、 完整，或嵌套的外部联接;外部联接中的列名中**ON**子句不具有其各自的表名称中的顺序相同**OUTER JOIN**子句; 结合外部联接; 和外部联接使用内部联接任何 ODBC 比较运算符。 如果 SQL_OJ_CAPABILITIES 信息类型返回 0，则不支持任何外部联接子句。
