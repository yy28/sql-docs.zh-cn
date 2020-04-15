---
title: 运行时构造的 SQL 语句 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 795335be2a2a3aab1be6dac26bf6d213161fe42e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301968"
---
# <a name="sql-statements-constructed-at-run-time"></a>在运行时构造的 SQL 语句
执行临时分析的应用程序通常在运行时生成 SQL 语句。 例如，电子表格可能允许用户选择要从中检索数据的列：  
  
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
  
 通常在运行时构造 SQL 语句的另一类应用程序是应用程序开发环境。 但是，它们构造的语句在构建的应用程序中是硬编码的，通常可以在其中对其进行优化和测试。  
  
 在运行时构造 SQL 语句的应用程序可以为用户提供极大的灵活性。 从前面的示例中可以看出，它甚至不支持**像 WHERE**子句 **、ORDER BY**子句或联接这样的常见操作，在运行时构造 SQL 语句比硬编码语句复杂得多。 此外，测试此类应用程序存在问题，因为它们可以构造任意数量的 SQL 语句。  
  
 在运行时构造 SQL 语句的潜在缺点是，构建语句所需的时间比使用硬编码语句的时间要多得多。 幸运的是，这很少是一个问题。 此类应用程序往往占用用户界面，与用户输入条件的时间相比，应用程序构建 SQL 语句所花费的时间通常很小。
