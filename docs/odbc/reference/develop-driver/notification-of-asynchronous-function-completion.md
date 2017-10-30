---
title: "异步函数完成通知的 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 336565da-4203-4745-bce2-4f011c08e357
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 91c63c55a3d36e1b0c788361a8ae13a01ece9a38
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="notification-of-asynchronous-function-completion"></a>异步函数完成通知的
在 Windows 8 SDK 中，ODBC 添加一种机制，以通知应用程序，一个异步操作完成后，我们将称为"通知在完成"。 (请参阅[异步执行 （通知方法）](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)有关详细信息。)本主题将讨论的一些问题的驱动程序开发人员。  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>驱动程序管理器和驱动程序之间的接口  
 驱动程序管理器内部提供的回调函数[SQLAsyncNotificationCallback 函数](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md)。 **SQLAsyncNotificationCallback**只能调用由驱动程序-应用程序不能直接调用它。 驱动程序调用**SQLAsyncNotificationCallback**每当新的数据从服务器收到最后一个返回 SQL_STILL_EXECUTING 后。  
  
 驱动程序管理器提供的回调机制，以便在相应的函数返回 SQL_STILL_EXECUTING 之后执行一个异步操作在进行某些进度时，驱动程序可以通知驱动程序管理器  
  
 驱动程序管理器与非 NULL 函数指针的类型 SQL_ASYNC_NOTIFICATION_CALLBACK，为要参与通知模式的驱动程序的驱动程序连接句柄设置 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 属性任何异步该句柄上的操作。 同样，驱动程序管理器可以用一个非 NULL 函数的指针，它还为类型 SQL_ASYNC_NOTIFICATION_CALLBACK，驱动程序通知模式中的工作的驱动程序语句句柄设置 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 属性该句柄上所有异步操作。  
  
 如果驱动程序句柄上执行异步操作，则应在非阻塞样式中运行的异步驱动程序函数。 如果无法立即完成的操作，该驱动程序函数应返回 SQL_STILL_EXECUTING。 此要求适用于轮询模式和通知模式。  
  
 如果句柄是通知的异步模式中，该驱动程序必须调用通知回调函数，其地址为 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK 或 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 属性的值，一次后返回 SQL_STILL_EXECUTING。 换而言之，一个返回 SQL_STILL_EXECUTING 必须成对使用的通知回调函数的一个调用。 该驱动程序应 SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT 或 SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT 句柄属性的当前值作为值将用于该调用后函数参数*pContext*。  
  
 该驱动程序必须在调用驱动程序函数中; 线程中返回调用没有无需函数返回前通知进度。 该驱动程序应使用回调到各自的线程。 驱动程序管理器不会使用驱动程序的回调线程用于执行大量的处理逻辑。  
  
 驱动程序管理器将再次调用原始函数之后该驱动程序回调。 驱动程序管理器可以使用一个应用程序线程和驱动程序线程都不是一个线程。 如果驱动程序使用一些与线程 （例如，安全令牌或用户标识符） 相关联的信息，该驱动程序应将所需的信息保存在初始的异步调用，并使用整个异步操作之前保存的值完成。 通常情况下，仅**SQLDriverConnect**， **SQLConnect**，或**SQLBrowseConnect**需要使用该类型的信息。  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)

