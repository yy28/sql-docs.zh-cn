---
title: 执行批次 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0ce0c043fcfad41a624ad129a757a047d2c87fb6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305728"
---
# <a name="executing-batches"></a>执行批处理
在应用程序执行一批语句之前，应首先检查它们是否受支持。 为此，应用程序使用SQL_BATCH_SUPPORT、SQL_PARAM_ARRAY_ROW_COUNTS和SQL_PARAM_ARRAY_SELECTS选项调用**SQLGetInfo。** 第一个选项返回显式批处理和过程是否支持行计数生成语句和结果集生成语句，而后两个选项返回有关参数化执行中行计数和结果集可用性的信息。  
  
 语句的批处理通过**SQLExecute**或**SQLExecDirect**执行。 例如，以下调用执行一批显式语句以打开新的销售订单。  
  
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
  
 执行一批结果生成语句时，它将返回一个或多个行计数或结果集。 有关如何检索这些结果的信息，请参阅[多个结果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 如果一批语句包含参数标记，则这些语句按与任何其他语句中的参数顺序一样编号。 例如，以下批处理的语句的参数编号为 1 到 21;第一个**INSERT**语句中的编号为 1 到 5，最后**一个 INSERT**语句中的编号为 18 到 21。  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
```  
  
 有关参数的详细信息，请参阅本节后面的[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。
