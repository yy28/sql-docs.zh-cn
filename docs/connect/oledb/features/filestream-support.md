---
title: FILESTREAM 支持 |Microsoft 文档
description: OLE DB 驱动程序中的 SQL Server 的 FILESTREAM 支持
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- FILESTREAM [SQL Server], OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server [FILESTREAM support]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d528a05cd30024d2ff865a99acae1a11f187dbfc
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="filestream-support"></a>FILESTREAM 支持
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  FILESTREAM 允许通过 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 或通过直接访问 Windows 文件系统来存储和访问大型二进制值。 大型二进制值是大于 2 GB 的值。 有关增强 FILESTREAM 支持的详细信息，请参阅[FILESTREAM &#40;SQL Server&#41;](../../../relational-databases/blob/filestream-sql-server.md)。  
  
 当打开数据库连接时， **@@TEXTSIZE** 将设置为-1 （"无限制"），默认情况下。  
  
 还可以使用 Windows 文件系统 API 访问和更新 FILESTREAM 列。  
  
 有关详细信息，请参阅以下主题：  
  
-   [FILESTREAM 支持&#40;OLE DB&#41;](../../oledb/ole-db/filestream-support-ole-db.md)    
  
-   [使用 OpenSqlFilestream 访问 FILESTREAM 数据](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
  
## <a name="querying-for-filestream-columns"></a>查询 FILESTREAM 列  
 OLE DB 中的架构行集不会报告某个列是否为 FILESTREAM 列。 在 OLE DB ITableDefinition 不能用于创建 FILESTREAM 列。    
  
 若要创建 FILESTREAM 列或检测哪些现有列是 FILESTREAM 列，可以使用**is_filestream**列[sys.columns](../../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)目录视图。  
  
 以下是一个示例：  
  
```  
-- Create a table with a FILESTREAM column.  
CREATE TABLE Bob_01 (GuidCol1 uniqueidentifier ROWGUIDCOL NOT NULL UNIQUE DEFAULT NEWID(), IntCol2 int, varbinaryCol3 varbinary(max) FILESTREAM);  
  
-- Find FILESTREAM columns.  
SELECT name FROM sys.columns WHERE is_filestream=1;  
  
-- Determine whether a column is a FILESTREAM column.  
SELECT is_filestream FROM sys.columns WHERE name = 'varbinaryCol3' AND object_id IN (SELECT object_id FROM sys.tables WHERE name='Bob_01');  
```  
  
## <a name="down-level-compatibility"></a>下级兼容性  
 如果你的客户端已经过编译使用 SQL Server 的 OLE DB 驱动程序，应用程序连接到[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]， **varbinary （max)**行为将与兼容[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 就是说，返回数据的最大大小将限制为不超过 2 GB。 更大的结果值的 2 GB，将发生截断，并且将返回"右侧的字符串数据的截断"警告。  
  
 如果将数据类型兼容性设置为 80，则客户端行为将与下级客户端行为一致。  
  
 使用 SQLOLEDB 或其他提供程序之前发布的客户端[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]， **varbinary （max)**将映射到映像。  
  
## <a name="see-also"></a>另请参阅  
 [用于 SQL Server 功能的 OLE DB 驱动程序](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
