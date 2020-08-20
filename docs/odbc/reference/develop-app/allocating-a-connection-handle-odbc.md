---
description: 分配连接句柄 ODBC
title: 分配连接句柄 ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- allocating connection handles [ODBC]
- data sources [ODBC], connection handles
- connecting to data source [ODBC], connection handles
- ODBC drivers [ODBC], connection handles
- connecting to driver [ODBC], connection handles
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: c99a8159-7693-4f97-8dcf-401336550e77
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6c17003ed3746f2953eb167f2dc3d944659e352
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456433"
---
# <a name="allocating-a-connection-handle-odbc"></a>分配连接句柄 ODBC
在应用程序可以连接到数据源或驱动程序之前，必须分配连接句柄，如下所示：  
  
1.  应用程序声明类型为 SQLHDBC 的变量。 然后，它调用 **SQLAllocHandle** 并传递此变量的地址、要在其中分配连接的环境的句柄和 SQL_HANDLE_DBC 选项。 例如：  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  驱动程序管理器分配一个结构，在该结构中存储有关语句的信息并返回变量中的连接句柄。  
  
 目前，驱动程序管理器不会调用驱动程序中的 **SQLAllocHandle** ，因为它不知道要调用哪个驱动程序。 在应用程序调用函数以连接到数据源之前，它会延迟在驱动程序中调用 **SQLAllocHandle** 。 有关详细信息，请参阅本部分后面的 [连接过程中的驱动程序管理器角色](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)。  
  
 需要特别注意的是，分配连接句柄不同于加载驱动程序。 在调用连接函数之前，不会加载驱动程序。 因此，在分配连接句柄之后，在连接到驱动程序或数据源之前，应用程序可以使用连接句柄调用的唯一函数是 **SQLSetConnectAttr**、 **SQLGetConnectAttr**或 **SQLGetInfo** 与 SQL_ODBC_VER 选项。 通过连接句柄调用其他函数（如 **SQLEndTran**）将返回 SQLSTATE 08003 (连接未打开) 。 有关完整的详细信息，请参阅 [附录 B： ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 有关连接句柄的详细信息，请参阅 [连接句柄](../../../odbc/reference/develop-app/connection-handles.md)。
