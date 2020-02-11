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
ms.openlocfilehash: 23b7539c32b6cb675f8616d9b8ec9db89be1208b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68022150"
---
# <a name="using-sqlgetdiagrec-and-sqlgetdiagfield"></a>使用 SQLGetDiagRec 和 SQLGetDiagField
应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**来检索诊断信息。 这些函数接受环境、连接、语句或描述符句柄，并从上次使用该句柄的函数返回诊断。 使用该句柄调用新的函数时，将丢弃在特定句柄上记录的诊断。 如果函数返回了多个诊断记录，应用程序将多次调用这些函数;通过使用 SQL_DIAG_NUMBER 选项为标头记录（记录0）调用**SQLGetDiagField**来检索状态记录总数。  
  
 应用程序通过调用**SQLGetDiagField**并指定要检索的字段来检索各个诊断字段。 某些诊断字段对某些类型的句柄没有任何意义。 有关诊断字段及其含义的列表，请参阅[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)函数说明。  
  
 应用程序通过调用**SQLGetDiagRec**检索单个调用中的 SQLSTATE、本机错误代码和诊断消息;**SQLGetDiagRec**不能用于从标头记录中检索信息。  
  
 例如，下面的代码提示用户提供一条 SQL 语句并执行该语句。 如果返回了任何诊断信息，则它会调用**SQLGetDiagField**来获取状态记录数和**SQLGetDiagRec** ，以获取 SQLSTATE、本机错误代码和这些记录中的诊断消息。  
  
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
