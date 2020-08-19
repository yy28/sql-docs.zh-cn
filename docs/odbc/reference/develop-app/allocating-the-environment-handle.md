---
description: 分配环境句柄
title: 分配环境句柄 |Microsoft Docs
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
ms.openlocfilehash: 390d7f4248d43e6fc6cb7910be5f42cb286f37e9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429449"
---
# <a name="allocating-the-environment-handle"></a>分配环境句柄
任何 ODBC 应用程序的第一个任务是加载驱动程序管理器;完成此操作的方式取决于操作系统。 例如，在运行 Microsoft® Windows NT® Server/Windows 2000 Server、Windows NT 工作站/Windows 2000 Professional 或 Microsoft Windows®95/98 的计算机上，应用程序将链接到驱动程序管理器库，或调用 **LoadLibrary** 以加载驱动程序管理器 DLL。  
  
 在应用程序可以调用任何其他 ODBC 函数之前，必须执行的下一个任务是初始化 ODBC 环境并分配环境句柄，如下所示：  
  
1.  应用程序声明类型为 SQLHENV 的变量。 然后，它调用 **SQLAllocHandle** 并传递此变量的地址和 SQL_HANDLE_ENV 选项。 例如：  
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  驱动程序管理器分配用于存储有关环境的信息的结构，并返回变量中的环境句柄。  
  
 目前，驱动程序管理器不会调用驱动程序中的 **SQLAllocHandle** ，因为它不知道要调用哪个驱动程序。 在应用程序调用函数以连接到数据源之前，它会延迟在驱动程序中调用 **SQLAllocHandle** 。 有关详细信息，请参阅本部分后面的 [连接过程中的驱动程序管理器角色](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)。  
  
 当应用程序使用完 ODBC 后，就可以使用 **SQLFreeHandle**释放环境句柄。 释放环境后，在对 ODBC 函数的调用中使用环境的句柄时，会出现应用程序编程错误;这样做没有定义，但可能会产生严重后果。  
  
 调用 **SQLFreeHandle** 时，驱动程序将释放用于存储有关环境的信息的结构。 请注意，只有在释放了该环境句柄上的所有连接句柄之后，才能为环境句柄调用 **SQLFreeHandle** 。  
  
 有关环境句柄的详细信息，请参阅 [环境句柄](../../../odbc/reference/develop-app/environment-handles.md)。
