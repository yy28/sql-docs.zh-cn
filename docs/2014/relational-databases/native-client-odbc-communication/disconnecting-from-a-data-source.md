---
title: 从数据源断开连接 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 93afdf5c897525d0b3e925736e763f3da066941e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017318"
---
# <a name="disconnecting-from-a-data-source"></a>与数据源断开连接
  当应用程序已完成将数据源使用时，它将调用**SQLDisconnect**。 **SQLDisconnect**释放连接分配的所有语句并将驱动程序与数据源断开连接。 断开连接之后，应用程序可以调用[SQLFreeHandle](../native-client-odbc-api/sqlfreehandle.md)释放连接句柄。 在退出之前, 应用程序还调用**SQLFreeHandle**释放环境句柄。  
  
 断开连接后，应用程序可以重用分配的连接句柄，以连接到其他数据源或重新连接到同一个数据源。 如果决定保持连接，而不是断开连接后重新连接，则要求应用程序编写人员考虑每种选择的相对成本。 连接到数据源并保持连接状态的开销可能相对较大，具体取决于连接介质。 权衡利弊时，应用程序还必须就同一数据源上存在其他操作的可能性以及这些操作的时间安排情况做出假设。 应用程序可能还必须使用多个连接。  
  
## <a name="see-also"></a>请参阅  
 [与 SQL Server 通信&#40;ODBC&#41;](communicating-with-sql-server-odbc.md)  
  
  