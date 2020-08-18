---
description: 语句参数
title: 语句参数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement parameters [ODBC]
ms.assetid: 58d5b166-2578-4699-a560-1f1e6d86c49a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7400367d4b237d2d0e22c6363d1559eb89506d7d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482890"
---
# <a name="statement-parameters"></a>语句参数
*参数*是 SQL 语句中的变量。 例如，假设 Parts 表包含名为 PartID、Description 和 Price 的列。 若要添加没有参数的部件，需要构造如下所示的 SQL 语句：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 尽管此语句插入新订单，但它不是订单输入应用程序的好解决方案，因为在应用程序中要插入的值不能进行硬编码。 一种替代方法是使用要插入的值在运行时构造 SQL 语句。 这也不是一个很好的解决方案，因为在运行时构造语句的复杂性很高。 最佳解决方案是将 **VALUES** 子句的元素替换为问号 (？ ) 或 *参数标记*：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 参数标记然后被绑定到应用程序变量。 若要添加新行，应用程序只需要设置变量的值并执行语句。 然后，驱动程序检索变量的当前值并将其发送至数据源。 如果多次执行该语句，则应用程序可以通过准备语句使该过程更高效。  
  
 刚才显示的语句可能在订单输入应用程序中硬编码为插入新行。 但参数标记并不限于垂直应用程序。 对于任何应用程序，都可以避免在运行时通过与文本之间的转换来构建 SQL 语句。 例如，刚才显示的部分 ID 很可能以整数的形式存储在应用程序中。 如果未使用参数标记构造 SQL 语句，则应用程序必须将部件 ID 转换为文本，并且数据源必须将其转换回整数。 通过使用参数标记，应用程序可以将部分 ID 作为整数发送到驱动程序，这通常可以将其作为整数发送到数据源。 这会保存两个转换。 对于长数据值，这一点非常重要，因为此类值的文本格式经常超出了 SQL 语句允许的长度。  
  
 参数仅在 SQL 语句的某些位置有效。 例如，在选择列表中不允许使用它们 (要由 **select** 语句) 返回的列的列表，也不允许它们作为二元运算符的两个操作数（如等号 (=) ），因为无法确定参数类型。 通常，参数仅在数据操作语言中有效 (DML) 语句，而不是 (DDL) 语句中的数据定义语言。 有关详细信息，请参阅附录 C： SQL 语法中的 [参数标记](../../../odbc/reference/appendixes/parameter-markers.md) 。  
  
 当 SQL 语句调用过程时，可以使用命名参数。 命名参数由其名称标识，而不是按其在 SQL 语句中的位置标识。 可以通过调用**SQLBindParameter**来绑定参数，但参数由 IPD (实现参数描述符) 的 SQL_DESC_NAME 字段标识，而不是由**SQLBindParameter**的*ParameterNumber*参数标识。 还可以通过调用 **SQLSetDescField** 或 **SQLSetDescRec**来绑定它们。 有关命名参数的详细信息，请参阅本部分后面的 [按名称绑定参数 (命名参数) ](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)。 有关描述符的详细信息，请参阅 [描述符](../../../odbc/reference/develop-app/descriptors.md)。  
  
 本部分包含以下主题。  
  
-   [绑定参数](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [设置参数值](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [发送 Long 数据](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [按 SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [过程参数](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [参数值的数组](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
