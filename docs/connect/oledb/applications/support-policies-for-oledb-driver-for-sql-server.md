---
title: 适用于 SQL Server 的 OLE DB 驱动程序的支持策略 | Microsoft Docs
description: 适用于 SQL Server 的 OLE DB 驱动程序的支持策略
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.custom: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 782745fa9957cd611aa875bec2f9b740b489f210
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53202006"
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>适用于 SQL Server 的 OLE DB 驱动程序的支持策略
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  本文介绍了各种数据访问组件可以与 OLE DB 驱动程序使用适用于 SQL Server。  

## <a name="server-support"></a>服务器支持  
 OLE DB Driver for SQL Server 支持连接到[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]， [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]， [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)]， [!INCLUDE[ssSQL17](../../../includes/sssql17-md.md)]，和[!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]。

## <a name="supported-operating-system-versions"></a>支持的操作系统版本  
 下表列出了 SQL Server 的操作系统支持 OLE DB 驱动程序。  

|受支持的操作系统|  
|--------------------------------------|---------------------------------|   
|Microsoft Windows 8.1<br /><br />Microsoft Windows 10<br /><br /> Microsoft Windows Server 2012<br /><br />Microsoft Windows Server 2012 R2<br /><br />Microsoft Windows Server 2016|  

## <a name="ado-support-policies"></a>ADO 支持策略  
 ADO 应用程序如果不需要 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更高版本的任何功能，则可以使用 Windows 附带的 SQLOLEDB OLE DB 访问接口。  

 ADO 应用程序可以使用 SQL Server 的 OLE DB 驱动程序，但如果用户这样做它们必须指定`DataTypeCompatibility=80`在连接字符串中。 如果连接字符串中包含 `DataTypeCompatibility=80`，则只能使用 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的功能。  

## <a name="ole-db-support-policies"></a>OLE DB 支持策略  
应用程序可使用随 Windows 操作系统附带的 OLE DB 提供程序 (SQLOLEDB)。 但是，这是在维护模式下，不再更新。 您应改用 OLE DB 驱动程序的 SQL Server (MSOLEDBSQL)。

## <a name="see-also"></a>另请参阅  
 [使用适用于 SQL Server 的 OLE DB 驱动程序生成应用程序](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
