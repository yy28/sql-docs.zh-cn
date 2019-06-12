---
title: 适用于 SQL Server 的 OLE DB 驱动程序的支持策略 | Microsoft Docs
description: 适用于 SQL Server 的 OLE DB 驱动程序的支持策略
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.custom: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 7aa291121c751b6634eed645fba52247849b6721
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66778080"
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
|Microsoft Windows 8.1 + [2014 年 4 月更新](https://go.microsoft.com/fwlink/?linkid=2073785) + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows 10<br /><br /> Microsoft Windows Server 2012 + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2012 R2 + [2014 年 4 月更新](https://go.microsoft.com/fwlink/?linkid=2073785) + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2016|  

## <a name="ado-support-policies"></a>ADO 支持策略  
 如果 ADO 应用程序不需要 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更高版本的任何功能，可以使用 Windows 附带的 SQLOLEDB OLE DB 提供程序。  

 ADO 应用程序可以使用 SQL Server 的 OLE DB 驱动程序，但如果用户这样做它们必须指定`DataTypeCompatibility=80`在连接字符串中。 如果连接字符串中包含 `DataTypeCompatibility=80`，则只能使用 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的功能。  

## <a name="ole-db-support-policies"></a>OLE DB 支持策略  
应用程序可使用随 Windows 操作系统附带的 OLE DB 提供程序 (SQLOLEDB)。 但是，这是在维护模式下，不再更新。 改为使用 OLE DB 驱动程序的 SQL Server (MSOLEDBSQL)。

## <a name="see-also"></a>另请参阅  
 [使用适用于 SQL Server 的 OLE DB 驱动程序生成应用程序](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
