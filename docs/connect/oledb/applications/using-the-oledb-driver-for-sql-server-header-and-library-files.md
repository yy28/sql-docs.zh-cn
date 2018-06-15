---
title: 使用 OLE DB 驱动程序适用于 SQL 的服务器标头和库文件 |Microsoft 文档
description: SQL Server 标头和库文件的使用 OLE DB 驱动程序
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: f228442c31d754265769645a640b1eb1285c5897
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2018
ms.locfileid: "35612142"
---
# <a name="using-the-ole-db-driver-for-sql-server-header-and-library-files"></a>使用 OLE DB 驱动程序适用于 SQL 的服务器标头和库文件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  当 SQL Server SDK 选项 OLE DB 驱动程序选择在安装过程期间安装 SQL Server 标头和库文件 OLE DB 驱动程序。 开发应用程序时，应将开发所需的所有文件复制到开发环境并进行安装，这一点非常重要。 有关安装和重新发布用于 SQL Server 的 OLE DB 驱动程序的详细信息，请参阅[安装 OLE DB 驱动程序的 SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md)。  
  
 用于 SQL Server 标头和库文件的 OLE DB 驱动程序安装在以下位置：  
  
 *%Program 文件 %* \Microsoft SQL Server\Client SDK\OLEDB\180\SDK  
  
 为 SQL Server 标头文件 (msoledbsql.h) OLE DB 驱动程序可以用于将 SQL Server 数据访问功能 OLE DB 驱动程序添加到你的自定义应用程序。 OLE DB 驱动程序为 SQL Server 标头文件包含所有的定义、 属性、 属性，并利用新功能所需的接口中引入[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。  
  
 除了 OLE DB 驱动程序为 SQL Server 标头文件，此外还有一个 msoledbsql.lib 库文件的导出库为[OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)功能。  
  
 为 SQL Server 标头文件 OLE DB 驱动程序是与 sqloledb.h 标头文件使用与 Microsoft 数据访问组件 (MDAC)，向后兼容，但未包含 SQLOLEDB 的 Clsid (OLE DB 访问接口[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]附带 MDAC) 或符号XML 功能 （这不受 SQL Server OLE DB 驱动程序）。    
  
 OLE DB 应用程序使用 SQL Server 的 OLE DB 驱动程序只需引用 msoledbsql.h。 如果应用程序使用 SQL Server 的 MDAC (SQLOLEDB) 和 OLE DB 驱动程序，它可引用 sqloledb.h 和 msoledbsql.h，但对 sqloledb.h 的引用必须出现在最前面。  
  
## <a name="using-the-ole-db-driver-for-sql-server-header-file"></a>SQL Server 的头文件使用 OLE DB 驱动程序  
 若要 SQL Server 的头文件使用 OLE DB 驱动程序，必须使用**包括**中你 C/c + + 编程代码语句。 下列各节描述如何执行此 OLE DB 应用程序。  
  
> [!NOTE]  
>  用于 SQL Server 标头和库文件的 OLE DB 驱动程序只能编译使用 Visual Studio c + + 2012年或更高版本。  
  
### <a name="ole-db"></a>OLE DB  
 若要使用 SQL Server 的 OLE DB 应用程序，使用下面的程序代码行的标头文件的 OLE DB 驱动程序：  
  
```    
include "msoledbsql.h";  
```  
  
> [!NOTE]  
>  如果应用程序**包括**sqloledb.h，语句**包括**msoledbsql.h 语句必须晚于它。  
  
 时创建 SQL Server 与通过 OLE DB 驱动程序的数据源的连接，请使用"MSOLEDBSQL"作为提供程序名称字符串。  

  
## <a name="component-names-and-properties-by-version"></a>基于版本的组件名称和属性  

|“属性”|用于 SQL Server 的 OLE DB 驱动程序|MDAC|  
|--------|----------------------------|----|   
|OLE DB PROGID|MSOLEDBSQL|SQLOLEDB|  
|OLE DB 头文件名|msoledbsql.h|Sqloledb.h|  
|OLE DB 访问接口 DLL|msoledbsql.dll|Sqloledb.dll| 
  
  
## <a name="static-linking-and-bcp-functions"></a>静态链接和 BCP 函数  
 在某一应用程序使用 BCP 函数时，对于该应用程序十分需要特别注意的是，应在连接字符串中指定来自用于编译该应用程序的头文件和库随附的相同版本的驱动程序。  
  
 有关详细信息，请参阅执行[执行大容量复制操作](../../oledb/features/performing-bulk-copy-operations.md)。  
  
## <a name="see-also"></a>请参阅  
 [使用适用于 SQL Server 的 OLE DB 驱动程序生成应用程序](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
