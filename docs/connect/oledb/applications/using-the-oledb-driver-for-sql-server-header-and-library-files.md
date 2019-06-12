---
title: 使用适用于 SQL Server 的 OLE DB 驱动程序头文件和库文件 | Microsoft Docs
description: 使用适用于 SQL Server 的 OLE DB 驱动程序头文件和库文件
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- header files [OLE DB Driver for SQL Server]
- MSOLEDBSQL, header files
- OLE DB, header files
- library files [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, header files
- data access [OLE DB Driver for SQL Server], header files
- data access [OLE DB Driver for SQL Server], library files
- OLE DB Driver for SQL Server, library files
- MSOLEDBSQL, library files
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: b188649e138dddfc7dd4fd9fe974d6ccf28cc904
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66777960"
---
# <a name="using-the-ole-db-driver-for-sql-server-header-and-library-files"></a>使用适用于 SQL Server 的 OLE DB 驱动程序头文件和库文件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  在安装过程中选择 SQL Server SDK 选项，OLE DB 驱动程序时安装 SQL Server 标头和库文件，OLE DB 驱动程序。 开发应用程序时，应将开发所需的所有文件复制到开发环境并进行安装，这一点非常重要。 有关安装和重新分发适用于 SQL Server 的 OLE DB 驱动程序的详细信息，请参阅[安装 OLE DB 驱动程序适用于 SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md)。  
  
 SQL Server 标头和库文件，OLE DB 驱动程序安装在以下位置：  
  
 *%PROGRAM FILES%* \Microsoft SQL Server\Client SDK\OLEDB\182\SDK  
  
 可以使用 SQL Server 标头文件 (msoledbsql.h) 的 OLE DB 驱动程序的 SQL Server 数据访问功能的 OLE DB 驱动程序添加到自定义应用程序。 在适用于 SQL Server 的 OLE DB 驱动程序头文件中，可找到利用 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中引入的新功能所需的所有定义、特性、属性和接口。  
  
 除了，OLE DB 驱动程序为 SQL Server 标头文件，还有一个 msoledbsql.lib 库文件，这是导出库有关[OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)功能。  
  
 适用于 SQL Server 的 OLE DB 驱动程序头文件与 Microsoft 数据访问组件 (MDAC) 使用的 sqloledb.h 头文件向后兼容，但不包含 SQLOLEDB 的 CLSID（MDAC 附带的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB 访问接口）或 XML 功能的符号（适用于 SQL Server 的 OLE DB 驱动程序不支持这些符号）。    
  
 OLE DB 应用程序，用于 SQL Server 的 OLE DB 驱动程序只需引用 msoledbsql.h。 如果应用程序使用 MDAC (SQLOLEDB) 和适用于 SQL Server 的 OLE DB 驱动程序，则可同时引用 sqloledb.h 和 msoledbsql.h，但必须先引用 sqloledb.h。  
  
## <a name="using-the-ole-db-driver-for-sql-server-header-file"></a>SQL Server 标头文件使用 OLE DB 驱动程序  
 若要为 SQL Server 标头文件使用 OLE DB 驱动程序，必须使用**包括**语句包含在你的 C /C++编程代码。 以下部分介绍如何在 OLE DB 应用程序中执行此操作。  
  
> [!NOTE]  
>  仅可使用 Visual Studio 编译的 SQL Server 标头和库文件，OLE DB 驱动程序C++2012年或更高版本。  
  
### <a name="ole-db"></a>OLE DB  
 若要使用 SQL Server OLE DB 应用程序，使用以下编程代码行中的标头文件，OLE DB 驱动程序：  
  
```    
include "msoledbsql.h";  
```  
  
> [!NOTE]  
>  如果应用程序**包括**sqloledb.h，语句**包括**msoledbsql.h 语句必须晚于它。  
  
 时创建 SQL Server 与通过 OLE DB 驱动程序的数据源的连接，请使用"MSOLEDBSQL"作为提供程序名称字符串。  

  
## <a name="component-names-and-properties-by-version"></a>基于版本的组件名称和属性  

|属性|适用于 SQL Server 的 OLE DB 驱动程序|MDAC|  
|--------|----------------------------|----|   
|OLE DB PROGID|MSOLEDBSQL|SQLOLEDB|  
|OLE DB 头文件名|msoledbsql.h|Sqloledb.h|  
|OLE DB 访问接口 DLL|msoledbsql.dll|Sqloledb.dll| 
  
  
## <a name="static-linking-and-bcp-functions"></a>静态链接和 BCP 函数  
 在某一应用程序使用 BCP 函数时，对于该应用程序十分需要特别注意的是，应在连接字符串中指定来自用于编译该应用程序的头文件和库随附的相同版本的驱动程序。  
  
 有关详细信息，请参阅执行[执行大容量复制操作](../../oledb/features/performing-bulk-copy-operations.md)。  
  
## <a name="see-also"></a>另请参阅  
 [使用适用于 SQL Server 的 OLE DB 驱动程序生成应用程序](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
