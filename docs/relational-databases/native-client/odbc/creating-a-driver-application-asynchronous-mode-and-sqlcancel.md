---
title: "异步模式和 SQLCancel |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|ODBC
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- asynchronous operations [SQL Server Native Client]
- SQLCancel function
- SQLSetConnectAttr function
- SQL Server Native Client, asynchronous operations
- ODBC functions
- ODBC applications, asynchronous operations
- SQL Server Native Client ODBC driver, asynchronous mode
ms.assetid: f31702a2-df76-4589-ac3b-da5412c03dc2
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 197375f12781b72ece9ef90ae0dac5043b862d41
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="creating-a-driver-application---asynchronous-mode-and-sqlcancel"></a>创建驱动程序应用程序的异步模式和 SQLCancel
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  某些 ODBC 函数既可同步操作，也可以异步操作。 应用程序可以为语句句柄或连接句柄启用异步操作。 如果为连接句柄设置了该选项，它将影响连接句柄上的所有语句句柄。 应用程序使用以下语句启用或禁用异步操作：  
  
```  
SQLSetConnectAttr(hdbc, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_ON, SQL_IS_INTEGER);  
SQLSetConnectAttr(hdbc, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_OFF, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_ON, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_OFF, SQL_IS_INTEGER);  
```  
  
 当某个应用程序以异步模式调用 ODBC 函数，在得到服务器已完成命令的通知之前，驱动程序不向应用程序返回控制权。  
  
 异步操作时，驱动程序立即向应用程序返回控制权，甚至在向服务器发送命令之前也可以。 驱动程序将返回代码设置为 SQL_STILL_EXECUTING。 应用程序随后可执行其他工作。  
  
 当应用程序测试命令是否完成时，它会向驱动程序发出带有相同参数的相同函数调用。 如果驱动程序尚未从服务器接收到回复，它将再次返回 SQL_STILL_EXECUTING。 应用程序必须定期测试该命令，直到返回 SQL_STILL_EXECUTING 之外的代码。 当应用程序收到其他任何返回代码（甚至是 SQL_ERROR）后，它可以确定命令是否已完成。  
  
 有时某个命令长时间未完成。 如果应用程序需要取消命令而无需等待答复，则可采用通过调用**SQLCancel**使用相同的语句作为未完成命令的处理。 这是唯一一次**SQLCancel**应使用。 某些程序员使用**SQLCancel**时处理这些情况下方式通过结果设置并且想要取消的结果集的其余部分。 [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md)或[SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md)应该用于不取消未完成的结果集的其余部分**SQLCancel**。  
  
## <a name="see-also"></a>另请参阅  
 [创建 SQL Server Native Client ODBC 驱动程序应用程序](../../../relational-databases/native-client/odbc/creating-a-driver-application.md)  
  
  
