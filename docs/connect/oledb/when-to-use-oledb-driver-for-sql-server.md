---
title: 何时使用用于 SQL Server 的 OLE DB 驱动程序 |Microsoft 文档
description: 何时使用用于 SQL Server 的 OLE DB 驱动程序
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], about OLE DB Driver for SQL Server
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: ec0fe6779f236e1d244f2768f787c59ae5a31271
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="when-to-use-ole-db-driver-for-sql-server"></a>何时使用用于 SQL Server 的 OLE DB 驱动程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  OLE DB 驱动程序的 SQL Server 是一个可用于访问中的数据的技术[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。  有关不同的数据访问技术的讨论，请参阅[数据访问技术路线图](http://go.microsoft.com/fwlink/?LinkID=179186)  
  
 在决定是否要作为数据访问技术的应用程序中使用 SQL Server 的 OLE DB 驱动程序时，应考虑以下几个因素。  
  
 对于新的应用程序，如果使用的是托管编程语言，如 Microsoft Visual C# 或 Visual Basic，且需要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的新功能，那么应当使用用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 .NET Framework 数据访问接口，该接口是用于 .NET Framework 的一部分。  
  
 如果你正在开发的基于 COM 的应用程序且需要访问中引入的新功能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，应使用用于 SQL Server 的 OLE DB 驱动程序。 如果不需要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的新功能，则可以继续使用 Windows 数据访问组件 (WDAC)。  
  
 对于现有的 OLE DB 应用程序，主要问题是你是否需要访问的新功能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果已有不需要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的新功能的成熟应用程序，那么可以继续使用 WDAC。 但是，如果你需要访问这些新功能，例如[xml 数据类型](../../t-sql/xml/xml-transact-sql.md)，应使用用于 SQL Server 的 OLE DB 驱动程序。  
  
 针对 SQL Server 和 MDAC 支持这两个 OLE DB 驱动程序读取已提交的事务隔离对 SQL Server 支持快照事务隔离使用行版本控制，但仅 OLE DB 驱动程序。 （在编程术语中，使用行版本控制的读取已提交的事务隔离是 Read Committed 事务相同。）  
  
 有关 OLE DB 驱动程序的 SQL Server 和 MDAC 之间的差异的信息，请参阅[更新为 OLE DB 驱动程序的应用程序适用于 SQL Server 从 MDAC](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)。  
  
## <a name="see-also"></a>另请参阅  
 [用于 SQL Server 的 OLE DB 驱动程序](../oledb/oledb-driver-for-sql-server.md)     
 [OLE DB 操作指南主题](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
