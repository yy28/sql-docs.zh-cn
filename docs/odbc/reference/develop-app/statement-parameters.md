---
title: "语句参数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- statement parameters [ODBC]
ms.assetid: 58d5b166-2578-4699-a560-1f1e6d86c49a
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5e56b61d47581f98f37560875de920c45029c2e9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="statement-parameters"></a>语句参数
A*参数*是中的 SQL 语句的变量。 例如，假设部件表具有名为 PartID、 描述和价格的列。 若要添加不带参数部件需要构造 SQL 语句，例如：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 尽管此语句中插入新订单，但它不一个顺序输入应用程序很好的解决方案因为要插入的值不能为硬编码在应用程序。 一种替代方法是构造 SQL 语句在运行时，使用值要插入。 这是还不很好的解决方案，因为在运行时构造语句的复杂性。 最佳解决方案是要替换的元素**值**带有问号 （？） 的子句或*参数标记*:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 参数标记然后被绑定到应用程序变量。 若要添加新行，该应用程序只是为了设置这些变量的值，然后执行该语句。 然后，驱动程序检索变量的当前值并将其发送至数据源。 如果将多次执行语句，应用程序可以使过程更加高效通过准备该语句。  
  
 只需所示的语句可能硬编码中的顺序输入应用程序，以插入新行。 但是，参数标记并不局限于垂直应用程序。 对于任何应用程序，它们易于通过避免之间的文本转换在运行时构造 SQL 语句的难度。 例如，只需显示的一部分 ID 很可能是存储在一个整数形式的应用程序。 如果没有参数标记来构造 SQL 语句时，应用程序必须将一部分 ID 转换为文本和数据源必须将其转换回整数。 通过使用参数标记，应用程序可以一部分 ID 发送给该驱动程序为一个整数，通常可以将其发送到数据源为整数。 这将保存两个转换。 对于长整型数据值，这一点非常重要，因为此类值的文本形式经常超过允许的长度的 SQL 语句。  
  
 参数仅中的 SQL 语句中的某些地方才有效。 例如，它们不允许在选择列表 (要返回的列列表**选择**语句)，它们允许作为等号 （=），如二元运算符的两个操作数因为不可能的也不确定参数类型。 通常情况下，参数都有效仅在数据操作语言 (DML) 语句，并且不在数据定义语言 (DDL) 语句。 有关详细信息，请参阅[参数标记](../../../odbc/reference/appendixes/parameter-markers.md)附录 c: SQL 语法中。  
  
 可以使用该 SQL 语句时调用名为参数的过程。 命名的参数由其名称，不按其位置的 SQL 语句中标识。 它们可以通过调用绑定**SQLBindParameter**，但参数不是由 IPD （实现参数描述符） SQL_DESC_NAME 字段*ParameterNumber*自变量**SQLBindParameter**。 它们还可以绑定通过调用**SQLSetDescField**或**SQLSetDescRec**。 有关命名参数的详细信息，请参阅[按名称 （名为参数） 的绑定参数](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)，本部分中更高版本。 有关描述符的详细信息，请参阅[描述符](../../../odbc/reference/develop-app/descriptors.md)。  
  
 本部分包含以下主题。  
  
-   [绑定参数](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [设置参数值](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [发送的长整型数据](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [检索由 SQLGetData 的输出参数](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [过程参数](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [参数值的数组](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
