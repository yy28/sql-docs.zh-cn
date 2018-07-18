---
title: 删除 SQL Server 索引 |Microsoft 文档
description: 删除 sql server 索引使用的 SQL Server OLE DB 驱动程序
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-tables-indexes
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- removing indexes
- deleting indexes
- DropIndex function
- dropping indexes
- OLE DB Driver for SQL Server, indexes
- indexes [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: a790633c129fe1cfb3da9a21a9e4fd9fae3513cd
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2018
ms.locfileid: "35690150"
---
# <a name="dropping-a-sql-server-index"></a>删除 SQL Server 索引
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server 的 OLE DB 驱动程序公开**IIndexDefinition::DropIndex**函数。 这允许使用者能够删除从索引[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]表。  
  
 SQL Server 的 OLE DB 驱动程序公开一些[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]作为索引的 PRIMARY KEY 和 UNIQUE 约束。 表所有者，数据库所有者和某些管理角色成员可以修改[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]表，删除约束。 默认情况下，只有表所有者才能删除现有索引。 因此， **DropIndex**成功还是失败取决于不仅应用程序用户的访问权限但还指示索引的类型。  
  
 使用者中 Unicode 字符串形式指定表名称*pwszName*的成员*uName*联合中*pTableID*参数。 *EKind*的成员*pTableID*必须 DBKIND_NAME。  
  
 使用者为 Unicode 字符字符串中指定的索引名称*pwszName*的成员*uName*联合中*pIndexID*参数。 *EKind*的成员*pIndexID*必须 DBKIND_NAME。 SQL Server 的 OLE DB 驱动程序不支持在表上删除所有索引的 OLE DB 功能时*pIndexID*为 null。 如果*pIndexID*是 null，则返回 E_INVALIDARG。  
  
## <a name="see-also"></a>请参阅  
 [表和索引](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md)   
 [DROP INDEX (Transact-SQL)](../../../t-sql/statements/drop-index-transact-sql.md)  
  
  
