---
title: "驱动程序管理器 &#39; s 角色在连接过程 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- driver manager [ODBC], role in connection process
- connecting to data source [ODBC], driver manager
- connecting to driver [ODBC], driver manager
- ODBC driver manager [ODBC]
ms.assetid: 77c05630-5a8b-467d-b80e-c705dc06d601
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 32a6629892ad9667b7d56a6bb6752c68001dddc9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="driver-manager39s-role-in-the-connection-process"></a>驱动程序管理器 &#39; s 连接过程中的角色
请记住，应用程序请勿直接调用驱动程序函数。 相反，这些驱动程序管理器具有相同名称的函数调用，驱动程序管理器调用驱动程序函数。 通常情况下，发生这种情况几乎立即。 例如，在应用程序调用**SQLExecute**驱动程序管理器中之后，一些错误检查，驱动程序管理器调用**SQLExecute**驱动程序中。  
  
 在连接过程是不同的。 在应用程序调用**SQLAllocHandle**使用 SQL_HANDLE_ENV 和 SQL_HANDLE_DBC 选项，该函数分配句柄仅在驱动程序管理器。 驱动程序管理器不调用此函数在驱动程序中的，因为它不知道要调用的驱动程序。 同样，如果应用程序将传递一个未连接到连接的句柄**SQLSetConnectAttr**或**SQLGetConnectAttr**、 只驱动程序管理器执行的函数。 它将存储或从其连接的属性值处理和返回尚未设置的属性获取的值和适用于哪些 ODBC 的 SQLSTATE 08003 （连接未打开），获取未定义默认值。  
  
 在应用程序调用**SQLConnect**， **SQLDriverConnect**，或**SQLBrowseConnect**，驱动程序管理器首先确定要使用的驱动程序。 然后，它检查以确定是否当前连接上加载某个驱动程序：  
  
-   如果在连接上不加载了任何驱动程序，驱动程序管理器检查是否在同一环境中的另一个连接上加载指定的驱动程序。 如果不是，驱动程序管理器将加载连接并调用上的驱动程序**SQLAllocHandle** SQL_HANDLE_ENV 选项与驱动程序中。  
  
     驱动程序管理器然后调用**SQLAllocHandle**在使用 SQL_HANDLE_DBC 选项驱动程序，是否这是刚加载。 如果应用程序设置任何连接属性，驱动程序管理器调用**SQLSetConnectAttr**在驱动程序; 如果发生错误，驱动程序管理器的连接函数返回 SQLSTATE IM006 (驱动程序的**SQLSetConnectAttr**失败)。 最后，驱动程序管理器驱动程序中调用连接函数。  
  
-   如果在连接上加载了指定的驱动程序，驱动程序管理器驱动程序中调用仅连接函数。 在这种情况下，该驱动程序必须确保连接上的所有连接属性都维护其当前设置。  
  
-   如果在连接上加载了不同的驱动程序，驱动程序管理器调用**SQLFreeHandle**驱动程序以释放连接中。 如果不没有使用的驱动程序的任何其他连接，驱动程序管理器调用**SQLFreeHandle**驱动程序以释放该环境中和卸载该驱动程序。 驱动程序管理器然后执行与连接上时不加载某个驱动程序相同的操作。  
  
 驱动程序管理器将会锁定环境句柄 (*henv*) 在调用驾之前**SQLAllocHandle**和**SQLFreeHandle**时*HandleType*设置为**SQL_HANDLE_DBC**。  
  
 在应用程序调用**SQLDisconnect**，驱动程序管理器调用**SQLDisconnect**驱动程序中。 但是，它留在应用程序重新连接到该驱动程序的情况下加载的驱动程序。 在应用程序调用**SQLFreeHandle**使用 SQL_HANDLE_DBC 选项时，驱动程序管理器调用**SQLFreeHandle**驱动程序中。 如果任何其他连接不使用该驱动程序，然后调用驱动程序管理器**SQLFreeHandle**中与 SQL_HANDLE_ENV 驱动程序选项和卸载该驱动程序。

