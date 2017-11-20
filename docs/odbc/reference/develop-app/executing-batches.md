---
title: "执行批处理 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- batches [ODBC], executing
- SQL statements [ODBC], batches
ms.assetid: f082c717-4f82-4820-a2fa-ba607d8fd872
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b3235040d910f2dd9b5bdbf4a81765d25dcd8be1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="executing-batches"></a>执行批处理
应用程序执行一批语句之前，应首先检查是否支持它们。 为此，应用程序调用**SQLGetInfo**使用 SQL_BATCH_SUPPORT、 SQL_PARAM_ARRAY_ROW_COUNTS 和 SQL_PARAM_ARRAY_SELECTS 选项。 第一个选项返回行计数 – 生成和生成集 – 语句支持显式批处理和过程，后者的两个选项的可用性返回信息的行计数和结果的设置中时的结果是否 parameterized执行。  
  
 通过执行的语句的批处理**SQLExecute**或**SQLExecDirect**。 例如，以下调用执行语句，以打开一个新的销售订单的显式批次。  
  
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
  
 当结果生成的批处理执行语句，它返回其中一个或多个行计数或结果集。 有关如何检索这些信息，请参阅[多个结果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 如果一批语句包括参数标记，这些编号以升序参数与任何其他语句。 例如，下面的语句的批处理具有编号从 1 到 21; 的参数在第一个那些**插入**语句包括编号 1 到 5 和在最后一个**插入**语句是通过 21 编号的 18。  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
```  
  
 有关参数的详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)，本部分中更高版本。

