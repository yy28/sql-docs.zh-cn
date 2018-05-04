---
title: 返回代码 ODBC |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- return codes [ODBC]
- diagnostic information [ODBC], return codes
ms.assetid: e893b719-4392-476f-911a-5ed6da6f7e94
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1729e02d3529d9666b3038356471bca6d414b337
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="return-codes-odbc"></a>返回代码 ODBC
ODBC 中的每个函数返回的代码，称为其*返回代码，*指示总体成功或失败的函数。 程序逻辑通常基于返回代码。  
  
 例如，下面的代码调用**SQLFetch**检索结果集中的行。 它会检查用于确定如果结果集的末尾已达到 (SQL_NO_DATA)，如果返回任何警告信息 (SQL_SUCCESS_WITH_INFO)，或如果出错 (SQL_ERROR) 的函数的返回代码。  
  
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
  
 下表定义返回代码。  
  
|返回代码|Description|  
|-----------------|-----------------|  
|SQL_SUCCESS|已成功完成的函数。 应用程序调用**SQLGetDiagField**标头记录中检索其他信息。|  
|SQL_SUCCESS_WITH_INFO|已成功完成，可能出现非致命错误 （警告） 的函数。 应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**检索其他信息。|  
|SQL_ERROR|失败的函数。 应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**检索其他信息。 函数的任何输出参数的内容是不确定的。|  
|SQL_INVALID_HANDLE|由于无效的环境、 连接、 语句或描述符句柄失败的函数。 这指示编程错误。 无更多信息位于**SQLGetDiagRec**或**SQLGetDiagField**。 此代码是仅句柄为 null 指针，或为错误的类型，如当语句句柄传递自变量需要连接句柄时返回的。|  
|SQL_NO_DATA|没有更多数据时可用。 应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**检索其他信息。 可能返回类 02xxx 中的一个或多个驱动程序定义的状态记录。 **注意：** ODBC 2 中。*x*，这会返回代码名为 SQL_NO_DATA_FOUND。|  
|SQL_NEED_DATA|需要更多的数据，例如在执行时发送参数数据或其他连接信息是必需的。 应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**检索其他信息，如果有的话。|  
|SQL_STILL_EXECUTING|仍在执行已以异步方式启动的函数。 应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**检索其他信息，如果有的话。|
