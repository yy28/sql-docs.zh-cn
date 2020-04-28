---
title: 异步函数完成通知 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 336565da-4203-4745-bce2-4f011c08e357
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a453967f2ffdda4af2a44429737f700f4a994cf8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287817"
---
# <a name="notification-of-asynchronous-function-completion"></a>异步函数完成通知
在 Windows 8 SDK 中，ODBC 添加了一种机制，用于在异步操作完成时通知应用程序，我们将其称为 "完成时通知"。 （有关详细信息，请参阅[异步执行（通知方法）](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md) 。）本主题讨论了驱动程序开发人员的一些问题。  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>驱动程序管理器和驱动程序之间的接口  
 驱动程序管理器内部提供回调函数[SQLAsyncNotificationCallback 函数](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md)。 **SQLAsyncNotificationCallback**只能由驱动程序调用--应用程序不能直接调用它。 当最后一次返回 SQL_STILL_EXECUTING 从服务器接收到的新数据时，驱动程序将调用**SQLAsyncNotificationCallback** 。  
  
 驱动程序管理器提供回调机制，以便驱动程序管理器可以在相应函数返回后执行异步操作时通知驱动程序管理器 SQL_STILL_EXECUTING  
  
 驱动程序管理器将驱动程序连接句柄上的 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 属性设置为包含 SQL_ASYNC_NOTIFICATION_CALLBACK 类型的非 NULL 函数指针，以便驱动程序在该句柄的任何异步操作的通知模式下工作。 同样，驱动程序管理器使用非 NULL 函数指针（也是 SQL_ASYNC_NOTIFICATION_CALLBACK 类型）对驱动程序语句句柄设置 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 特性，以便驱动程序在该句柄的任何异步操作的通知模式下工作。  
  
 如果对驱动程序句柄执行异步操作，则异步驱动程序函数应以非阻止样式工作。 如果操作无法立即完成，驱动程序函数应返回 SQL_STILL_EXECUTING。 对于轮询模式和通知模式，此要求均为 true。  
  
 如果句柄处于通知异步模式，则驱动程序必须调用通知回调函数，其 address 为 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 或 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 属性的值，并在返回 SQL_STILL_EXECUTING 后一次。 换言之，一个返回 SQL_STILL_EXECUTING 必须与一个通知回调函数调用成对出现。 驱动程序应使用 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT 的当前值，或将 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT 句柄特性的值用作回调函数参数*pContext*的值。  
  
 驱动程序不得在调用驱动程序函数的线程中回调;在函数返回之前，没有理由通知进度。 驱动程序应使用其自己的线程来回调。 驱动程序管理器不会使用驱动程序的回调线程来执行大量处理逻辑。  
  
 驱动程序管理器将在驱动程序回调之后再次调用原始函数。 驱动程序管理器可能使用既不是应用程序线程也不是驱动程序线程的线程。 如果驱动程序使用与线程关联的某些信息（例如，安全令牌或用户标识符），则驱动程序应在初始异步调用中保存所需的信息，并在整个异步操作完成之前使用保存的值。 通常，只有**SQLDriverConnect**、 **SQLConnect**或**SQLBrowseConnect**需要使用这种类型的信息。  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
