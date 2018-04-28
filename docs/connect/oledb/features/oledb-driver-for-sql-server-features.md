---
title: 用于 SQL Server 功能的 OLE DB 驱动程序 |Microsoft 文档
description: OLE DB 驱动程序的 SQL Server 功能
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], features
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 66f48a985dd0ddafc6f147c45b3fc3be76f7ec19
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="ole-db-driver-for-sql-server-features"></a>用于 SQL Server 功能的 OLE DB 驱动程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  除了公开功能的 Windows (以前称为 Microsoft) 数据访问组件 (WDAC)，OLE DB 驱动程序的 SQL Server 还实现了许多其他功能来公开[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]功能。  
  
## <a name="in-this-section"></a>本節內容    
 [使用数据库镜像](../../oledb/features/using-database-mirroring.md)  
 讨论如何 OLE DB 驱动程序的 SQL Server 支持是一种功能要保留的副本，或者镜像，镜像数据库，使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]备用服务器上的数据库。  
  
 [执行异步操作](../../oledb/features/performing-asynchronous-operations.md)  
 讨论如何 OLE DB 驱动程序的 SQL Server 支持了异步操作，这是立即返回而不会阻止调用线程上的功能。  
  
 [使用多个活动的结果集 (MARS)](../../oledb/features/using-multiple-active-result-sets-mars.md)  
 讨论 OLE DB 驱动程序的 SQL Server 如何支持多个活动结果集 (MARS)。 MARS 支持使用单一数据库连接执行和接收多个结果集。  
  
 [使用 XML 数据类型](../../oledb/features/using-xml-data-types.md)  
 讨论如何 OLE DB 驱动程序的 SQL Server 支持 XML 数据类型，它是可以用作列类型，变量类型、 参数类型或函数返回类型的基于 XML 的数据类型。  
  
 [使用用户定义的类型](../../oledb/features/using-user-defined-types.md)  
 讨论 OLE DB 驱动程序的 SQL Server 如何支持用户定义类型 (UDT)，它扩展，它允许你存储对象和自定义数据结构中的 SQL 类型系统[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据库。  
  
 [使用较大的值类型](../../oledb/features/using-large-value-types.md)  
 讨论如何 OLE DB 驱动程序的 SQL Server 支持大型值数据类型，它们是大型对象数据类型 (LOB)。  
  
 [以编程方式更改密码](../../oledb/features/changing-passwords-programmatically.md)  
 讨论如何 OLE DB 驱动程序的 SQL Server 支持的密码过期的处理，以便现在可以在无需管理员介入客户端上更改密码。  
  
 [使用快照隔离](../../oledb/features/working-with-snapshot-isolation.md)  
 讨论如何 OLE DB 驱动程序的 SQL Server 支持行版本控制，它通过避免读取器 / 编写器阻塞情况提高数据库性能增强功能。  
  
 [使用查询通知](../../oledb/features/working-with-query-notifications.md)  
 讨论 OLE DB 驱动程序的 SQL Server 如何支持对行集修改的使用者通知。  
  
 [执行大容量复制操作](../../oledb/features/performing-bulk-copy-operations.md)  
 讨论如何 OLE DB 驱动程序的 SQL Server 支持允许的大量数据传输到或外的大容量复制操作[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]表或视图。  
  
 [使用不带验证的加密](../../oledb/features/using-encryption-without-validation.md)  
 讨论如何使用 OLE DB 驱动程序的 SQL Server 来加密数据而无需验证证书发送到服务器。  
  
 [表值参数&#40;用于 SQL Server 的 OLE DB 驱动程序&#41;](../../oledb/features/table-valued-parameters-oledb-driver-for-sql-server.md)  
 For SQL Server 对表值参数支持讨论 OLE DB 驱动程序。  
  
 [大型 CLR 用户定义类型](../../oledb/features/large-clr-user-defined-types.md)  
 讨论对大型公共语言运行时 (CLR) 用户定义类型 (UDT) 的支持。  
  
 [FILESTREAM 支持](../../oledb/features/filestream-support.md)  
 介绍对增强的 FILESTREAM 功能的 SQL Server 支持 OLE DB 驱动程序。  
  
 [服务主体名称&#40;SPN&#41;中客户端连接的支持](../../oledb/features/service-principal-name-spn-support-in-client-connections.md)  
 讨论如何扩展对服务主体名称 (SPN) 的支持，以便能够跨所有协议进行相互身份验证。  
  
 [适用于 SQL Server 的 OLE DB 驱动程序的稀疏列支持](../../oledb/features/sparse-columns-support-in-oledb-driver-for-sql-server.md)  
 对于稀疏列的 SQL Server 支持讨论 OLE DB 驱动程序。  
  
 [日期和时间改进](../../oledb/features/date-and-time-improvements.md)  
 讨论的日期和时间数据类型为 SQL 服务器添加到 OLE DB 驱动程序的支持。  
  
 [元数据发现](../../oledb/features/metadata-discovery.md)  
 讨论对 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中的元数据发现功能进行的改进。  
  
 [适用于 SQL Server 的 OLE DB 驱动程序的 UTF-16 支持](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)  
 讨论 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中引入的行为更改。 如果绑定列结果或输出参数时提供固定长度缓冲区，并且如果**wchar**字符写入到缓冲区之前终止字符是一个高代理项码位的代理项对，并且如果下一步**wchar**字符是一个低代理项码位，OLE DB 驱动程序的 SQL Server 将不向缓冲区添加的高代理项码位。  
  
 [适用于 SQL Server 的 OLE DB 驱动程序对高可用性和灾难恢复的支持](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  
 讨论如何配置你的应用程序以充分利用添加功能的高可用性、 灾难恢复[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]。  
  
 [访问扩展事件日志中的诊断信息](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)  
 讨论 OLE DB 驱动程序用于 SQL Server 和环形缓冲区和 XEvents 日志中的诊断信息使你可以访问的数据跟踪的增强功能。  
  
 [适用于 SQL Server 的 OLE DB 驱动程序对 LocalDB 的支持](../../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)  
 介绍对 LocalDB 功能的 SQL Server 支持 OLE DB 驱动程序。  
  
## <a name="see-also"></a>另请参阅  
 [用于 SQL Server 的 OLE DB 驱动程序](../../oledb/oledb-driver-for-sql-server.md)      
 [OLE DB 操作指南主题](../../oledb/ole-db-how-to/ole-db-how-to-topics.md)   
 [安装适用于 SQL Server 的 OLE DB 驱动程序](../../oledb/applications/installing-oledb-driver-for-sql-server.md)  
  
  
