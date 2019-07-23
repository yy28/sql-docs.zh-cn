---
title: 何时使用适用于 SQL Server 的 OLE DB 驱动程序 | Microsoft Docs
description: 何时使用适用于 SQL Server 的 OLE DB 驱动程序
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], about OLE DB Driver for SQL Server
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 74bd79c24b913cd3c3d2f782b77cf2bb4c23e397
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015185"
---
# <a name="when-to-use-ole-db-driver-for-sql-server"></a>何时使用适用于 SQL Server 的 OLE DB 驱动程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  SQL Server OLE DB 驱动程序是一种可以用来访问[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库中的数据的技术。  有关不同数据访问技术的讨论，请参阅[数据访问技术路线图](https://go.microsoft.com/fwlink/?LinkID=179186)  
  
 在决定是否使用适用于 SQL Server 的 OLE DB 驱动程序作为应用程序的数据访问技术时，应当考虑多种因素。  
  
 对于新的应用程序，如果使用的是托管编程语言，如 Microsoft Visual C# 或 Visual Basic，且需要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的新功能，那么应当使用用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 .NET Framework 数据访问接口，该接口是用于 .NET Framework 的一部分。  
  
 如果要开发基于 COM 的应用程序，且需要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中引入的新功能，则应当使用适用于 SQL Server 的 OLE DB 驱动程序。 如果不需要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的新功能，则可以继续使用 Windows 数据访问组件 (WDAC)。  
  
 对于现有的 OLE DB 应用程序，主要问题在于是否需要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的新功能。 如果已有不需要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的新功能的成熟应用程序，那么可以继续使用 WDAC。 但如果确实需要这些新功能（如 [xml 数据类型](../../t-sql/xml/xml-transact-sql.md)），则应当使用适用于 SQL Server 的 OLE DB 驱动程序。  
  
 SQL Server 和 MDAC OLE DB 驱动程序均支持使用行版本控制的已提交读事务隔离, 但仅 SQL Server 的 OLE DB 驱动程序支持快照事务隔离。 （从编程的角度而言，具有行版本控制的已提交读事务隔离等同于已提交读事务。）  
  
 有关 SQL Server 和 MDAC OLE DB 驱动程序之间的差异的信息, 请参阅[将应用程序更新为从 MDAC SQL Server OLE DB 驱动程序](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)。  
  
## <a name="see-also"></a>另请参阅  
 [适用于 SQL Server 的 OLE DB 驱动程序](../oledb/oledb-driver-for-sql-server.md)     
 [OLE DB 操作指南主题](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
