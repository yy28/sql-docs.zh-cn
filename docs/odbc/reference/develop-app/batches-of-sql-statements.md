---
title: 批量 SQL 语句 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC]
- SQL statements [ODBC], batches
- batches [ODBC], about batches
ms.assetid: 766488cc-450c-434c-9c88-467f6c57e17c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d68ea1c13655ca7c57ba076823f461a4b2e22055
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283507"
---
# <a name="batches-of-sql-statements"></a>SQL 语句的批处理
一批 SQL 语句是两个或多个 SQL 语句的组或单个 SQL 语句，其效果与两个或多个 SQL 语句组的效果相同。 在某些实现中，在任何结果可用之前执行整个批处理语句。 这通常比单独提交语句更有效，因为网络流量通常可以减少，数据源有时可以优化一批 SQL 语句的执行。 在其他实现中，调用**SQLMore结果**会触发批处理中下一个语句的执行。 ODBC 支持以下类型的批次：  
  
-   **显式批处理***显式批处理*是两个或多个 SQL 语句，由分号分隔（;)。 例如，以下批处理的 SQL 语句将打开新的销售订单。 这需要将行插入到"订单"和"行"表中。 请注意，最后一个语句之后没有分号。  
  
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
  
-   **程序**如果过程包含多个 SQL 语句，则它被视为一批 SQL 语句。 例如，以下特定于 SQL Server 的语句创建一个过程，返回一个包含有关客户的信息的结果集和列出该客户所有已结销售订单的结果集：  
  
    ```  
    CREATE PROCEDURE GetCustInfo (@CustomerID INT) AS  
       SELECT * FROM Customers WHERE CustID = @CustomerID  
       SELECT OrderID FROM Orders  
          WHERE CustID = @CustomerID AND Status = 'OPEN'  
    ```  
  
     **CREATE 程序**语句本身不是一批 SQL 语句。 但是，它创建的过程是一批 SQL 语句。 没有分号分隔两个**SELECT**语句，因为**CREATE 程序**语句特定于 SQL Server，并且 SQL Server 不需要分号来分隔**CREATE 程序**语句中的多个语句。  
  
-   **参数数组**参数数组可与参数化 SQL 语句一起使用，作为执行批量操作的有效方法。 例如，参数数组可以与以下**INSERT**语句一起使用，以便将多行插入到 Lines 表中，同时仅执行单个 SQL 语句：  
  
    ```  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (?, ?, ?, ?)  
    ```  
  
     如果数据源不支持参数数组，驱动程序可以通过为每个参数集执行 SQL 语句一次来模拟它们。 有关详细信息，请参阅参数[值的](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)和数组，请参阅本节后面的语句参数和数组。  
  
 不同类型的批处理不能以可互操作的方式混合。 也就是说，应用程序如何确定执行包含过程调用的显式批处理、使用参数数组的显式批处理以及使用参数数组的过程调用的结果是特定于驱动程序的。  
  
 本部分包含以下主题。  
  
-   [结果生成和无结果语句](../../../odbc/reference/develop-app/result-generating-and-result-free-statements.md)  
  
-   [执行批处理](../../../odbc/reference/develop-app/executing-batches.md)  
  
-   [错误和批处理](../../../odbc/reference/develop-app/errors-and-batches.md)
