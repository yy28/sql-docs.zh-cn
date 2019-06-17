---
title: 使用 SQLGetDiagRec 和 SQLGetDiagField |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 4f486bb1-fad8-4064-ac9d-61f2de85b68b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1db402e7c015ef50ce47b5137e670d9f1836a326
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63208430"
---
# <a name="using-sqlgetdiagrec-and-sqlgetdiagfield"></a>使用 SQLGetDiagRec 和 SQLGetDiagField
应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**检索诊断信息。 这些函数接受一个环境、 连接、 语句或描述符句柄，并从上一次使用该句柄的函数返回诊断。 使用该句柄调用新的函数时，将被丢弃特定句柄上记录的诊断。 如果该函数返回多个诊断记录，应用程序调用这些函数多次;通过调用检索的状态记录总数**SQLGetDiagField** SQL_DIAG_NUMBER 选项具有的标头记录 （记录 0）。  
  
 应用程序通过调用来检索各个诊断字段**SQLGetDiagField**并指定要检索的字段。 特定诊断字段没有任何意义，对某些类型的句柄。 诊断字段及其含义的列表，请参阅[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)函数说明。  
  
 应用程序通过调用检索 SQLSTATE、 本机错误代码和单个调用中的诊断消息**SQLGetDiagRec**;**SQLGetDiagRec**不能用于从标头记录中检索信息。  
  
 例如，下面的代码会提示用户输入的 SQL 语句，并执行它。 如果未返回任何诊断信息，则会调用**SQLGetDiagField**若要获取的状态记录数和**SQLGetDiagRec**从那些获取 SQLSTATE、 本机错误代码和诊断消息记录。  
  
```  
SQLCHAR       SqlState[6], SQLStmt[100], Msg[SQL_MAX_MESSAGE_LENGTH];  
SQLINTEGER    NativeError;  
SQLSMALLINT   i, MsgLen;  
SQLRETURN     rc1, rc2;  
SQLHSTMT      hstmt;  
  
// Prompt the user for an SQL statement.  
GetSQLStmt(SQLStmt);  
  
// Execute the SQL statement and return any errors or warnings.  
rc1 = SQLExecDirect(hstmt, SQLStmt, SQL_NTS);  
if ((rc1 == SQL_SUCCESS_WITH_INFO) || (rc1 == SQL_ERROR)) {
   SQLLEN numRecs = 0;
   SQLGetDiagField(SQL_HANDLE_STMT, hstmt, 0, SQL_DIAG_NUMBER, &numRecs, 0, 0);
   // Get the status records.
   i = 1;  
   while (i <= numRecs && (rc2 = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, SqlState, &NativeError,  
            Msg, sizeof(Msg), &MsgLen)) != SQL_NO_DATA) {  
      DisplayError(SqlState,NativeError,Msg,MsgLen);  
      i++;  
   }  
}  
  
if ((rc1 == SQL_SUCCESS) || (rc1 == SQL_SUCCESS_WITH_INFO)) {  
   // Process statement results, if any.  
}  
```
