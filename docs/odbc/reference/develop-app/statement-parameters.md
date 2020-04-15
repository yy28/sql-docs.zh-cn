---
title: 语句参数 |微软文档
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
ms.openlocfilehash: 02327ff4bb6a1ac3ac57fbf7d3c6b09b70c11534
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306818"
---
# <a name="statement-parameters"></a>语句参数
*参数*是 SQL 语句中的变量。 例如，假设"零件"表具有名为"PartID"、"说明"和"价格"的列。 要添加没有参数的零件，需要构造 SQL 语句，例如：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 尽管此语句插入了新订单，但它不是订单输入应用程序的良好解决方案，因为要插入的值在应用程序中不能硬编码。 另一种方法是在运行时使用要插入的值构造 SQL 语句。 由于在运行时构造语句的复杂性，这还不是很好的解决方案。 最佳解决方案是用问号 （？） 或*参数标记*替换**VALUE**子句的元素：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 参数标记然后被绑定到应用程序变量。 要添加新行，应用程序只需设置变量的值并执行语句。 然后，驱动程序检索变量的当前值并将其发送至数据源。 如果语句将执行多次，则应用程序可以通过准备语句使该过程更加高效。  
  
 刚刚显示的语句可能是在订单输入应用程序中硬编码的，用于插入新行。 但是，参数标记并不限于垂直应用。 对于任何应用程序，它们通过避免与文本转换来简化在运行时构造 SQL 语句的难度。 例如，刚才显示的部件 ID 最有可能作为整数存储在应用程序中。 如果 SQL 语句构造时没有参数标记，则应用程序必须将部件 ID 转换为文本，数据源必须将其转换回整数。 通过使用参数标记，应用程序可以将部件 ID 作为整数发送到驱动程序，该整数通常可以将其作为整数发送到数据源。 这样可以节省两次转换。 对于长数据值，这一点非常重要，因为此类值的文本形式经常超过 SQL 语句的允许长度。  
  
 参数仅在 SQL 语句中的某些位置有效。 例如，它们不允许在选择列表中（**由 SELECT**语句返回的列列表），也不允许它们作为二进制运算符（如等号 （*）的两个操作数，因为无法确定参数类型。 通常，参数仅在数据操作语言 （DML） 语句中有效，而在数据定义语言 （DDL） 语句中无效。 有关详细信息，请参阅附录 C 中的[参数标记](../../../odbc/reference/appendixes/parameter-markers.md)：SQL 语法。  
  
 当 SQL 语句调用过程时，可以使用命名参数。 命名参数由名称标识，而不是由它们在 SQL 语句中的位置标识。 它们可以由对**SQLBind参数**的调用绑定，但参数由 IPD 的SQL_DESC_NAME字段（实现参数描述符）标识，而不是由**SQLBind参数**的*参数编号*参数标识。 它们也可以通过调用**SQLSetDescField**或**SQLSetDescRec**来绑定。 有关命名参数的详细信息，请参阅本节后面的["按名称（命名参数）绑定参数](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)"。 有关描述符的详细信息，请参阅[描述符](../../../odbc/reference/develop-app/descriptors.md)。  
  
 本部分包含以下主题。  
  
-   [绑定参数](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [设置参数值](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [发送 Long 数据](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [按 SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [过程参数](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [参数值的数组](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
