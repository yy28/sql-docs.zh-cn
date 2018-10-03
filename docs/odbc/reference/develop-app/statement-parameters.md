---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b366ddd7a665112e6b40b814b13037a517d623a5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47648865"
---
# <a name="statement-parameters"></a>语句参数
一个*参数*是可变的 SQL 语句。 例如，假设一个部件表具有名为 PartID、 描述和价格的列。 若要添加不带参数部件需要构造 SQL 语句，例如：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 尽管此语句将插入新订单，但它不订单输入应用程序的好因为要插入的值不能是硬编码应用程序中。 一种替代方法是构造 SQL 语句在运行时，使用用于插入的值。 这是还不是好的解决由于在运行时构造语句的复杂性。 最佳解决方案是替换的元素**值**子句后的接问号 （？），或*参数标记*:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 参数标记然后被绑定到应用程序变量。 若要添加新行，应用程序只需将变量的值，然后执行该语句。 然后，驱动程序检索变量的当前值并将其发送至数据源。 如果将多次执行语句，该应用程序可以使过程更加高效通过准备此语句。  
  
 刚才所示的语句可能是订单输入应用程序以插入新行中硬编码。 但是，参数标记并不局限于垂直应用程序。 对于任何应用程序，它们易于通过避免文本之间的转换在运行时构造 SQL 语句的难度。 例如，刚才所示的部分 ID 是最有可能存储在应用程序作为一个整数。 如果 SQL 语句构建时没有参数标记，该应用程序必须将部分 ID 转换为文本和数据源必须将其转换为整数。 通过使用参数标记，该应用程序可以一部分 ID 发送给该驱动程序通常可以将其发送到数据源为整数的整数。 这可节省两次转换。 对于长数据值，这一点非常重要，因为此类值的文本形式经常超出允许的 SQL 语句的长度。  
  
 仅在 SQL 语句中特定位置参数才有效。 例如，不允许在 select 列表中 (要返回的列的列表**选择**语句)，也不它们允许为等号 （=），如二元运算符的两个操作数因为不可能的确定参数类型。 通常情况下，参数都是仅在数据操作语言 (DML) 语句，而不在数据定义语言 (DDL) 语句有效。 有关详细信息，请参阅[参数标记](../../../odbc/reference/appendixes/parameter-markers.md)附录 c: SQL 语法中。  
  
 可以使用该 SQL 语句时调用一个名为参数的过程。 命名的参数由其名称，不是由 SQL 语句中的位置标识。 可以将它们绑定通过调用**SQLBindParameter**，但无法由参数标识由 IPD （实现参数描述符） 的 SQL_DESC_NAME 字段*ParameterNumber*的自变量**SQLBindParameter**。 它们还可以绑定通过调用**SQLSetDescField**或**SQLSetDescRec**。 有关命名参数的详细信息，请参阅[按名称 （命名参数） 绑定参数](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)，在本部分中更高版本。 有关描述符的详细信息，请参阅[描述符](../../../odbc/reference/develop-app/descriptors.md)。  
  
 本部分包含以下主题。  
  
-   [绑定参数](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [设置参数值](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [发送 Long 数据](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [SQLGetData 检索输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [过程参数](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [参数值的数组](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
