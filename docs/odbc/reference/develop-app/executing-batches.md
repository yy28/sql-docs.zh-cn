---
title: 执行批处理 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC], executing
- SQL statements [ODBC], batches
ms.assetid: f082c717-4f82-4820-a2fa-ba607d8fd872
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 84d3cf65284d767d437987c8ff2b21793466106e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67901260"
---
# <a name="executing-batches"></a>执行批处理
在应用程序执行批处理语句之前，首先应检查它们是否受支持。 为此，应用程序将调用带有 SQL_BATCH_SUPPORT、SQL_PARAM_ARRAY_ROW_COUNTS 和 SQL_PARAM_ARRAY_SELECTS 选项的**SQLGetInfo** 。 第一种方法返回显式批处理和过程中是否支持行计数生成和结果集生成语句，而后两个选项返回有关参数化中的行计数和结果集的可用性的信息操作.  
  
 批处理语句通过**SQLExecute**或**SQLExecDirect**执行。 例如，以下调用执行一批显式语句，以打开新的销售订单。  
  
```  
SQLCHAR *BatchStmt =  
   "INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)"  
      "VALUES (2002, 1001, {fn CURDATE()}, 'Garcia', 'OPEN');"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 1, 1234, 10);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 2, 987, 8);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 3, 566, 17);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 4, 412, 500)";  
  
SQLExecDirect(hstmt, BatchStmt, SQL_NTS);  
```  
  
 执行一批结果生成语句时，将返回一个或多个行计数或结果集。 有关如何检索这些结果的信息，请参阅[多个结果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 如果一批语句包含参数标记，则这些语句将按其在任何其他语句中的递增参数顺序进行编号。 例如，下面的一批语句的参数编号为1到 21;第一个 Insert 语句中的第一个**insert**语句的编号为1到5，而最后一个**insert**语句中的编号为18到21。  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
```  
  
 有关参数的详细信息，请参阅本部分后面的[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。
