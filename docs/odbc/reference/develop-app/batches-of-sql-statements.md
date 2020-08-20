---
description: SQL 语句的批处理
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e342fd7eaef721f8fb0033a5ae022ca8de74cda1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465929"
---
# <a name="batches-of-sql-statements"></a>SQL 语句的批处理
一批 SQL 语句是包含两个或更多 SQL 语句的一组或单个 SQL 语句，其效果与包含两个或更多个 SQL 语句的一组相同。 在某些实现中，将执行整个批处理语句，然后再执行任何结果。 这通常比单独提交语句更为有效，因为网络流量常常会降低，并且数据源有时可以优化一批 SQL 语句的执行。 在其他实现中，调用 **SQLMoreResults** 会触发批处理中下一条语句的执行。 ODBC 支持以下类型的批处理：  
  
-   **显式批处理***显式批处理*是以分号分隔的两个或多个 SQL 语句 (; ) 。 例如，下面的一批 SQL 语句将打开一个新的销售订单。 这要求在 Orders 表和 Lines 表中插入行。 请注意，最后一个语句后没有分号。  
  
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
  
-   **过程** 如果过程包含多个 SQL 语句，则将其视为一批 SQL 语句。 例如，以下 SQL Server 特定的语句创建一个返回包含客户信息的结果集的过程，以及一个列出该客户的所有开放式销售订单的结果集：  
  
    ```  
    CREATE PROCEDURE GetCustInfo (@CustomerID INT) AS  
       SELECT * FROM Customers WHERE CustID = @CustomerID  
       SELECT OrderID FROM Orders  
          WHERE CustID = @CustomerID AND Status = 'OPEN'  
    ```  
  
     **CREATE PROCEDURE**语句本身不是一批 SQL 语句。 但它创建的过程是一批 SQL 语句。 因为**CREATE procedure**语句是特定于 SQL Server 的，并且 SQL Server 在**create procedure**语句中不需要使用分号分隔多个语句，所以没有分号分隔这两个**SELECT**语句。  
  
-   **参数数组** 参数数组可用于参数化的 SQL 语句，作为执行大容量操作的一种有效方式。 例如，参数数组可以与以下 **insert** 语句结合使用，以便在行表中插入多行，同时只执行一个 SQL 语句：  
  
    ```  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (?, ?, ?, ?)  
    ```  
  
     如果数据源不支持参数数组，则驱动程序可以通过对每个参数集执行 SQL 语句一次来模拟它们。 有关详细信息，请参阅本部分后面的 [语句参数](../../../odbc/reference/develop-app/statement-parameters.md) 和 [参数值的数组](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)。  
  
 不同类型的批处理不能以可互操作的方式混合。 也就是说，应用程序如何确定执行包含过程调用的显式批处理的结果、使用参数数组的显式批处理，以及使用参数数组的过程调用是否特定于驱动程序。  
  
 本部分包含以下主题。  
  
-   [结果生成和无结果语句](../../../odbc/reference/develop-app/result-generating-and-result-free-statements.md)  
  
-   [执行批处理](../../../odbc/reference/develop-app/executing-batches.md)  
  
-   [错误和批处理](../../../odbc/reference/develop-app/errors-and-batches.md)
