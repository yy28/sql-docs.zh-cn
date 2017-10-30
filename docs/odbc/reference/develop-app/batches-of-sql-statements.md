---
title: "SQL 语句的批处理 |Microsoft 文档"
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
- batches [ODBC]
- SQL statements [ODBC], batches
- batches [ODBC], about batches
ms.assetid: 766488cc-450c-434c-9c88-467f6c57e17c
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 70649ee51ec7b5c2ef3926706f802da8189fc3b2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="batches-of-sql-statements"></a>SQL 语句的批处理
SQL 语句的批处理是一组两个或多个 SQL 语句或具有相同的效果的一组两个或多个 SQL 语句的单个 SQL 语句。 在某些实现中，可使用任何结果之前执行整个批处理语句。 这通常会更高效比单独，提交语句，因为通常可以减少网络流量和数据源有时可以优化的一批 SQL 语句的执行。 在其他实现中，调用**SQLMoreResults**触发的批次中的下一个语句执行。 ODBC 支持以下类型的批处理：  
  
-   **显式批处理***显式批处理*是用分号 （;） 分隔的两个或多个 SQL 语句。 例如，下面的 SQL 语句的批处理会打开新的销售订单。 这需要将行插入到订单和行的表。 请注意最后一个语句后没有任何分号。  
  
    ```  
    INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
       VALUES (2002, 1001, {fn CURDATE()}, 'Garcia', 'OPEN');  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 1, 1234, 10);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 2, 987, 8);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 3, 566, 17);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 4, 412, 500)  
    ```  
  
-   **过程**如果一个过程包含多个 SQL 语句，它被视为可一批 SQL 语句。 例如，下面的 SQL Server 特定语句将创建返回的结果集包含有关客户和结果集列出为该客户的所有未结销售订单信息的过程：  
  
    ```  
    CREATE PROCEDURE GetCustInfo (@CustomerID INT) AS  
       SELECT * FROM Customers WHERE CustID = @CustomerID  
       SELECT OrderID FROM Orders  
          WHERE CustID = @CustomerID AND Status = 'OPEN'  
    ```  
  
     **CREATE PROCEDURE**语句本身不是一批 SQL 语句。 但是，它将创建的过程是一批的 SQL 语句。 不使用分号分隔两个**选择**语句因为**CREATE PROCEDURE**语句是特定于 SQL Server 和 SQL Server 不需要用分号分隔多个语句中**CREATE PROCEDURE**语句。  
  
-   **参数数组**可与参数化 SQL 语句，可以有效地执行大容量操作使用的参数数组。 例如，可以替换为以下使用的参数数组**插入**语句以执行只有单个 SQL 语句时将多个行插入到行表：  
  
    ```  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (?, ?, ?, ?)  
    ```  
  
     如果数据源不支持的参数数组，该驱动程序可以通过执行一次为每个参数集的 SQL 语句来模拟它们。 有关详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)和[参数值的数组](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)，本部分中更高版本。  
  
 不同类型的批处理不能混合在互操作的方式。 即，应用程序如何确定执行显式的批处理包含过程的结果调用时，使用的参数，数组的显式批处理和使用的参数数组的过程调用是特定于驱动程序的。  
  
 本部分包含以下主题。  
  
-   [结果生成和无结果的语句](../../../odbc/reference/develop-app/result-generating-and-result-free-statements.md)  
  
-   [执行批处理](../../../odbc/reference/develop-app/executing-batches.md)  
  
-   [错误和批处理](../../../odbc/reference/develop-app/errors-and-batches.md)

