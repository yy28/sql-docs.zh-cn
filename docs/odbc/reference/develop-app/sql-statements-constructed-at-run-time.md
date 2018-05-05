---
title: 在运行时构造的 SQL 语句 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- run time constructed SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], building at run time
ms.assetid: f6554486-d49c-436a-82e3-4c158d26acd8
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 18f5a02bdcec575ac1362d3f656480eb0ab9b4a3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sql-statements-constructed-at-run-time"></a>在运行时构造的 SQL 语句
在运行时，通常执行即席分析的应用程序生成 SQL 语句。 例如，电子表格可能允许用户选择要从中检索数据的列：  
  
```  
// SQL_Statements_Constructed_at_Run_Time.cpp  
#include <windows.h>  
#include <stdio.h>  
#include <sqltypes.h>  
  
int main() {  
   SQLCHAR *Statement = 0, *TableName = 0;  
   SQLCHAR **TableNamesArray, **ColumnNamesArray = 0;  
   BOOL *ColumnSelectedArray = 0;  
   BOOL  CommaNeeded;  
   SQLSMALLINT i = 0, NumColumns = 0;  
  
   // Use SQLTables to build a list of tables (TableNamesArray[]). Let the  
   // user select a table and store the selected table in TableName.  
  
   // Use SQLColumns to build a list of the columns in the selected table  
   // (ColumnNamesArray). Set NumColumns to the number of columns in the  
   // table. Let the user select one or more columns and flag these columns  
   // in ColumnSelectedArray[].  
  
   // Build a SELECT statement from the selected columns.  
   CommaNeeded = FALSE;  
   Statement = (SQLCHAR*)malloc(8);  
   strcpy_s((char*)Statement, 8, "SELECT ");  
  
   for (i = 0 ; i = NumColumns ; i++) {  
      if (ColumnSelectedArray[i]) {  
         if (CommaNeeded)  
            strcat_s((char*)Statement, sizeof(Statement), ",");  
         else  
            CommaNeeded = TRUE;  
         strcat_s((char*)Statement, sizeof(Statement), (char*)ColumnNamesArray[i]);  
      }  
   }  
  
   strcat_s((char*)Statement, 15, " FROM ");  
   // strcat_s((char*)Statement, 100, (char*)TableName);  
  
   // Execute the statement . It will be executed once, do not prepare it.  
   // SQLExecDirect(hstmt, Statement, SQL_NTS);  
}  
```  
  
 应用程序通常在运行时构造 SQL 语句的另一个类是应用程序的开发环境。 但是，它们构造的语句是硬编码在它们在构建，其中他们可以通常优化和测试应用程序中。  
  
 应用程序在运行时构造 SQL 语句可以向用户提供更大的灵活性。 可以从前面的示例，甚至不支持诸如常见操作看到**其中**子句， **ORDER BY**子句或联接，在运行时构造 SQL 语句是极大地更复杂比硬编码的语句。 此外，测试此类应用程序会产生问题的因为它们可以构造任意数目的 SQL 语句。  
  
 在运行时构造 SQL 语句的潜在缺点是它需要更多的时间比使用硬编码语句构造的语句。 幸运的是，这很少是一个问题。 此类应用程序往往是一个用户界面大量和应用程序所花费的时间构造 SQL 语句是通常不大与用户所输入的条件花费的时间进行比较。
