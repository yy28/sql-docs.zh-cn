---
title: FILESTREAM 支持 |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 030f2e002c4dba8148a1e4bbcbb9eff9033308f3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47688993"
---
# <a name="filestream-support"></a>FILESTREAM 支持
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  FILESTREAM 允许通过 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 或通过直接访问 Windows 文件系统来存储和访问大型二进制值。 大型二进制值是大于 2 GB 的值。 有关增强的 FILESTREAM 支持的详细信息，请参阅[FILESTREAM &#40;SQL Server&#41;](../../../relational-databases/blob/filestream-sql-server.md)。  
  
 默认情况下，在打开数据库连接时，@@TEXTSIZE 将设置为 -1（“无限制”）。  
  
 还可以使用 Windows 文件系统 API 访问和更新 FILESTREAM 列。  
  
 有关详细信息，请参阅以下主题：  
  
-   [FILESTREAM 支持&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/filestream-support-ole-db.md)  
  
-   [FILESTREAM 支持&#40;ODBC&#41;](../../../relational-databases/native-client/odbc/filestream-support-odbc.md)  
  
-   [使用 OpenSqlFilestream 访问 FILESTREAM 数据](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
  
## <a name="querying-for-filestream-columns"></a>查询 FILESTREAM 列  
 OLE DB 中的架构行集不会报告某个列是否为 FILESTREAM 列。 OLE DB 中的 ITableDefinition 不能用于创建 FILESTREAM 列。  
  
 如 SQLColumns 在 ODBC 目录函数不会报告列是否是 FILESTREAM 列。  
  
 若要创建 FILESTREAM 列或检测哪些现有列是 FILESTREAM 列，可以使用 [sys.columns](../../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) 目录视图的 is_filestream 列。  
  
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
 如果您的客户端在编译时使用的版本[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]附带的本机客户端[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]，并在应用程序连接到[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]， **varbinary （max)** 行为将与兼容[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. 就是说，返回数据的最大大小将限制为不超过 2 GB。 对于超过 2 GB 的结果值，将发生截断，并将返回“字符串数据，右截断”警告。  
  
 如果将数据类型兼容性设置为 80，则客户端行为将与下级客户端行为一致。  
  
 使用 SQLOLEDB 或其他提供程序之前发布的客户端[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]新版[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client **varbinary （max)** 将映射到映像。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
