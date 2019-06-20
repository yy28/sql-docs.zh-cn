---
title: 断开与数据源的连接 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC data sources, connections
- data sources [SQL Server Native Client]
- disconnecting [ODBC]
- ODBC applications, disconnecting
- SQLDisconnect function
- ODBC applications, data sources
- connections [SQL Server Native Client]
- SQLFreeHandle function
- ODBC data sources, disconnecting
- SQL Server Native Client ODBC driver, data sources
- ODBC functions
- SQL Server Native Client ODBC driver, connections
ms.assetid: 65b0267d-b2ab-4a59-83f2-436d90cfbf79
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 43ccc784d0d8759c559e705cbbb65861040f6e8a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63205677"
---
# <a name="disconnecting-from-a-data-source"></a>与数据源断开连接
  当应用程序使用完数据源时，它将调用**SQLDisconnect**。 **SQLDisconnect**释放在连接分配任何语句，并与数据源断开连接，驱动程序。 断开连接后，应用程序可以调用[SQLFreeHandle](../native-client-odbc-api/sqlfreehandle.md)以释放连接句柄。 退出之前，应用程序还调用**SQLFreeHandle**以释放环境句柄。  
  
 断开连接后，应用程序可以重用分配的连接句柄，以连接到其他数据源或重新连接到同一个数据源。 如果决定保持连接，而不是断开连接后重新连接，则要求应用程序编写人员考虑每种选择的相对成本。 连接到数据源并保持连接状态的开销可能相对较大，具体取决于连接介质。 权衡利弊时，应用程序还必须就同一数据源上存在其他操作的可能性以及这些操作的时间安排情况做出假设。 应用程序可能还必须使用多个连接。  
  
## <a name="see-also"></a>请参阅  
 [与 SQL Server 通信&#40;ODBC&#41;](communicating-with-sql-server-odbc.md)  
  
  
