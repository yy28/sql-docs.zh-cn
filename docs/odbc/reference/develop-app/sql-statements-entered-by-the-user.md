---
description: 用户输入的 SQL 语句
title: 用户输入的 SQL 语句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- user-entered SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], entered by user
ms.assetid: 109af162-93ba-425a-8fe5-49c7dc7cc784
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6d7d7ee7ffc2a4c949173c3eee888e4c41b9e741
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424539"
---
# <a name="sql-statements-entered-by-the-user"></a>用户输入的 SQL 语句
执行即席分析的应用程序也通常允许用户直接输入 SQL 语句。 例如：  
  
```  
SQLCHAR *     Statement, SqlState[6], Msg[SQL_MAX_MESSAGE_LENGTH];  
SQLSMALLINT   i, MsgLen;  
SQLINTEGER    NativeError;  
SQLRETURN     rc1, rc2;  
  
// Prompt user for SQL statement.  
GetSQLStatement(Statement);  
  
// Execute the statement directly. Because it will be executed only once,  
// do not prepare it.  
rc1 = SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Process any errors or returned information.  
if ((rc1 == SQL_ERROR) || rc1 == SQL_SUCCESS_WITH_INFO) {  
   i = 1;  
   while ((rc2 = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, SqlState, &NativeError,  
         Msg, sizeof(Msg), &MsgLen)) != SQL_NO_DATA) {  
      DisplayError(SqlState, NativeError, Msg, MsgLen);  
      i++;  
   }  
}  
```  
  
 此方法简化了应用程序编码;应用程序依赖于用户生成 SQL 语句，并依赖于数据源来检查语句的有效性。 由于很难编写充分公开 SQL 复杂性的图形用户界面，因此只需要求用户输入 SQL 语句文本可能是首选的替代方法。 但是，这要求用户不仅知道 SQL，还需要知道正在查询的数据源的架构。 某些应用程序提供了一个图形用户界面，用户可以通过该界面创建基本的 SQL 语句，还可以提供一个文本界面，用户可以使用该界面来修改它。
