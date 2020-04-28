---
title: Embedded SQL 示例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- embedded SQL [ODBC]
ms.assetid: b8a26e05-3c82-4c5f-8f01-9de0edb645e9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 39ec504c423817c6a3e11bc954555b201b8b09c6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81294168"
---
# <a name="embedded-sql-example"></a>嵌入式 SQL 示例
下面的代码是一个以 C 编写的简单的嵌入式 SQL 程序。该程序阐释了许多（但并非全部）的嵌入式 SQL 技术。 该程序将提示用户输入订单号、检索客户编号、销售人员和订单状态，并在屏幕上显示检索到的信息。  
  
```cpp  
int main() {  
   EXEC SQL INCLUDE SQLCA;  
   EXEC SQL BEGIN DECLARE SECTION;  
      int OrderID;         /* Employee ID (from user)         */  
      int CustID;            /* Retrieved customer ID         */  
      char SalesPerson[10]   /* Retrieved salesperson name      */  
      char Status[6]         /* Retrieved order status        */  
   EXEC SQL END DECLARE SECTION;  
  
   /* Set up error processing */  
   EXEC SQL WHENEVER SQLERROR GOTO query_error;  
   EXEC SQL WHENEVER NOT FOUND GOTO bad_number;  
  
   /* Prompt the user for order number */  
   printf ("Enter order number: ");  
   scanf_s("%d", &OrderID);  
  
   /* Execute the SQL query */  
   EXEC SQL SELECT CustID, SalesPerson, Status  
      FROM Orders  
      WHERE OrderID = :OrderID  
      INTO :CustID, :SalesPerson, :Status;  
  
   /* Display the results */  
   printf ("Customer number:  %d\n", CustID);  
   printf ("Salesperson: %s\n", SalesPerson);  
   printf ("Status: %s\n", Status);  
   exit();  
  
query_error:  
   printf ("SQL error: %ld\n", sqlca->sqlcode);  
   exit();  
  
bad_number:  
   printf ("Invalid order number.\n");  
   exit();  
}  
```  
  
 请注意有关此计划的以下内容：  
  
-   **主机变量**主机变量是在由**BEGIN DECLARE 节**和**END declare 节**关键字括起来的部分中声明的。 每个主机变量名称以冒号（:)在嵌入的 SQL 语句中出现。 冒号允许预编译器区分具有相同名称的主机变量和数据库对象（例如表和列）。  
  
-   **数据类型**DBMS 和主机语言支持的数据类型可能会有很大不同。 这会影响主机变量，因为它们扮演了双重角色。 一方面，主机变量是由主机语言语句声明和操作的程序变量。 另一方面，它们用于嵌入的 SQL 语句中以检索数据库数据。 如果没有与 DBMS 数据类型对应的主机语言类型，DBMS 会自动转换数据。 但是，因为每个 DBMS 都有其自己的与转换过程关联的规则和特性，所以必须仔细选择主机变量类型。  
  
-   **错误处理**DBMS 通过 SQL 通信区域或 SQLCA 向应用程序程序报告运行时错误。 在上面的代码示例中，第一个嵌入式 SQL 语句包含 SQLCA。 这会告知预编译器在程序中包含 SQLCA 结构。 只要程序处理 DBMS 返回的错误，就需要这样做。 每次 .。。GOTO 语句告诉预编译器生成错误处理代码，该代码在发生错误时分支到特定标签。  
  
-   **单一实例选择**用于返回数据的语句是单独的 SELECT 语句;也就是说，它只返回一行数据。 因此，该代码示例不声明或使用游标。
