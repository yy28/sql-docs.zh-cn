---
title: SQL Server 的 OLE DB 驱动程序支持策略 |Microsoft 文档
description: 对 SQL Server OLE DB 驱动程序支持策略
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: dfac5b5acd86c71787e3ee5052927d7d59969f8b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>用于 SQL Server 的 OLE DB 驱动程序的支持策略
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  本文讨论了各种数据访问组件可以使用 OLE DB 驱动程序用于针对 SQL Server。  

## <a name="server-support"></a>服务器支持  
 OLE DB 驱动程序的 SQL Server 支持连接到[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]， [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]，[!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)]， [!INCLUDE[ssSQL17](../../../includes/sssql17-md.md)]，和[!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]。

## <a name="supported-operating-system-versions"></a>支持的操作系统版本  
 下表列出了 SQL Server 哪些操作系统支持 OLE DB 驱动程序。  

|支持的操作系统|  
|--------------------------------------|---------------------------------|   
|Microsoft Windows 8.1<br /><br />Microsoft Windows 10<br /><br /> Microsoft Windows Server 2012<br /><br />Microsoft Windows Server 2012 R2<br /><br />Microsoft Windows Server 2016|  

## <a name="ado-support-policies"></a>ADO 支持策略  
 ADO 应用程序如果不需要 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更高版本的任何功能，则可以使用 Windows 附带的 SQLOLEDB OLE DB 访问接口。  

 ADO 应用程序可以使用的 SQL Server 的 OLE DB 驱动程序，但如果它们在这样做它们必须指定`DataTypeCompatibility=80`的连接字符串中。 如果连接字符串中包含 `DataTypeCompatibility=80`，则只能使用 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的功能。  

## <a name="ole-db-support-policies"></a>OLE DB 支持策略  
应用程序可以使用 Windows 操作系统中包含的 OLE DB 访问接口 (SQLOLEDB)。 但是，这是在维护模式下，无法再更新。 您应改用 OLE DB 驱动程序的 SQL Server (MSOLEDBSQL)。

## <a name="see-also"></a>另请参阅  
 [使用适用于 SQL Server 的 OLE DB 驱动程序生成应用程序](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
