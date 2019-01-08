---
title: SQL 语句的批处理 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 09805ab73af76bc55890222fc1ffd0e1857d0f33
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52531237"
---
# <a name="batches-of-sql-statements"></a>SQL 语句的批处理
一批 SQL 语句是一组两个或多个 SQL 语句或单个 SQL 语句具有相同的效果的一组两个或多个 SQL 语句。 在某些实现中，整个批处理语句之前，执行任何结果都可用。 这主要是通常比单个提交语句，因为通常可以减少网络流量和数据源有时可以优化执行一批 SQL 语句有效。 在其他实现中，调用**SQLMoreResults**触发批处理中的下一个语句执行。 ODBC 支持以下类型的批处理：  
  
-   **显式批处理***显式批处理*是以分号 （;） 分隔的两个或多个 SQL 语句。 例如，以下批处理 SQL 语句会打开一个新销售订单。 这要求将行插入到订单和行的表。 请注意最后一个语句后没有分号。  
  
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
  
-   **过程**如果过程包含多个 SQL 语句，它被视为可一批 SQL 语句。 例如，以下特定于 SQL Server 的语句将创建返回的结果集包含有关客户和结果集列出所有打开该客户销售订单信息的过程：  
  
    ```  
    CREATE PROCEDURE GetCustInfo (@CustomerID INT) AS  
       SELECT * FROM Customers WHERE CustID = @CustomerID  
       SELECT OrderID FROM Orders  
          WHERE CustID = @CustomerID AND Status = 'OPEN'  
    ```  
  
     **CREATE PROCEDURE**语句本身不是一批 SQL 语句。 但是，它会创建该过程是一批 SQL 语句。 没有使用分号分隔两个**选择**语句由于**CREATE PROCEDURE**语句是特定于 SQL Server 和 SQL Server 不需要分号来分隔中的多个语句**CREATE PROCEDURE**语句。  
  
-   **参数的数组**参数的数组可以用于参数化 SQL 语句，可以有效地执行批量操作。 例如，可以使用以下使用参数的数组**插入**语句以执行仅单个 SQL 语句时将多个行插入到行表：  
  
    ```  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (?, ?, ?, ?)  
    ```  
  
     如果数据源不支持参数的数组，该驱动程序可以模拟它们通过执行每组参数一次的 SQL 语句。 有关详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)并[参数值数组](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)稍后在本部分中。  
  
 不能以可互操作的方式混合不同类型的批处理。 即，应用程序如何确定执行显式批包含过程的结果调用使用的参数数组的显式批次，并使用参数的数组的过程调用是特定于驱动程序的。  
  
 本部分包含以下主题。  
  
-   [结果生成和无结果语句](../../../odbc/reference/develop-app/result-generating-and-result-free-statements.md)  
  
-   [执行批处理](../../../odbc/reference/develop-app/executing-batches.md)  
  
-   [错误和批处理](../../../odbc/reference/develop-app/errors-and-batches.md)
