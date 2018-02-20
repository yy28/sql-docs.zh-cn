---
title: "使用 SQLGetDiagRec 和 SQLGetDiagField |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 4f486bb1-fad8-4064-ac9d-61f2de85b68b
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: db4a853206e402228eb9d76dca72a421444ed042
ms.sourcegitcommit: 4edac878b4751efa57601fe263c6b787b391bc7c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2018
---
# <a name="using-sqlgetdiagrec-and-sqlgetdiagfield"></a>使用 SQLGetDiagRec 和 SQLGetDiagField
应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**检索诊断信息。 这些函数接受一个环境、 连接、 语句或描述符句柄，并从上次使用该句柄的函数返回诊断。 使用该句柄调用新函数时，将被丢弃登录特定句柄的诊断。 如果该函数返回多个诊断记录，在应用程序调用这些函数多次;通过调用检索的状态记录总数**SQLGetDiagField** SQL_DIAG_NUMBER 选项的标头记录 （记录 0）。  
  
 应用程序通过调用来检索各个诊断字段**SQLGetDiagField**并指定要检索的字段。 某些诊断字段没有任何意义对某些类型的句柄。 有关诊断的字段以及它们的含义的列表，请参阅[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)函数说明。  
  
 应用程序通过调用检索 SQLSTATE、 本机错误代码和在单个调用中的诊断消息**SQLGetDiagRec**;**SQLGetDiagRec**不能用于从标头记录中检索信息。  
  
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
