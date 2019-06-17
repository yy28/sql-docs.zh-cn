---
title: SQLAsyncNotificationCallback Function | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c56aedc9-f7f7-4641-b605-f0f98ed4400c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b78764e1dccb7118d43cc967f3b03838366d6eb0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63224513"
---
# <a name="sqlasyncnotificationcallback-function"></a>SQLAsyncNotificationCallback 函数
**符合性**  
 版本引入了：ODBC 3.8  
  
 标准符合性：None  
  
 **摘要**  
 **SQLAsyncNotificationCallback**使驱动程序没有为当前的异步操作的某些进度后驱动程序返回 SQL_STILL_EXECUTING 时回调到驱动程序管理器。 **SQLAsyncNotificationCallback**只能由驱动程序调用。  
  
 驱动程序不调用**SQLAsyncNotificationCallback**使用函数名**SQLAsyncNotificationCallback**。 相反，驱动程序管理器函数将指针传递到驱动程序的相应连接句柄或语句句柄的 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 或 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 属性的值分别。 可在不同的图柄分配不同的函数指针值。 函数指针的类型定义为 SQL_ASYNC_NOTIFICATION_CALLBACK。  
  
 **SQLAsyncNotificationCallback**是线程安全的。 驱动程序可以选择使用多个线程调用**SQLAsyncNotificationCallback**上不同处理同时。  
  
## <a name="syntax"></a>语法  
  
```  
typedef SQLRETURN (SQL_API *SQL_ASYNC_NOTIFICATION_CALLBACK)(  
   SQLPOINTER pContex,   
   BOOL fLast);  
```  
  
## <a name="arguments"></a>参数  
 *pContex*  
 定义由驱动程序管理器中的数据结构的指针。 通过 SQLSetConnectAttr(SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT) 或 SQLSetStmtAttr(SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT) 传递给驱动程序的值。  该驱动程序没有访问的值。  
  
 *fLast*  
 由驱动程序来指示调用此回调函数是当前的异步操作的最后一个。 驱动程序管理器会再次调用该函数时，该驱动程序将返回 SQL_STILL_EXECUTING 之外的返回代码。 驱动程序管理器可能会使用此信息，例如，若要通知的应用程序预先将完成异步操作。  
  
 如果*处理*不是由指定类型的有效句柄*HandleType*， **SQLCancelHandle**返回 SQL_INVALID_HANDLE。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS 或 SQL_ERROR。  
  
## <a name="diagnostics"></a>诊断  
 **SQLAsyncNotificationCallback**可以返回 SQL_ERROR，以下两种情况下 （这些指示驱动程序或驱动程序管理器中的实现问题。  
  
|错误|Description|  
|-----------|-----------------|  
|连接或语句没有请求通知。||  
|无效*处理*|该驱动程序传递失败的内部驱动程序管理器验证测试的无效句柄。|  
  
## <a name="see-also"></a>请参阅  
 [异步执行（轮询方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
