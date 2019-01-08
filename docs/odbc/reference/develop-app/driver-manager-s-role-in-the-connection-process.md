---
title: 驱动程序管理器&#39;s 的连接过程中的角色 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], role in connection process
- connecting to data source [ODBC], driver manager
- connecting to driver [ODBC], driver manager
- ODBC driver manager [ODBC]
ms.assetid: 77c05630-5a8b-467d-b80e-c705dc06d601
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: af81fd6c4b0b56474497a829985a754ccf88f3ff
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52408844"
---
# <a name="driver-manager39s-role-in-the-connection-process"></a>驱动程序管理器&#39;s 的连接过程中的角色
请记住，应用程序不要直接调用驱动程序函数。 相反，这些驱动程序管理器具有相同名称的函数调用和驱动程序管理器调用驱动程序函数。 通常情况下，这几乎会立即发生。 例如，在应用程序调用**SQLExecute**驱动程序管理器中，一些错误检查之后，驱动程序管理器调用**SQLExecute**驱动程序中。  
  
 连接过程是不同的。 当应用程序调用**SQLAllocHandle** SQL_HANDLE_ENV 和 SQL_HANDLE_DBC 选项，该函数分配句柄仅在驱动程序管理器。 驱动程序管理器不会调用此函数在驱动程序中的，因为它不知道要调用的驱动程序。 同样，如果应用程序传递一个未连接到连接的句柄**SQLSetConnectAttr**或**SQLGetConnectAttr**，只有驱动程序管理器执行的函数。 它将存储，或者获取从其连接的属性值处理，并返回 SQLSTATE 08003 （连接未打开），尚未设置属性获取值并用于哪些 ODBC 未定义默认值。  
  
 当应用程序调用**SQLConnect**， **SQLDriverConnect**，或**SQLBrowseConnect**，驱动程序管理器首先确定要使用的驱动程序。 然后，它检查，以确定在连接上当前是否加载了驱动程序：  
  
-   如果在连接上不加载任何驱动程序，则驱动程序管理器检查是否在同一环境中的另一个连接上加载指定的驱动程序。 如果不是，驱动程序管理器将加载上连接并调用的驱动程序**SQLAllocHandle** SQL_HANDLE_ENV 选项与驱动程序中。  
  
     然后，驱动程序管理器调用**SQLAllocHandle**中使用 SQL_HANDLE_DBC 选项的驱动程序，该值指示是否是只需加载。 如果应用程序设置连接属性，驱动程序管理器调用**SQLSetConnectAttr**在驱动程序; 如果出错，则驱动程序管理器的连接函数将返回 SQLSTATE IM006 (驱动程序的**SQLSetConnectAttr**失败)。 最后，驱动程序管理器驱动程序中调用的连接函数。  
  
-   如果在连接上加载指定的驱动程序，则驱动程序管理器驱动程序中调用仅连接函数。 在这种情况下，该驱动程序必须确保在连接上的所有连接属性都保留其当前设置。  
  
-   如果在连接上加载不同的驱动程序，则驱动程序管理器调用**SQLFreeHandle**驱动程序以释放连接中。 如果不没有使用该驱动程序的任何其他连接，驱动程序管理器会调用**SQLFreeHandle**驱动程序以释放环境中并卸载该驱动程序。 然后，驱动程序管理器执行与该连接未加载驱动程序时相同的操作。  
  
 驱动程序管理器将会锁定环境句柄 (*henv*) 调用的驱动程序之前**SQLAllocHandle**并**SQLFreeHandle**时*HandleType*设置为**SQL_HANDLE_DBC**。  
  
 当应用程序调用**SQLDisconnect**，驱动程序管理器调用**SQLDisconnect**驱动程序中。 但是，它使应用程序重新连接到该驱动程序的情况下加载的驱动程序。 当应用程序调用**SQLFreeHandle** SQL_HANDLE_DBC 选项后，驱动程序管理器调用**SQLFreeHandle**驱动程序中。 如果驱动程序不使用任何其他连接，然后调用驱动程序管理器**SQLFreeHandle**中与 SQL_HANDLE_ENV 驱动程序选项和卸载该驱动程序。
