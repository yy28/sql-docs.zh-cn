---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 83964bf1e76eef5c7c4ba4121b0c581e8d8a406b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63288319"
---
# <a name="allocating-a-connection-handle-odbc"></a>分配连接句柄 ODBC
应用程序可以连接到数据源或驱动程序之前，必须分配连接句柄，按如下所示：  
  
1.  应用程序声明类型 SQLHDBC 的变量。 然后，它调用**SQLAllocHandle** ，并将传递此变量，用来将该连接和 SQL_HANDLE_DBC 选项分配环境句柄的地址。 例如：  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  驱动程序管理器分配要在其中存储有关语句的信息的结构，并在变量中返回的连接句柄。  
  
 驱动程序管理器不会调用**SQLAllocHandle**此驱动程序中的时间，因为它不知道要调用的驱动程序。 它会调用延迟**SQLAllocHandle**驱动程序直到应用程序调用一个函数来连接到数据源中。 有关详细信息，请参阅[的连接过程中的驱动程序管理器角色](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)稍后在本部分中。  
  
 请务必注意，分配连接句柄并不相同加载驱动程序。 连接函数调用之前，未加载该驱动程序。 因此后分配连接句柄, 并连接到的驱动程序或数据源之前，应用程序可以调用与连接句柄的唯一函数是**SQLSetConnectAttr**， **SQLGetConnectAttr**，或**SQLGetInfo** SQL_ODBC_VER 选项。 调用其他函数与连接句柄，例如**SQLEndTran**，返回的 SQLSTATE 08003 （连接未打开）。 有关完整详细信息，请参阅[附录 b:状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 有关连接句柄的详细信息，请参阅[连接句柄](../../../odbc/reference/develop-app/connection-handles.md)。
