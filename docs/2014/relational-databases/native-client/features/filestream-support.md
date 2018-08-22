---
title: FILESTREAM 支持 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- FILESTREAM [SQL Server], SQL Server Native Client
- SQL Server Native Client [FILESTREAM support]
ms.assetid: 1ad3400d-7fcd-40c9-87ae-f5afc61e0374
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 743ffc19d94f81b3e44b02911e4086e99774eaee
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393127"
---
# <a name="filestream-support"></a>FILESTREAM 支持
  FILESTREAM 允许通过 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 或通过直接访问 Windows 文件系统来存储和访问大型二进制值。 大型二进制值是大于 2 GB 的值。 有关增强的 FILESTREAM 支持的详细信息，请参阅[FILESTREAM &#40;SQL Server&#41;](../../blob/filestream-sql-server.md)。  
  
 默认情况下，在打开数据库连接时，`@@TEXTSIZE` 将设置为 -1（“无限制”）。  
  
 还可以使用 Windows 文件系统 API 访问和更新 FILESTREAM 列。  
  
 有关详细信息，请参阅以下主题：  
  
-   [FILESTREAM 支持&#40;OLE DB&#41;](../ole-db/filestream-support-ole-db.md)  
  
-   [FILESTREAM 支持&#40;ODBC&#41;](../odbc/filestream-support-odbc.md)  
  
-   [使用 OpenSqlFilestream 访问 FILESTREAM 数据](../../blob/access-filestream-data-with-opensqlfilestream.md)  
  
## <a name="querying-for-filestream-columns"></a>查询 FILESTREAM 列  
 OLE DB 中的架构行集不会报告某个列是否为 FILESTREAM 列。 OLE DB 中的 ITableDefinition 不能用于创建 FILESTREAM 列。  
  
 如 SQLColumns 在 ODBC 目录函数不会报告列是否是 FILESTREAM 列。  
  
 若要创建 FILESTREAM 列或检测哪些现有列是 FILESTREAM 列，可以使用`is_filestream`的列[sys.columns](/sql/relational-databases/system-catalog-views/sys-columns-transact-sql)目录视图。  
  
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
 如果您的客户端在编译时使用的版本[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]附带的本机客户端[!INCLUDE[ssVersion2005](../../../includes/sscurrent-md.md)]，`varbinary(max)`行为将与兼容[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 就是说，返回数据的最大大小将限制为不超过 2 GB。 对于超过 2 GB 的结果值，将发生截断，并将返回“字符串数据，右截断”警告。  
  
 如果将数据类型兼容性设置为 80，则客户端行为将与下级客户端行为一致。  
  
 使用 SQLOLEDB 或其他提供程序之前发布的客户端[!INCLUDE[ssVersion2005](../../../includes/ssnoversion-md.md)]Native Client，`varbinary(max)`将映射到映像。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client 功能](sql-server-native-client-features.md)  
  
  
