---
title: 分配连接句柄 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cfda8d23f3be8b37f9eb3876496394fc32660769
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702069"
---
# <a name="allocating-a-connection-handle"></a>分配连接句柄
  应用程序可以连接到数据源或驱动程序之前，必须分配连接句柄。 这是通过调用**SQLAllocHandle**并将*HandleType*参数设置为 SQL_HANDLE_DBC，并将*将 inputhandle*指向已初始化的环境句柄来完成的。  
  
 连接的特征通过设置连接属性控制。 例如，因为事务发生在连接级别，所以事务隔离级别就是一个连接属性。 与此类似，登录超时或超时前尝试连接的等待秒数，也是连接属性。  
  
 连接属性是通过[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md)设置的，其当前设置是通过[SQLGetConnectAttr](../native-client-odbc-api/sqlgetconnectattr.md)检索的。 如果在尝试连接之前调用**SQLSetConnectAttr** ，ODBC 驱动程序管理器会将属性存储在其连接结构中，并在该驱动程序中将它们设置为连接过程的一部分。 有些连接属性必须在应用程序尝试连接前设置，另一些则可以在连接完成之后设置。 例如，SQL_ATTR_ODBC_CURSORS 必须在连接前设置，但 SQL_ATTR_AUTOCOMMIT 可以在连接后设置。  
  
 针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 或更高版本运行的应用程序，可以通过重置表格格式数据流 (TDS) 网络数据包大小，改善它们的性能。 服务器上设置的默认数据包大小为 4 KB。 一般来说，数据包大小介于 4 KB 到 8 KB 之间时表现出的性能最佳。 如果测试表明采用另一数据包大小时，应用程序的性能表现更佳，则可以重置数据包大小。 ODBC 应用程序可以通过使用 SQL_ATTR_PACKET_SIZE 选项调用**SQLSetConnectAttr**来进行连接。 有些应用程序在使用较大的数据包时表现更佳，但数据包大小大于 8 KB 时，性能鲜有提高。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驱动程序具有许多扩展连接属性，应用程序可以使用这些属性来增加其功能。 在这些属性当中，有些控制可以在数据源中指定的相同选项，并覆盖数据源中设置的任何选项。 例如，如果应用程序使用带引号的标识符，它可以将特定于驱动程序的属性 SQL_COPT_SS_QUOTED_IDENT 设置为 SQL_QI_ON，确保无论数据源中如何设置，该选项始终这样设置。  
  
## <a name="see-also"></a>另请参阅  
 [与 SQL Server &#40;ODBC&#41;通信](communicating-with-sql-server-odbc.md)  
  
  
