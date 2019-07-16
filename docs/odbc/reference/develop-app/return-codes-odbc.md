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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e5f780f9abc47a367a1825d51b12159292ace5da
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020420"
---
# <a name="return-codes-odbc"></a>返回代码 ODBC
在 ODBC 中的每个函数返回代码，称为其*返回代码，* 指示总体成功或失败的函数。 程序逻辑通常基于返回代码。  
  
 例如，下面的代码调用**SQLFetch**以检索结果集中的行。 它会检查用于确定如果 (SQL_SUCCESS_WITH_INFO) 返回任何警告信息，已达到 (SQL_NO_DATA)、 结果集的末尾或出现错误 (SQL_ERROR) 的函数的返回代码。  
  
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
  
 下表定义的返回代码。  
  
|返回代码|描述|  
|-----------------|-----------------|  
|SQL_SUCCESS|已成功完成的函数。 应用程序调用**SQLGetDiagField**标头记录中检索其他信息。|  
|SQL_SUCCESS_WITH_INFO|已成功完成，可能出现非致命错误 （警告） 的函数。 应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**检索其他信息。|  
|SQL_ERROR|失败的函数。 应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**检索其他信息。 函数的任何输出自变量的内容未定义。|  
|SQL_INVALID_HANDLE|由于环境、 连接、 语句或描述符句柄无效而失败的函数。 这指示编程错误。 从没有其他信息，则**SQLGetDiagRec**或**SQLGetDiagField**。 仅当该句柄为空指针或类型有误，如当语句句柄传递的参数所需的连接句柄时，才返回此代码。|  
|SQL_NO_DATA|没有更多数据不可用。 应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**检索其他信息。 可能返回类 02xxx 中的一个或多个驱动程序定义的状态记录。 **注意：** 在 ODBC 2。*x*，这会返回代码名为 SQL_NO_DATA_FOUND。|  
|SQL_NEED_DATA|需要更多的数据，例如在执行时发送参数数据或其他连接信息是必需的。 应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**要检索的其他信息，如果有的话。|  
|SQL_STILL_EXECUTING|以异步方式启动的函数仍在执行。 应用程序调用**SQLGetDiagRec**或**SQLGetDiagField**要检索的其他信息，如果有的话。|
