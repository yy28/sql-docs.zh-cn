---
title: 分配连接句柄 |微软文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9c88b8cfb74f9ce91b98fa078cbff6a550e1a015
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307750"
---
# <a name="allocating-a-connection-handle"></a>分配连接句柄
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  应用程序可以连接到数据源或驱动程序之前，必须分配连接句柄。 这是通过将*处理类型*参数设置为SQL_HANDLE_DBC调用**SQLAllocHandle**和*InputHandle*以指向初始化环境句柄来实现的。  
  
 连接的特征通过设置连接属性控制。 例如，因为事务发生在连接级别，所以事务隔离级别就是一个连接属性。 与此类似，登录超时或超时前尝试连接的等待秒数，也是连接属性。  
  
 连接属性使用[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)设置，并且其当前设置使用[SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)检索。 如果在尝试连接之前调用**SQLSetConnectAttr，** 则 ODBC 驱动程序管理器将属性存储在其连接结构中，并将其设置为驱动程序中的连接过程的一部分。 有些连接属性必须在应用程序尝试连接前设置，另一些则可以在连接完成之后设置。 例如，SQL_ATTR_ODBC_CURSORS 必须在连接前设置，但 SQL_ATTR_AUTOCOMMIT 可以在连接后设置。  
  
 针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 或更高版本运行的应用程序，可以通过重置表格格式数据流 (TDS) 网络数据包大小，改善它们的性能。 服务器上设置的默认数据包大小为 4 KB。 一般来说，数据包大小介于 4 KB 到 8 KB 之间时表现出的性能最佳。 如果测试表明采用另一数据包大小时，应用程序的性能表现更佳，则可以重置数据包大小。 ODBC 应用程序可以通过使用SQL_ATTR_PACKET_SIZE选项调用**SQLSetConnectAttr**来连接之前执行此操作。 有些应用程序在使用较大的数据包时表现更佳，但数据包大小大于 8 KB 时，性能鲜有提高。  
  
 本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 ODBC 驱动程序具有许多扩展连接属性，应用程序可以使用这些属性来增加其功能。 在这些属性当中，有些控制可以在数据源中指定的相同选项，并覆盖数据源中设置的任何选项。 例如，如果应用程序使用带引号的标识符，它可以将特定于驱动程序的属性 SQL_COPT_SS_QUOTED_IDENT 设置为 SQL_QI_ON，确保无论数据源中如何设置，该选项始终这样设置。  
  
## <a name="see-also"></a>另请参阅  
 [与 SQL 服务器通信 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
