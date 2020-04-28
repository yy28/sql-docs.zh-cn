---
title: 返回代码 ODBC |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304308"
---
# <a name="return-codes-odbc"></a>返回代码 ODBC
ODBC 中的每个函数都返回一个称为其*返回代码*的代码，该代码指示函数的总体成功或失败。 程序逻辑通常基于返回代码。  
  
 例如，下面的代码调用**SQLFetch**来检索结果集中的行。 它将检查函数的返回代码，以确定是否已到达结果集的末尾（SQL_NO_DATA）、是否返回了任何警告信息（SQL_SUCCESS_WITH_INFO），或者是否发生了错误（SQL_ERROR）。  
  
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
  
|返回代码|说明|  
|-----------------|-----------------|  
|SQL_SUCCESS|函数已成功完成。 应用程序调用**SQLGetDiagField**从标头记录中检索其他信息。|  
|SQL_SUCCESS_WITH_INFO|函数已成功完成，可能出现非致命错误（警告）。 应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**来检索其他信息。|  
|SQL_ERROR|函数失败。 应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**来检索其他信息。 未定义函数的任何输出参数的内容。|  
|SQL_INVALID_HANDLE|由于环境、连接、语句或描述符句柄无效，函数失败。 这表明编程错误。 **SQLGetDiagRec**或**SQLGetDiagField**中不提供任何其他信息。 仅当句柄为空指针或类型错误时，才返回此代码，例如，为需要连接句柄的参数传递语句句柄。|  
|SQL_NO_DATA|没有更多的可用数据。 应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**来检索其他信息。 可以返回类02xxx 中的一个或多个驱动程序定义的状态记录。 **注意：** 在 ODBC 2 中。*x*，此返回代码的名称为 SQL_NO_DATA_FOUND。|  
|SQL_NEED_DATA|需要更多数据，如在执行时发送参数数据或需要其他连接信息时。 应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**来检索附加信息（如果有）。|  
|SQL_STILL_EXECUTING|异步启动的函数仍在执行。 应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**来检索附加信息（如果有）。|
