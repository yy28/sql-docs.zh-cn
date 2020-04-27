---
title: FILESTREAM 支持 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- FILESTREAM [SQL Server], SQL Server Native Client
- SQL Server Native Client [FILESTREAM support]
ms.assetid: 1ad3400d-7fcd-40c9-87ae-f5afc61e0374
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 33e447048f7058ee81b0b144f0aa94a370f6d670
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63046259"
---
# <a name="filestream-support"></a>FILESTREAM 支持
  FILESTREAM 允许通过 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 或通过直接访问 Windows 文件系统来存储和访问大型二进制值。 大型二进制值是大于 2 GB 的值。 若要详细了解增强的 FILESTREAM 支持，请参阅 [FILESTREAM (SQL Server)](../../blob/filestream-sql-server.md)。  
  
 默认情况下，在打开数据库连接时，`@@TEXTSIZE` 将设置为 -1（“无限制”）。  
  
 还可以使用 Windows 文件系统 API 访问和更新 FILESTREAM 列。  
  
 有关详细信息，请参阅下列主题：  
  
-   [FILESTREAM 支持 &#40;OLE DB&#41;](../ole-db/filestream-support-ole-db.md)  
  
-   [FILESTREAM 支持 &#40;ODBC&#41;](../odbc/filestream-support-odbc.md)  
  
-   [使用 OpenSqlFilestream 访问 FILESTREAM 数据](../../blob/access-filestream-data-with-opensqlfilestream.md)  
  
## <a name="querying-for-filestream-columns"></a>查询 FILESTREAM 列  
 OLE DB 中的架构行集不会报告某个列是否为 FILESTREAM 列。 OLE DB 中的 ITableDefinition 不能用于创建 FILESTREAM 列。  
  
 ODBC 中的目录函数（如 SQLColumns）不会报告某个列是否为 FILESTREAM 列。  
  
 若要创建 FILESTREAM 列或检测哪些现有列是 FILESTREAM 列，可以使用[sys.databases](/sql/relational-databases/system-catalog-views/sys-columns-transact-sql)目录`is_filestream`视图的列。  
  
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
 如果客户[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]端是使用附带的 Native client 版本编译的[!INCLUDE[ssVersion2005](../../../includes/sscurrent-md.md)]， `varbinary(max)`则行为将与[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]兼容。 就是说，返回数据的最大大小将限制为不超过 2 GB。 对于超过 2 GB 的结果值，将发生截断，并将返回“字符串数据，右截断”警告。  
  
 如果将数据类型兼容性设置为 80，则客户端行为将与下级客户端行为一致。  
  
 对于使用 SQLOLEDB 的客户端或在[!INCLUDE[ssVersion2005](../../../includes/ssnoversion-md.md)] Native Client 之前发布的其他提供程序`varbinary(max)` ，将映射到映像。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client 功能](sql-server-native-client-features.md)  
  
  
