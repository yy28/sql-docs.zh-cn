---
title: 嵌入式 SQL 示例 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294168"
---
# <a name="embedded-sql-example"></a>嵌入式 SQL 示例
以下代码是一个简单的嵌入式 SQL 程序，用 C 编写。该程序演示了许多（但不是全部）嵌入式 SQL 技术。 程序提示用户输入订单号，检索客户编号、销售人员和订单状态，并在屏幕上显示检索到的信息。  
  
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
  
 请注意有关此程序的以下内容：  
  
-   **主机变量**主机变量在由**BEGIN DECLARE C 和****结束声明节**关键字随附的部分中声明。 每个主机变量名称都由冒号（:)当它出现在嵌入的 SQL 语句中时。 冒号允许预编译器区分具有相同名称的主机变量和数据库对象（如表和列）。  
  
-   **数据类型**DBMS 和宿主语言支持的数据类型可能大不相同。 这会影响主机变量，因为它们具有双重作用。 一方面，主机变量是程序变量，由宿主语言语句声明和操作。 另一方面，它们用于嵌入式 SQL 语句来检索数据库数据。 如果没有与 DBMS 数据类型对应的主机语言类型，DBMS 将自动转换数据。 但是，由于每个 DBMS 都有自己的规则和与转换过程关联的特性，因此必须仔细选择主机变量类型。  
  
-   **错误处理**DBMS 通过 SQL 通信区域或 SQLCA 向应用程序报告运行时错误。 在前面的代码示例中，第一个嵌入的 SQL 语句是 INCLUDE SQLCA。 这告诉预编译器在程序中包括 SQLCA 结构。 每当程序处理 DBMS 返回的错误时，都需要这样做。 随时...GOTO 语句告诉预编译器生成错误处理代码，当发生错误时，该代码分支到特定标签。  
  
-   **单顿选择**用于返回数据的语句是单例 SELECT 语句;用于返回数据的语句是单例 SELECT 语句。也就是说，它只返回一行数据。 因此，代码示例不声明或使用游标。
