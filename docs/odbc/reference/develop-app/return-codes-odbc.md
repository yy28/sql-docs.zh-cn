---
title: 返回代码 ODBC |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- return codes [ODBC]
- diagnostic information [ODBC], return codes
ms.assetid: e893b719-4392-476f-911a-5ed6da6f7e94
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 15e434025ed1201ca61371c2fb88e70143e131a5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304308"
---
# <a name="return-codes-odbc"></a>返回代码 ODBC
ODBC 中的每个函数返回一个代码，称为*返回代码，* 它指示函数的总体成功或失败。 程序逻辑通常基于返回代码。  
  
 例如，以下代码调用**SQLFetch**来检索结果集中的行。 它检查函数的返回代码，以确定是否到达了结果集的末尾（SQL_NO_DATA）、是否返回了任何警告信息（SQL_SUCCESS_WITH_INFO），或者是否发生了错误（SQL_ERROR）。  
  
```  
SQLRETURN   rc;  
SQLHSTMT    hstmt;  
  
while ((rc=SQLFetch(hstmt)) != SQL_NO_DATA) {  
   if (rc == SQL_SUCCESS_WITH_INFO) {  
      // Call function to display warning information.  
   } else if (rc == SQL_ERROR) {  
      // Call function to display error information.  
      break;  
   }  
   // Process row.  
}  
```  
  
 返回代码 SQL_INVALID_HANDLE 始终指示编程错误，并且决不能在运行时遇到。 所有其他返回代码提供运行时信息，但 SQL_ERROR 可以指示编程错误。  
  
 下表定义了返回代码。  
  
|返回代码|描述|  
|-----------------|-----------------|  
|SQL_SUCCESS|功能已成功完成。 应用程序调用**SQLGetDiagField**从标头记录检索其他信息。|  
|SQL_SUCCESS_WITH_INFO|功能成功完成，可能带有非致命错误（警告）。 该应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**来检索其他信息。|  
|SQL_ERROR|功能失败。 该应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**来检索其他信息。 函数的任何输出参数的内容都是未定义的。|  
|SQL_INVALID_HANDLE|由于环境、连接、语句或描述符句柄无效，功能失败。 这表示编程错误。 **SQLGetDiagRec**或**SQLGetDiagField**没有其他信息。 仅当句柄为空指针或类型错误（例如为需要连接句柄的参数传递语句句柄时）才返回此代码。|  
|SQL_NO_DATA|没有更多的数据可用。 该应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**来检索其他信息。 可以返回 02xxx 类中的一个或多个驱动程序定义的状态记录。 **注：** 在 ODBC 2 中。*x*，此返回码SQL_NO_DATA_FOUND。|  
|SQL_NEED_DATA|需要更多的数据，例如何时在执行时发送参数数据或需要额外的连接信息。 该应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**来检索其他信息（如果有）。|  
|SQL_STILL_EXECUTING|以异步方式启动的函数仍在执行中。 该应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**来检索其他信息（如果有）。|
