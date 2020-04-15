---
title: 外部联接 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 81988d34dca38d5c041ff9f87e9674d7c97d76cc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282439"
---
# <a name="outer-joins"></a>外部联接
ODBC 支持 SQL-92 左、右和完整的外部联接语法。 外部联接的转义序列是  
  
 **[oj** _外部联接_**]**  
  
 *外部联接*是  
  
 *表引用*[**左&#124; 右&#124;完整] 外部联接**[*表引用*&#124;*外部联接*=_在搜索条件_**上**  
  
 *表引用*指定表名称，*搜索条件*指定*表引用 之间的*联接条件。  
  
 外部联接请求必须出现在**FROM**关键字之后和**WHERE**子句之前（如果存在）。 有关完整的语法信息，请参阅附录 C 中的[外部联接转义序列](../../../odbc/reference/appendixes/outer-join-escape-sequence.md)：SQL 语法。  
  
 例如，以下 SQL 语句创建相同的结果集，该结果集列出所有客户并显示已打开的订单。 第一个语句使用转义序列语法。 第二个语句使用 Oracle 的本机语法，不可互操作。  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 要确定数据源和驱动程序支持的外部联接类型，应用程序使用 SQL_OJ_CAPABILITIES 标志调用**SQLGetInfo。** 可能支持的外部联接类型为左联接、右联接、完整联接或嵌套外部联接;**ON**子句中的列名称与**OUTER JOIN**子句中的相应表名的顺序不相同的外部联接;内部联接与外部联接结合;和外部联接使用任何 ODBC 比较运算符。 如果SQL_OJ_CAPABILITIES信息类型返回 0，则不支持外部联接子句。
