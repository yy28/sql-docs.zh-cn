---
title: "分配连接句柄 ODBC |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- allocating connection handles [ODBC]
- data sources [ODBC], connection handles
- connecting to data source [ODBC], connection handles
- ODBC drivers [ODBC], connection handles
- connecting to driver [ODBC], connection handles
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: c99a8159-7693-4f97-8dcf-401336550e77
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 678ba0fa4e256402e9fc25e2e4e60ba4877c6c44
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="allocating-a-connection-handle-odbc"></a>分配 ODBC 连接句柄
应用程序可以连接到数据源或驱动程序，它必须先分配然后连接句柄，如下所示：  
  
1.  应用程序声明类型 SQLHDBC 的变量。 然后，它调用**SQLAllocHandle**并将传递此变量，在其中分配连接和 SQL_HANDLE_DBC 选项的环境的句柄的地址。 例如：  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  驱动程序管理器分配要在其中存储有关语句的信息的结构，并在变量中返回连接句柄。  
  
 驱动程序管理器不会调用**SQLAllocHandle**在驱动程序在此时间，因为它不知道要调用的驱动程序。 会延迟调用**SQLAllocHandle**驱动程序，直到应用程序调用一个函数来连接到数据源中。 有关详细信息，请参阅[连接过程中的驱动程序管理器角色](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)，本部分中更高版本。  
  
 请务必注意，分配连接句柄不相同加载驱动程序。 不，直到连接函数调用，将加载驱动程序。 因此，分配连接句柄并后连接到该驱动程序或数据源之前，应用程序可以调用与连接句柄的唯一函数是**SQLSetConnectAttr**， **SQLGetConnectAttr**，或**SQLGetInfo** SQL_ODBC_VER 选项。 调用其他函数与连接句柄，例如**SQLEndTran**，返回 SQLSTATE 08003 （连接未打开）。 有关完整详细信息，请参阅[附录 b: ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 有关连接句柄的详细信息，请参阅[连接句柄](../../../odbc/reference/develop-app/connection-handles.md)。
