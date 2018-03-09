---
title: "分配连接句柄 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-communication
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ODBC applications, passwords
- ODBC applications, connections
- handles [SQL Server Native Client]
- expiration [SQL Server Native Client]
- passwords [SQL Server], modifying
- SQL Server Native Client ODBC driver, connection handles
- connection handles [SQL Server Native Client]
- modifying passwords
- SQLAllocHandle function
ms.assetid: 471d8a31-199c-4f92-bb10-004fc7733b35
caps.latest.revision: "32"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2046fc4df80ba780e7ab16948105ef0aebb1e84c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="allocating-a-connection-handle"></a>分配连接句柄
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  应用程序可以连接到数据源或驱动程序之前，必须分配连接句柄。 这可通过调用**SQLAllocHandle**与*HandleType*参数设置为 SQL_HANDLE_DBC 和*InputHandle*指向初始化的环境句柄。  
  
 连接的特征通过设置连接属性控制。 例如，因为事务发生在连接级别，所以事务隔离级别就是一个连接属性。 与此类似，登录超时或超时前尝试连接的等待秒数，也是连接属性。  
  
 连接属性设置与[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)，与检索它们的当前设置，而不对[SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)。 如果**SQLSetConnectAttr**是调用之前将尝试进行连接，ODBC 驱动程序管理器将属性存储在其连接结构并将这些驱动程序中设置连接过程的一部分。 有些连接属性必须在应用程序尝试连接前设置，另一些则可以在连接完成之后设置。 例如，SQL_ATTR_ODBC_CURSORS 必须在连接前设置，但 SQL_ATTR_AUTOCOMMIT 可以在连接后设置。  
  
 针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 或更高版本运行的应用程序，可以通过重置表格格式数据流 (TDS) 网络数据包大小，改善它们的性能。 服务器上设置的默认数据包大小为 4 KB。 一般来说，数据包大小介于 4 KB 到 8 KB 之间时表现出的性能最佳。 如果测试表明采用另一数据包大小时，应用程序的性能表现更佳，则可以重置数据包大小。 ODBC 应用程序可以执行此操作通过调用连接之前**SQLSetConnectAttr** SQL_ATTR_PACKET_SIZE 选项。 有些应用程序在使用较大的数据包时表现更佳，但数据包大小大于 8 KB 时，性能鲜有提高。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序都有大量的应用程序可以使用它来提高其功能的扩展的连接属性。 在这些属性当中，有些控制可以在数据源中指定的相同选项，并覆盖数据源中设置的任何选项。 例如，如果应用程序使用带引号的标识符，它可以将特定于驱动程序的属性 SQL_COPT_SS_QUOTED_IDENT 设置为 SQL_QI_ON，确保无论数据源中如何设置，该选项始终这样设置。  
  
## <a name="see-also"></a>另请参阅  
 [通信使用 SQL Server &#40; ODBC &#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
