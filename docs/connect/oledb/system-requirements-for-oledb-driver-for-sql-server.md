---
title: 适用于 SQL Server 的 OLE DB 驱动程序的系统要求 | Microsoft Docs
description: 适用于 SQL Server 的 OLE DB 驱动程序的要求
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- system requirements [OLE DB Driver for SQL Server]
- data access [OLE DB Driver for SQL Server], system requirements
- OLE DB Driver for SQL Server, system requirements
- MSOLEDBSQL, system requirements
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: a2ff38f4322209c7ed6eb46a5ba97f360ca3650b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47821025"
---
# <a name="system-requirements-for-ole-db-driver-for-sql-server"></a>适用于 SQL Server 的 OLE DB 驱动程序的系统要求
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的数据访问功能（如 MARS），必须安装以下软件：  

-   OLE DB 驱动程序在客户端上的 SQL Server。  

-   服务器上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。   

> [!NOTE]  
>  确保以管理员权限进行登录，然后再安装此软件。  

## <a name="operating-system-requirements"></a>操作系统要求  
 有关支持的 SQL Server 的 OLE DB 驱动程序的操作系统的列表，请参阅[的 OLE DB Driver for SQL Server 支持策略](../oledb/applications/support-policies-for-oledb-driver-for-sql-server.md)。  

## <a name="sql-server-requirements"></a>SQL Server 要求  
 若要使用用于 SQL Server 的 OLE DB 驱动程序中访问数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库，必须具有的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装。  

 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 支持与 MDAC 的所有版本、Windows 数据访问组件以及适用于 SQL Server 的 OLE DB 驱动程序的所有版本的连接。 如果客户端的较旧版本连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，则该客户端未知的服务器数据类型将映射到与客户端版本相兼容的类型。 有关详细信息，请参阅本主题后面的“客户端版本的数据类型兼容性”。  

## <a name="cross-language-requirements"></a>跨语言要求  
 英文版的适用于 SQL Server 的 OLE DB 驱动程序可以在所有受支持的本地化操作系统上使用。 在同一语言的本地化 OLE DB 驱动程序的 SQL Server 版本的本地化操作系统上支持的 OLE DB 驱动程序适用于 SQL Server 本地化的版本。 只要安装了匹配的语言设置，则受支持的操作系统的英文版还支持适用于 SQL Server 的 OLE DB 驱动程序的本地化版本。  

 对于升级：  

-   适用于 SQL Server，英语语言版本的 OLE DB 驱动程序适用于 SQL Server 可以升级到任何本地化版本的 OLE DB 驱动程序。  

-   OLE DB 驱动程序适用于 SQL Server 的本地化的版本可以同语言的 SQL server 升级到本地化版本的 OLE DB 驱动程序。  

-   适用于 SQL Server，OLE DB Driver for SQL Server 的本地化的版本可以升级到英文版本的 OLE DB 驱动程序。  

-   OLE DB 驱动程序适用于 SQL Server 的本地化的版本无法升级到本地化 OLE DB 驱动程序的不同本地化语言的 SQL Server 版本。  

## <a name="data-type-compatibility-for-client-versions"></a>客户端版本的数据类型兼容性  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和适用于 SQL Server 的 OLE DB 驱动程序将新数据类型映射到与下级客户端相兼容的较旧的数据类型，如下表所示。  

 OLE DB 和 ADO 应用程序可以使用**DataTypeCompatibility**使用 OLE DB 驱动程序用于与旧的数据类型一起运行的 SQL Server 的连接字符串关键字。 如果 DataTypeCompatibility=80，OLE DB 客户端将使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 表格格式数据流 (TDS) 版本而不是 TDS 版本进行连接。 也就是说，对于 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和较新的数据类型，将由服务器而不是适用于 SQL Server 的 OLE DB 驱动程序执行下级转换。 此外，这还意味着，连接中的可用功能将被限制为 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 功能集。 尽可能早地对 API 调用中使用新数据类型或功能的尝试进行检测，将错误返回给调用应用程序，而不是尝试将无效的请求传递给服务器。   


 IDBInfo::GetKeywords 将始终返回的关键字列表，在连接上的服务器版本相对应，不受**DataTypeCompatibility**。  

|数据类型|SQL Server Native Client<br /><br />SQL Server 2005|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|适用于 SQL Server 的 OLE DB 驱动程序|Windows 数据访问组件、MDAC 及<br /><br /> OLE DB 驱动程序的 SQL Server OLE DB 应用程序与 DataTypeCompatibility = 80|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|CLR UDT (\<= 8Kb)|udt|udt|udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|varbinary|图像|  
|varchar(max)|varchar|varchar|varchar|文本|  
|nvarchar(max)|NVARCHAR|NVARCHAR|NVARCHAR|Ntext|  
|xml|xml|xml|xml|Ntext|  
|CLR UDT (> 8Kb)|varbinary|udt|udt|图像|  
|日期|varchar|日期|日期|Varchar|  
|datetime2|varchar|datetime2|datetime2|Varchar|  
|datetimeoffset|varchar|datetimeoffset|datetimeoffset|Varchar|  
|time|varchar|time|time|Varchar|  

## <a name="see-also"></a>另请参阅  
 [适用于 SQL Server 的 OLE DB 驱动程序](../oledb/oledb-driver-for-sql-server.md)   
 [安装适用于 SQL Server 的 OLE DB 驱动程序](../oledb/applications/installing-oledb-driver-for-sql-server.md)  
