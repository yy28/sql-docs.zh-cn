---
title: 分配连接句柄 ODBC |微软文档
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
ms.openlocfilehash: 12e9f65ee81612e269c1f86ebabd049588443cb8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288517"
---
# <a name="allocating-a-connection-handle-odbc"></a>分配连接句柄 ODBC
在应用程序可以连接到数据源或驱动程序之前，它必须分配连接句柄，如下所示：  
  
1.  应用程序声明 SQLHDBC 类型的变量。 然后，它调用**SQLAllocHandle**并传递此变量的地址、要分配连接的环境的句柄以及SQL_HANDLE_DBC选项。 例如：  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  驱动程序管理器分配一个结构，用于存储有关语句的信息并在变量中返回连接句柄。  
  
 驱动程序管理器此时不会在驱动程序中调用**SQLAllocHandle，** 因为它不知道要调用哪个驱动程序。 它会延迟在驱动程序中调用**SQLAllocHandle，** 直到应用程序调用函数以连接到数据源。 有关详细信息，请参阅[驱动程序管理器在连接过程中的角色](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)，请参阅本节后面的部分。  
  
 请务必注意，分配连接句柄与加载驱动程序不同。 在调用连接函数之前，不会加载驱动程序。 因此，在分配连接句柄后，在连接到驱动程序或数据源之前，应用程序可以使用连接句柄调用的唯一函数是**SQLSetConnectAttr、SQLGetConnectAttr**或**SQLGetInfo，** 带有SQL_ODBC_VER选项。 **SQLGetConnectAttr** 使用连接句柄调用其他函数（如**SQLEndTran**）返回 SQLSTATE 08003（连接未打开）。 有关完整详细信息，请参阅[附录 B：ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 有关连接句柄的详细信息，请参阅[连接句柄](../../../odbc/reference/develop-app/connection-handles.md)。
