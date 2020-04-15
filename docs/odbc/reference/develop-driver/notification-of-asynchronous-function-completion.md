---
title: 异步功能完成通知 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287817"
---
# <a name="notification-of-asynchronous-function-completion"></a>异步函数完成通知
在 Windows 8 SDK 中，ODBC 添加了一种机制，以便在异步操作完成时通知应用程序，我们将将其称为"完成通知"。 （有关详细信息，请参阅[异步执行（通知方法）。](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)本主题讨论驱动程序开发人员的一些问题。  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>驱动程序管理器和驱动程序之间的接口  
 驱动程序管理器内部提供回调函数[SQLAsync 通知回调函数](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md)。 **SQLAsync 通知回调**只能由驱动程序调用 - 应用程序不能直接调用它。 每当上次返回SQL_STILL_EXECUTING后从服务器收到新数据时，驱动程序都会调用**SQLAsync 通知回拨。**  
  
 驱动程序管理器提供回调机制，这样当相应的函数返回SQL_STILL_EXECUTING后，在执行异步操作方面取得了一些进展时，驱动程序可以通知驱动程序管理器SQL_STILL_EXECUTING  
  
 驱动程序管理器使用非 NULL 函数指针在驱动程序连接句柄上设置SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK属性，该指针的类型为SQL_ASYNC_NOTIFICATION_CALLBACK，以便驱动程序在该句柄上的任何异步操作在通知模式下工作。 同样，Driver Manager 使用非 NULL 函数指针（也属于SQL_ASYNC_NOTIFICATION_CALLBACK类型）在驱动程序语句句柄上设置SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK属性，以便驱动程序在该句柄上的任何异步操作在通知模式下工作。  
  
 如果在驱动程序句柄上执行异步操作，异步驱动程序函数应以非阻塞样式工作。 如果操作无法立即完成，则驱动程序功能应返回SQL_STILL_EXECUTING。 轮询模式和通知模式都要求此要求为 true。  
  
 如果句柄处于通知异步模式，驱动程序必须在返回SQL_STILL_EXECUTING后调用通知回调函数，该函数的地址是SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK或SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK属性的值。 换句话说，一个返回SQL_STILL_EXECUTING必须与通知回调函数的一个调用配对。 驱动程序应使用SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT的当前值或SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT句柄属性作为回调函数参数*pContext*的值。  
  
 驱动程序不得在调用驱动程序函数的线程中回调;没有理由在函数返回之前通知进度。 驱动程序应使用自己的线程进行回调。 驱动程序管理器不会使用驱动程序的回调线程执行广泛的处理逻辑。  
  
 驱动程序管理器将在驱动程序回电后再次调用原始函数。 驱动程序管理器可以使用既不是应用程序线程也不是驱动程序线程的线程。 如果驱动程序使用与线程关联的某些信息（例如，安全令牌或用户标识符），驱动程序应在初始异步调用中保存所需信息，并在整个异步操作完成之前使用保存的值。 通常，只有**SQLDriverConnect、SQLConnect**或**SQLBrowseConnect**需要使用此类信息。 **SQLConnect**  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
