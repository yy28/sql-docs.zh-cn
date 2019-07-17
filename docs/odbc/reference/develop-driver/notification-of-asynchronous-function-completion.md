---
title: 异步函数完成通知的 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 336565da-4203-4745-bce2-4f011c08e357
author: MightyPen
ms.author: genemi
ms.openlocfilehash: de3496661f2ab329e5bf662a9cb8fa749cb81bfc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129321"
---
# <a name="notification-of-asynchronous-function-completion"></a>异步函数完成通知
在 Windows 8 SDK、 ODBC 添加了一种机制，以通知应用程序的异步操作完成后，我们将称为"完成后通知"。 (请参阅[异步执行 （通知方法）](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)有关详细信息。)本主题将讨论的一些问题的驱动程序开发人员。  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>驱动程序管理器和驱动程序之间的接口  
 驱动程序管理器在内部提供的回调函数[SQLAsyncNotificationCallback 函数](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md)。 **SQLAsyncNotificationCallback**只能在调用由驱动程序-应用程序不能直接调用它。 驱动程序调用**SQLAsyncNotificationCallback**每当新的数据从服务器收到后最后一个返回 SQL_STILL_EXECUTING。  
  
 驱动程序管理器提供了一种回调机制，以便在相应的函数返回 SQL_STILL_EXECUTING 后执行异步操作在进行某些进度时，驱动程序可以通知驱动程序管理器  
  
 驱动程序管理器设置 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 属性上驱动程序连接句柄与非 NULL 函数指针的类型 SQL_ASYNC_NOTIFICATION_CALLBACK，驱动程序在的通知模式下工作的任何异步对该句柄的操作。 同样，驱动程序管理器设置上驱动程序语句句柄类型 SQL_ASYNC_NOTIFICATION_CALLBACK，驱动程序在的通知模式下工作的也是为非 NULL 函数指针 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 属性该句柄的任何异步操作。  
  
 如果驱动程序句柄上执行异步操作，则应在非阻止性样式中运行的异步驱动程序函数。 如果无法立即完成的操作，该驱动程序函数应返回 SQL_STILL_EXECUTING。 此要求适用于轮询模式和通知模式。  
  
 如果句柄是在通知异步模式下，该驱动程序必须调用通知回调函数，其地址为 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 或 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 属性的值，一次后返回 SQL_STILL_EXECUTING。 换而言之，必须使用一个通知回调函数的调用配对一个返回 SQL_STILL_EXECUTING。 该驱动程序应调用后的函数参数的值使用 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT 或 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT 句柄属性的当前值*pContext*。  
  
 该驱动程序不能调用驱动程序函数中; 在线程中返回调用没有理由在函数返回前通知进度。 该驱动程序应使用其自己的线程回调。 驱动程序管理器不会执行大量的处理逻辑使用驱动程序的回调线程。  
  
 驱动程序调用返回后，驱动程序管理器将再次调用原始函数。 驱动程序管理器可能使用不是应用程序线程或驱动程序线程的线程。 如果驱动程序使用与线程 （例如，安全令牌或用户标识符） 关联的某些信息，该驱动程序应将所需的信息保存在初始的异步调用，并使用整个异步操作之前保存的值完成。 通常情况下，仅**SQLDriverConnect**， **SQLConnect**，或**SQLBrowseConnect**需要使用此类信息。  
  
## <a name="see-also"></a>请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
