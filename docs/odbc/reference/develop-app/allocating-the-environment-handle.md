---
title: 分配的环境句柄 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC drivers [ODBC], environment handles
- allocating environment handles [ODBC]
- connecting to driver [ODBC], environment handles
- environment handles [ODBC]
- data sources [ODBC], environment handles
- connecting to data source [ODBC], environment handles
- handles [ODBC], environment
ms.assetid: 77b5d1d6-7eb7-428d-bf75-a5c5a325d25c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bcbfc5e9a8be2bf1fc543e9d458658a918e40b6d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="allocating-the-environment-handle"></a>分配的环境句柄
任何 ODBC 应用程序的第一个任务是加载驱动程序管理器;如何做到这一点与操作系统相关。 例如，在运行 Microsoft® Windows NT® Server/Windows 2000 Server、 Windows NT 工作站/Windows 2000 Professional 或 Microsoft Windows® 95/98 的计算机，在应用程序或者链接到驱动程序管理器库或调用**LoadLibrary**加载驱动程序管理器 DLL。  
  
 下一个任务，必须先完成应用程序可以调用任何其他 ODBC 函数，是初始化 ODBC 环境并分配环境句柄，，如下所示：  
  
1.  应用程序声明类型 SQLHENV 的变量。 然后，它调用**SQLAllocHandle**并将传递此变量和 SQL_HANDLE_ENV 选项的地址。 例如：  
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  驱动程序管理器分配要在其中存储有关的环境的信息的结构，并在变量中返回的环境句柄。  
  
 驱动程序管理器不会调用**SQLAllocHandle**在驱动程序在此时间，因为它不知道要调用的驱动程序。 会延迟调用**SQLAllocHandle**驱动程序，直到应用程序调用一个函数来连接到数据源中。 有关详细信息，请参阅[连接过程中的驱动程序管理器角色](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)，本部分中更高版本。  
  
 完成后使用 ODBC 的应用程序，它会释放使用的环境句柄**SQLFreeHandle**。 后释放环境，它是对应用程序编程错误对 ODBC 函数; 的调用中使用环境的句柄因此，这样做具有未定义，但可能严重后果。  
  
 当**SQLFreeHandle**调用，用于存储有关的环境信息结构的驱动程序版本。 请注意， **SQLFreeHandle**被释放该环境句柄上的所有连接句柄之后不能为环境句柄之前调用。  
  
 有关环境句柄的详细信息，请参阅[环境处理](../../../odbc/reference/develop-app/environment-handles.md)。
