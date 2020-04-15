---
title: 使用 SQLGetDiagRec 和 SQLGetDiagField |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69a17086253b40469b0ed98cb6f870f319f03f52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306748"
---
# <a name="using-sqlgetdiagrec-and-sqlgetdiagfield"></a>使用 SQLGetDiagRec 和 SQLGetDiagField
应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**来检索诊断信息。 这些函数接受环境、连接、语句或描述符句柄，并从上次使用该句柄的函数返回诊断。 当使用该句柄调用新功能时，在特定句柄上记录的诊断将被丢弃。 如果函数返回多个诊断记录，应用程序会多次调用这些函数;如果函数返回多个诊断记录，则调用这些函数。通过使用SQL_DIAG_NUMBER选项调用**SQLGetDiagField**获取标头记录（记录 0）来检索状态记录的总数。  
  
 应用程序通过调用**SQLGetDiagField**并指定要检索的字段来检索各个诊断字段。 某些诊断字段对某些类型的句柄没有任何意义。 有关诊断字段及其含义的列表，请参阅[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)函数说明。  
  
 应用程序通过调用**SQLGetDiagRec**在单个调用中检索 SQLSTATE、本机错误代码和诊断消息。**SQLGetDiagRec**不能用于从标头记录中检索信息。  
  
 例如，以下代码提示用户执行 SQL 语句。 如果返回任何诊断信息，它将调用**SQLGetDiagField**获取状态记录的数量，并从这些记录获取**SQLSTATE、** 本机错误代码和诊断消息。  
  
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
