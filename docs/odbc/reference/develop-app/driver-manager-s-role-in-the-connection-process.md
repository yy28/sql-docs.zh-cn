---
title: 驱动程序管理器&#39;连接过程中的角色 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0227a4063573cb05ecaa9434605ba35f2811bd06
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305798"
---
# <a name="driver-manager39s-role-in-the-connection-process"></a>驱动程序管理器&#39;连接过程中的角色
请记住，应用程序不直接调用驱动程序函数。 相反，它们调用具有相同名称的驱动程序管理器函数，驱动程序管理器调用驱动程序函数。 通常，这种情况几乎立即发生。 例如，应用程序在驱动程序管理器中调用**SQLExecute，** 在进行几次错误检查后，驱动程序管理器在驱动程序中调用**SQLExecute。**  
  
 连接过程不同。 当应用程序使用SQL_HANDLE_ENV和SQL_HANDLE_DBC选项调用**SQLAllocHandle**时，该函数仅在驱动程序管理器中分配句柄。 驱动程序管理器不会在驱动程序中调用此函数，因为它不知道要调用哪个驱动程序。 同样，如果应用程序将未连接的连接的句柄传递给**SQLSetConnectAttr**或**SQLGetConnectAttr，** 则只有驱动程序管理器执行该函数。 它存储或获取其连接句柄的属性值，并在获取尚未设置且 ODBC 未为其定义默认值的属性的值时返回 SQLSTATE 08003（连接未打开）。  
  
 当应用程序调用**SQLConnect** **、SQLDriverConnect**或**SQLBrowseConnect**时，驱动程序管理器首先确定要使用的驱动程序。 然后，它会检查以确定当前是否在连接上加载了驱动程序：  
  
-   如果连接上未加载驱动程序，则驱动程序管理器将检查指定驱动程序是否在同一环境中的另一个连接上加载。 如果没有，驱动程序管理器将驱动程序加载到连接上，并在驱动程序中使用SQL_HANDLE_ENV选项调用**SQLAllocHandle。**  
  
     然后，驱动程序管理器在驱动程序中使用SQL_HANDLE_DBC选项调用**SQLAllocHandle，** 无论是否刚刚加载。 如果应用程序设置了任何连接属性，驱动程序管理器在驱动程序中调用**SQLSetConnectAttr;如果驱动程序中调用 SQLSetConnectAttr;如果驱动程序中调用 SQLSetConnectAttr，则驱动程序将调用 SQLSetConnectAttr。** 如果发生错误，驱动程序管理器的连接函数将返回 SQLSTATE IM006（驱动程序的**SQLSetConnectAttr**失败）。 最后，驱动程序管理器调用驱动程序中的连接函数。  
  
-   如果在连接上加载了指定的驱动程序，则驱动程序管理器仅调用驱动程序中的连接功能。 在这种情况下，驱动程序必须确保连接上的所有连接属性都保持其当前设置。  
  
-   如果连接上加载了其他驱动程序，驱动程序管理器会调用驱动程序中的**SQLFreeHandle**以释放连接。 如果没有使用驱动程序的其他连接，驱动程序管理器在驱动程序中调用**SQLFreeHandle**以释放环境并卸载驱动程序。 然后，驱动程序管理器执行与未在连接上加载驱动程序时相同的操作。  
  
 当*HandleType*设置为**SQL_HANDLE_DBC**时，驱动程序管理器将锁定环境句柄 *（henv），* 然后再调用驱动程序的**SQLAllocHandle**和**SQLFreeHandle。**  
  
 当应用程序调用**SQLDISCONNECT**时，驱动程序管理器在驱动程序中调用**SQLDISCONNECT。** 但是，它会在应用程序重新连接到驱动程序的情况下加载驱动程序。 当应用程序使用SQL_HANDLE_DBC选项调用**SQLFreeHandle**时，驱动程序管理器在驱动程序中调用**SQLFreeHandle。** 如果驱动程序未被任何其他连接使用，则驱动程序管理器然后在驱动程序中调用**SQLFreeHandle，** 并带有SQL_HANDLE_ENV选项并卸载驱动程序。
