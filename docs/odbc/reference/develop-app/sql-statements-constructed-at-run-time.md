---
title: 在运行时构造的 SQL 语句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- run time constructed SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], building at run time
ms.assetid: f6554486-d49c-436a-82e3-4c158d26acd8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0573851ee93bda4aa33e8645148cf2ee66200bee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149134"
---
# <a name="sql-statements-constructed-at-run-time"></a>在运行时构造的 SQL 语句
执行即席分析常用的应用程序在运行时生成的 SQL 语句。 例如，电子表格可能会使用户能够选择要从其中检索数据的列：  
  
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
  
 应用程序通常在运行时构建 SQL 语句的另一个类是应用程序的开发环境。 但是，它们构建的语句是硬编码它们要构建，其中它们通常进行优化和测试应用程序中。  
  
 在运行时构造 SQL 语句的应用程序可以向用户提供更大的灵活性。 前面的示例，甚至不支持等常见操作中可以看出**其中**子句**ORDER BY**子句或联接，在运行时构造 SQL 语句是代价相当复杂比硬编码的语句。 此外，测试此类应用程序是有问题的因为它们可以构造任意数目的 SQL 语句。  
  
 在运行时构造 SQL 语句的一个潜在缺点是它将比以往更多时间来构造的语句不是使用硬编码的语句。 幸运的是，这并不是问题。 此类应用程序往往是占用大量用户界面，且应用程序所花费的时间构造 SQL 语句是通常较小用户在输入条件方面所花费的时间。
