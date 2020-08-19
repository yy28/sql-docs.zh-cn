---
description: 在运行时构造的 SQL 语句
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fff9f7a4e579ce4e1d1177b8f5fa67f7d13a4fdc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424549"
---
# <a name="sql-statements-constructed-at-run-time"></a>在运行时构造的 SQL 语句
执行即席分析的应用程序通常会在运行时生成 SQL 语句。 例如，电子表格可能允许用户选择要从中检索数据的列：  
  
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
  
 通常在运行时构造 SQL 语句的另一类应用程序是应用程序开发环境。 但是，它们构造的语句在生成的应用程序中进行了硬编码，它们通常可以进行优化和测试。  
  
 在运行时构造 SQL 语句的应用程序可以为用户提供极大的灵活性。 正如前面的示例所示，该示例甚至不 **支持在运行** 时构造 SQL 语句这样的常见 **操作，而** 是在运行时构造 SQL 语句，这比硬编码语句要复杂得多。 而且，测试此类应用程序会产生问题，因为它们可以构造任意数量的 SQL 语句。  
  
 在运行时构造 SQL 语句的一个潜在缺点是，使用硬编码语句构造语句所用的时间要多得多。 幸运的是，这种情况并不是很重要。 此类应用程序通常是用户界面密集型，与用户输入条件的时间相比，应用程序用来构造 SQL 语句的时间通常较小。
