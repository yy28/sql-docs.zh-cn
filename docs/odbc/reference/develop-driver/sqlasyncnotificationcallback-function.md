---
title: "SQLAsyncNotificationCallback 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c56aedc9-f7f7-4641-b605-f0f98ed4400c
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 615792da52bcdc2dd12775d2c62450f95364b115
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sqlasyncnotificationcallback-function"></a>SQLAsyncNotificationCallback 函数
**一致性**  
 版本引入了： ODBC 3.8  
  
 标准合规性： 无  
  
 **摘要**  
 **SQLAsyncNotificationCallback**允许要在没有为当前的异步操作的某些进度驱动程序返回 SQL_STILL_EXECUTING 之后时回调到驱动程序管理器的驱动程序。 **SQLAsyncNotificationCallback**只能由驱动程序调用。  
  
 驱动程序不调用**SQLAsyncNotificationCallback**使用函数名**SQLAsyncNotificationCallback**。 相反，驱动程序管理器的函数指针到驱动程序将作为传递相应的连接句柄或语句句柄的 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 或 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 特性的值分别。 不同的句柄可能会分配不同的函数指针值。 函数指针的类型定义为 SQL_ASYNC_NOTIFICATION_CALLBACK。  
  
 **SQLAsyncNotificationCallback**是线程安全的。 驱动程序可以选择使用多个线程调用**SQLAsyncNotificationCallback**上不同处理同时。  
  
## <a name="syntax"></a>语法  
  
```  
typedef SQLRETURN (SQL_API *SQL_ASYNC_NOTIFICATION_CALLBACK)(  
   SQLPOINTER pContex,   
   BOOL fLast);  
```  
  
## <a name="arguments"></a>参数  
 *pContex*  
 指向由驱动程序管理器中定义的数据结构的指针。 通过 SQLSetConnectAttr(SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT) 或 SQLSetStmtAttr(SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT) 传递到该驱动程序的值。  该驱动程序没有值的访问。  
  
 *fLast*  
 由驱动程序用于指示此回调函数调用是当前的异步操作的最后一个。 驱动程序管理器再次调用此函数时，该驱动程序将返回非 SQL_STILL_EXECUTING 的返回代码。 驱动程序管理器可以使用此信息，例如，通知应用程序提前异步操作将完成。  
  
 如果*处理*不由指定的类型是有效句柄*HandleType*， **SQLCancelHandle**返回 SQL_INVALID_HANDLE。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS 或 SQL_ERROR。  
  
## <a name="diagnostics"></a>诊断  
 **SQLAsyncNotificationCallback**可以返回 SQL_ERROR 以下两种情况下 （这些警报表示在驱动程序或驱动程序管理器中的存在实施问题。  
  
|错误|Description|  
|-----------|-----------------|  
|连接或语句未请求通知。||  
|无效*处理*|在失败的内部的驱动程序管理器验证测试的无效句柄中传递该驱动程序。|  
  
## <a name="see-also"></a>另请参阅  
 [异步执行（轮询方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
