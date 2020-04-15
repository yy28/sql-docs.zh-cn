---
title: SQLSync 通知回拨功能 |微软文档
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
ms.openlocfilehash: e6c182c48b8e5ddb70204ddd3a94d9651f97595d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294534"
---
# <a name="sqlasyncnotificationcallback-function"></a>SQLAsyncNotificationCallback 函数
**一致性**  
 版本介绍： ODBC 3.8  
  
 标准合规性：无  
  
 **摘要**  
 **SQLAsync 通知回拨**允许驱动程序在驱动程序返回SQL_STILL_EXECUTING后当前异步操作有一些进展时回调到驱动程序管理器。 **SQLAsync 通知回调**只能由驱动程序调用。  
  
 驱动程序不调用**SQLAsync 通知回调**，功能名称**SQLAsync 通知回调**。 相反，驱动程序管理器将函数指针传递给驱动程序，作为相应连接句柄或语句句柄SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK或SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK属性的值。 可以分配不同的句柄，以指示不同的函数指针值。 函数指针的类型定义为SQL_ASYNC_NOTIFICATION_CALLBACK。  
  
 **SQLSync 通知回调**是线程安全的。 驱动程序可以选择在不同的句柄上同时使用调用**SQLAsync 通知回调**的多个线程。  
  
## <a name="syntax"></a>语法  
  
```  
typedef SQLRETURN (SQL_API *SQL_ASYNC_NOTIFICATION_CALLBACK)(  
   SQLPOINTER pContex,   
   BOOL fLast);  
```  
  
## <a name="arguments"></a>参数  
 *普康特克斯*  
 指向驱动程序管理器定义的数据结构的指针。 该值通过 SQLSetConnectAttr（SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT）或 SQLSetStmtAttr（SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT）传递给驱动程序。  驱动程序无法访问该值。  
  
 *fLast*  
 驱动程序用于指示此回调函数调用是当前异步操作的最后一个调用。 当驱动程序管理器再次调用该函数时，驱动程序将返回SQL_STILL_EXECUTING以外的返回代码。 例如，驱动程序管理器可以使用此信息提前通知应用程序异步操作将完成。  
  
 如果*句柄*不是*HandleType*指定的类型的有效句柄 **，SQLCancelHandle**将返回SQL_INVALID_HANDLE。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS或SQL_ERROR。  
  
## <a name="diagnostics"></a>诊断  
 **SQLAsync 通知回拨**可以返回以下两种情况SQL_ERROR（这些表示驱动程序或驱动程序管理器中的实现问题）。  
  
|错误|描述|  
|-----------|-----------------|  
|连接或语句未请求通知。||  
|句柄*无效*|驱动程序在无效的句柄中传递，这未通过内部驱动程序管理器验证测试。|  
  
## <a name="see-also"></a>另请参阅  
 [异步执行（轮询方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
