---
title: 连接过程中的驱动程序管理器&#39;s 角色 |Microsoft Docs
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
ms.openlocfilehash: fdc7f82059579f23c9a1a1203aee5e45c87693e9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046939"
---
# <a name="driver-manager39s-role-in-the-connection-process"></a>连接过程中的驱动程序管理器&#39;s 角色
请记住，应用程序不会直接调用驱动程序函数。 相反，它们调用具有相同名称的驱动程序管理器函数，驱动程序管理器调用驱动程序函数。 通常，这种情况几乎会立即发生。 例如，应用程序会在驱动程序管理器中调用**SQLExecute** ，并在进行几次错误检查后，驱动程序管理器将在驱动程序中调用**SQLExecute** 。  
  
 连接过程是不同的。 当应用程序调用带有 SQL_HANDLE_ENV 和 SQL_HANDLE_DBC 选项的**SQLAllocHandle**时，该函数只在驱动程序管理器中分配句柄。 驱动程序管理器不会在驱动程序中调用此函数，因为它不知道要调用哪个驱动程序。 同样，如果应用程序将未连接的连接的句柄传递给**SQLSetConnectAttr**或**SQLGetConnectAttr**，则只有驱动程序管理器执行该函数。 它在获取尚未设置的属性的值时，存储或获取其连接句柄中的属性值，并在 ODBC 未定义默认值时返回 SQLSTATE 08003 （连接未打开）。  
  
 当应用程序调用**SQLConnect**、 **SQLDriverConnect**或**SQLBrowseConnect**时，驱动程序管理器首先确定要使用的驱动程序。 然后，它会检查以确定连接上当前是否加载了驱动程序：  
  
-   如果连接上没有加载驱动程序，则驱动程序管理器会检查是否在同一环境中的另一个连接上加载了指定的驱动程序。 否则，驱动程序管理器会在该连接上加载驱动程序，并在 SQL_HANDLE_ENV 选项的驱动程序中调用**SQLAllocHandle** 。  
  
     然后，驱动程序管理器会将驱动程序中的**SQLAllocHandle**与 SQL_HANDLE_DBC 选项一起调用，无论它是否已加载。 如果应用程序设置了任何连接属性，则驱动程序管理器将在驱动程序中调用**SQLSetConnectAttr** ;如果发生错误，驱动程序管理器的连接函数将返回 SQLSTATE IM006 （驱动程序的**SQLSetConnectAttr**失败）。 最后，驱动程序管理器将调用驱动程序中的连接函数。  
  
-   如果在连接上加载了指定的驱动程序，则驱动程序管理器仅调用驱动程序中的连接函数。 在这种情况下，驱动程序必须确保连接上的所有连接属性都保持其当前设置。  
  
-   如果在连接上加载了不同的驱动程序，驱动程序管理器将在该驱动程序中调用**SQLFreeHandle**以释放该连接。 如果没有其他连接使用该驱动程序，则驱动程序管理器会在该驱动程序中调用**SQLFreeHandle** ，以释放该环境并卸载该驱动程序。 然后，驱动程序管理器执行与连接上未加载驱动程序时相同的操作。  
  
 当*HandleType*设置为**SQL_HANDLE_DBC**时，驱动程序管理器将在调用驱动程序的**SQLAllocHandle**和**SQLFreeHandle**之前锁定环境句柄（*henv*）。  
  
 当应用程序调用**SQLDisconnect**时，驱动程序管理器将在驱动程序中调用**SQLDisconnect** 。 但是，在应用程序重新连接到驱动程序时，它会保留加载的驱动程序。 当应用程序调用带有 SQL_HANDLE_DBC 选项的**SQLFreeHandle**时，驱动程序管理器将在驱动程序中调用**SQLFreeHandle** 。 如果任何其他连接未使用该驱动程序，则驱动程序管理器会使用 SQL_HANDLE_ENV 选项调用该驱动程序中的**SQLFreeHandle**并卸载该驱动程序。
