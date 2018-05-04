---
title: SQL Server 的 OLE DB 驱动程序的系统要求 |Microsoft 文档
description: SQL Server 的 OLE DB 驱动程序的要求
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
- system requirements [OLE DB Driver for SQL Server]
- data access [OLE DB Driver for SQL Server], system requirements
- OLE DB Driver for SQL Server, system requirements
- MSOLEDBSQL, system requirements
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 346e5d331e9d96f23d1dd0ff2b93722b145bf3d2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="system-requirements-for-ole-db-driver-for-sql-server"></a>SQL Server 的 OLE DB 驱动程序的系统要求
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的数据访问功能（如 MARS），必须安装以下软件：  

-   OLE DB 驱动程序的客户端上的 SQL Server。  

-   服务器上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。   

> [!NOTE]  
>  确保以管理员权限进行登录，然后再安装此软件。  

## <a name="operating-system-requirements"></a>操作系统要求  
 对 SQL Server 的支持 OLE DB 驱动程序的操作系统的列表，请参阅[的 OLE DB Driver for SQL Server 支持策略](../oledb/applications/support-policies-for-oledb-driver-for-sql-server.md)。  

## <a name="sql-server-requirements"></a>SQL Server 要求  
 若要使用用于 SQL Server 的 OLE DB 驱动程序中访问数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库，你必须具有的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装。  

 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 适用于 SQL Server 支持的 MDAC、 Windows 数据访问组件，以及所有版本的 OLE DB 驱动程序的所有版本中的连接。 如果客户端的较旧版本连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，则该客户端未知的服务器数据类型将映射到与客户端版本相兼容的类型。 有关详细信息，请参阅本主题后面的“客户端版本的数据类型兼容性”。  

## <a name="cross-language-requirements"></a>跨语言要求  
 支持的操作系统的所有本地化版本支持的 OLE DB 驱动程序的 SQL Server 的英语语言版本。 是与本地化 OLE DB 驱动程序的 SQL Server 版本相同的语言的本地化操作系统上支持的 OLE DB 驱动程序的 SQL Server 的本地化的版本。 只要匹配的语言设置已安装英语语言版本的支持的操作系统也支持 OLE DB 驱动程序的 SQL Server 的本地化的版本。  

 对于升级：  

-   对于 SQL Server，英语语言版本的 OLE DB 驱动程序的 SQL Server 可以升级到 OLE DB 驱动程序的任何本地化版本。  

-   对于语言相同的 SQL Server，OLE DB 驱动程序的 SQL Server 的本地化的版本可以升级到 OLE DB 驱动程序的本地化版本。  

-   对于 SQL Server 的 OLE DB 驱动程序的 SQL Server 的本地化的版本可以升级到 OLE DB 驱动程序的英语语言版本。  

-   OLE DB 驱动程序的 SQL Server 的本地化的版本无法升级到本地化 OLE DB 驱动程序的 SQL Server 版本的另一种本地化语言。  

## <a name="data-type-compatibility-for-client-versions"></a>客户端版本的数据类型兼容性  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 OLE DB 驱动程序的 SQL Server 映射新数据类型，到较旧的数据类型与下层客户端兼容下表中所示。  

 OLE DB 和 ADO 的应用程序可以使用**DataTypeCompatibility**与 OLE DB 驱动程序的 SQL Server 以运行旧的数据类型的连接字符串关键字。 当**DataTypeCompatibility = 80**，OLE DB 客户端将连接使用[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]的表格格式数据流 (TDS) 版本，而不是 TDS 版本。 这意味着，对于[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]和更高版本的数据类型，低级别转换将执行按服务器，而不是 OLE DB 驱动程序的 SQL Server。 此外，这还意味着，连接中的可用功能将被限制为 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 功能集。 尽可能早地对 API 调用中使用新数据类型或功能的尝试进行检测，将错误返回给调用应用程序，而不是尝试将无效的请求传递给服务器。   


 IDBInfo::GetKeywords 将始终返回关键字列表，对应于连接上的服务器版本不受**DataTypeCompatibility**。  

|数据类型|SQL Server Native Client<br /><br />SQL Server 2005|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|用于 SQL Server 的 OLE DB 驱动程序|Windows 数据访问组件、MDAC 及<br /><br /> OLE DB 驱动程序的 SQL Server OLE DB 应用程序与 DataTypeCompatibility = 80|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|CLR UDT (\<= 8 Kb)|udt|udt|udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|varbinary|图像|  
|varchar(max)|varchar|varchar|varchar|Text|  
|nvarchar(max)|nvarchar|nvarchar|nvarchar|Ntext|  
|xml|xml|xml|xml|Ntext|  
|CLR UDT (> 8Kb)|varbinary|udt|udt|图像|  
|date|varchar|date|date|Varchar|  
|datetime2|varchar|datetime2|datetime2|Varchar|  
|datetimeoffset|varchar|datetimeoffset|datetimeoffset|Varchar|  
|time|varchar|time|time|Varchar|  

## <a name="see-also"></a>另请参阅  
 [用于 SQL Server 的 OLE DB 驱动程序](../oledb/oledb-driver-for-sql-server.md)   
 [安装适用于 SQL Server 的 OLE DB 驱动程序](../oledb/applications/installing-oledb-driver-for-sql-server.md)  
