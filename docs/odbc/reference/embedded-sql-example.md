---
title: "嵌入式 SQL 示例 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- embedded SQL [ODBC]
ms.assetid: b8a26e05-3c82-4c5f-8f01-9de0edb645e9
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ae3b2c60025f82d3153166a887fea12453443450
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="embedded-sql-example"></a>嵌入式的 SQL 的示例
下面的代码是一个简单嵌入的 SQL 程序，用 C 语言编写程序演示很多，但不是全部的嵌入 SQL 技术。 程序提示用户输入订单号、 检索客户编号、 销售人员和订单的状态，并在屏幕上显示检索到的信息。  
  
```  
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
  
 请注意有关此程序：  
  
-   **承载变量**括在部分中声明的主机变量**开始声明部分**和**结尾声明部分**关键字。 每个主机变量名称作为前缀的嵌入式 SQL 语句中出现冒号 （:）。 冒号允许预编译器来区分主机变量和数据库对象，例如表和列，具有相同的名称。  
  
-   **数据类型**DBMS 和主机语言支持的数据类型可以是有很大差异。 这会影响主机变量，因为它们发挥双重作用。 在一方面，主机变量是程序变量，声明和操作由主机语言语句。 另一方面，它们用于嵌入的 SQL 语句中检索数据库数据。 如果不存在主机语言类型对应于 DBMS 数据类型，DBMS 自动将数据转换。 但是，由于每个 DBMS 具有其自己的规则和转换过程与关联的特性，主机变量类型必须慎重选择。  
  
-   **错误处理**DBMS 向应用程序通过 SQL 通信区域，或 SQLCA 报告运行时错误。 在前面的代码示例中，第一个嵌入的 SQL 语句是包括 SQLCA。 这将告知预编译器在程序中包括 SQLCA 结构。 每当程序将处理返回的 DBMS 错误，这是必需的。 WHENEVER...GOTO 语句告知预编译器生成的分支到特定的标签错误发生的错误处理代码。  
  
-   **单独选择**用于返回数据的语句是单独的 SELECT 语句; 也就是说，它返回单个行的数据。 因此，此代码示例不声明或不使用游标。
