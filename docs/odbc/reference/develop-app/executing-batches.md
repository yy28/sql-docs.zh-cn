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
manager: craigg
ms.openlocfilehash: 46b224e8167587c4e4860f171b132d23539143e8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47695026"
---
# <a name="executing-batches"></a>执行批处理
应用程序执行一批语句之前，应首先检查是否支持它们。 为此，应用程序调用**SQLGetInfo** SQL_BATCH_SUPPORT、 SQL_PARAM_ARRAY_ROW_COUNTS 和 SQL_PARAM_ARRAY_SELECTS 选项。 第一个选项返回是否行计数 – 生成和结果集 – 生成语句中显式批处理和过程，行计数和结果的返回信息可用性设置中的后一种两个选项时支持参数化执行。  
  
 通过执行语句的批处理**SQLExecute**或**SQLExecDirect**。 例如，以下调用执行语句，以打开新的销售订单的显式批次。  
  
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
  
 结果生成的批处理时执行语句，它将返回一个或多个行计数或结果设置。 有关如何检索这些属性的信息，请参阅[多个结果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 如果一批语句包括参数标记，这些编号递增参数顺序，因为它们位于任何其他语句。 例如，以下批处理语句具有参数编号从 1 到 21;第一个中的那些**插入**语句是编号 1 到 5 和最后一个中的那些**插入**语句是通过 21 编号的 18。  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
```  
  
 有关参数的详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)，在本部分中更高版本。
