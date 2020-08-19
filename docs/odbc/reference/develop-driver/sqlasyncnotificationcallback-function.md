---
description: SQLAsyncNotificationCallback 函数
title: SQLAsyncNotificationCallback 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c56aedc9-f7f7-4641-b605-f0f98ed4400c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b9d03e8a3fa7e62c19dd09a210dca3a56348c692
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476226"
---
# <a name="sqlasyncnotificationcallback-function"></a>SQLAsyncNotificationCallback 函数
**度**  
 引入的版本： ODBC 3。8  
  
 标准符合性：无  
  
 **摘要**  
 当驱动程序返回 SQL_STILL_EXECUTING 后，当当前异步操作有一些进度时， **SQLAsyncNotificationCallback**允许驱动程序回叫驱动程序管理器。 **SQLAsyncNotificationCallback** 只能由驱动程序调用。  
  
 驱动程序不会将 **SQLAsyncNotificationCallback** 与函数名称 **SQLAsyncNotificationCallback**一起调用。 相反，驱动程序管理器会将函数指针作为相应连接句柄或语句句柄的 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 或 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 属性的值传递给驱动程序。 可以为不同的句柄分配不同的函数指针值。 函数指针的类型定义为 SQL_ASYNC_NOTIFICATION_CALLBACK。  
  
 **SQLAsyncNotificationCallback** 是线程安全的。 驱动程序可以选择使用多个线程同时在不同的句柄上调用 **SQLAsyncNotificationCallback** 。  
  
## <a name="syntax"></a>语法  
  
```  
typedef SQLRETURN (SQL_API *SQL_ASYNC_NOTIFICATION_CALLBACK)(  
   SQLPOINTER pContex,   
   BOOL fLast);  
```  
  
## <a name="arguments"></a>参数  
 *pContex*  
 指向由驱动程序管理器定义的数据结构的指针。 通过 SQLSetConnectAttr (SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT) 或 SQLSetStmtAttr (SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT) 将值传递给驱动程序。  驱动程序无法访问值。  
  
 *fLast*  
 由驱动程序用来指示此回调函数调用是当前异步操作的最后一个。 驱动程序管理器再次调用函数时，驱动程序将返回除 SQL_STILL_EXECUTING 以外的返回代码。 例如，驱动程序管理器可能会使用此信息来提前通知应用程序异步操作将完成。  
  
 如果 *句柄* 不是 *HandleType*指定的类型的有效句柄，则 **SQLCancelHandle** 将返回 SQL_INVALID_HANDLE。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS 或 SQL_ERROR。  
  
## <a name="diagnostics"></a>诊断  
 在以下两种情况下， **SQLAsyncNotificationCallback**可能会返回 SQL_ERROR (这表明驱动程序或驱动程序管理器中的实现问题。  
  
|错误|说明|  
|-----------|-----------------|  
|连接或语句未请求通知。||  
|*句柄*无效|驱动程序传入了无效的句柄，导致内部驱动程序管理器验证测试失败。|  
  
## <a name="see-also"></a>另请参阅  
 [异步执行 (轮询方法) ](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
