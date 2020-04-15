---
title: 分配环境句柄 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], environment handles
- allocating environment handles [ODBC]
- connecting to driver [ODBC], environment handles
- environment handles [ODBC]
- data sources [ODBC], environment handles
- connecting to data source [ODBC], environment handles
- handles [ODBC], environment
ms.assetid: 77b5d1d6-7eb7-428d-bf75-a5c5a325d25c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e33b850b2786960a368720deaf89a2203c7dd159
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303000"
---
# <a name="allocating-the-environment-handle"></a>分配环境句柄
任何 ODBC 应用程序的第一个任务是加载驱动程序管理器;如何做到这一点取决于操作系统。 例如，在运行 Microsoft ® Windows NT® 服务器/Windows 2000 服务器、Windows NT 工作站/Windows 2000 专业版或 Microsoft Windows ® 95/98 的计算机上，应用程序要么链接到驱动程序管理器库，要么调用**LoadLibrary**来加载驱动程序管理器 DLL。  
  
 下一个任务，必须在应用程序调用任何其他 ODBC 函数之前完成，是初始化 ODBC 环境并分配环境句柄，如下所示：  
  
1.  应用程序声明 SQLHENV 类型的变量。 然后，它调用**SQLAllocHandle**并传递此变量的地址和SQL_HANDLE_ENV选项。 例如：  
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  驱动程序管理器分配一个结构，用于存储有关环境的信息，并在变量中返回环境句柄。  
  
 驱动程序管理器此时不会在驱动程序中调用**SQLAllocHandle，** 因为它不知道要调用哪个驱动程序。 它会延迟在驱动程序中调用**SQLAllocHandle，** 直到应用程序调用函数以连接到数据源。 有关详细信息，请参阅[驱动程序管理器在连接过程中的角色](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)，请参阅本节后面的部分。  
  
 当应用程序完成使用 ODBC 后，它将使用**SQLFreeHandle**释放环境句柄。 释放环境后，在调用 ODBC 函数时使用环境的句柄是一种应用程序编程错误;这样做有未定义，但可能是致命的后果。  
  
 调用**SQLFreeHandle**时，驱动程序将释放用于存储有关环境的信息的结构。 请注意，在释放该环境句柄上的所有连接句柄之前，无法为环境句柄调用**SQLFreeHandle。**  
  
 有关环境句柄的详细信息，请参阅[环境句柄](../../../odbc/reference/develop-app/environment-handles.md)。
