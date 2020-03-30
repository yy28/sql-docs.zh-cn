---
title: 删除 SQL Server 索引 | Microsoft Docs
description: 使用 OLE DB Driver for SQL Server 删除 SQL Server 索引
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- removing indexes
- deleting indexes
- DropIndex function
- dropping indexes
- OLE DB Driver for SQL Server, indexes
- indexes [OLE DB]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 708deecefe451115ca0fca97075f88311dec2f5a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "68015251"
---
# <a name="dropping-a-sql-server-index"></a>删除 SQL Server 索引
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 公开 IIndexDefinition::DropIndex  函数。 这允许使用者从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 表中删除某一索引。  
  
 OLE DB Driver for SQL Server 将一些 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PRIMARY KEY 和 UNIQUE 约束作为索引公开。 表所有者、数据库所有者或某些管理角色成员可以修改 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 表，以及删除约束。 默认情况下，只有表所有者才能删除现有索引。 因此，DropIndex 成功或失败不仅取决于应用程序用户的访问权限，而且取决于指示的索引的类型  。  
  
 在 pTableID 参数的 uName 联合的 pwszName 成员中，使用者将表名指定为 Unicode 字符串    。 pTableID 的 eKind 成员必须是 DBKIND_NAME   。  
  
 在 pIndexID 参数的 uName 联合的 pwszName成员中，使用者将索引名指定为 Unicode 字符串    。 pIndexID 的 eKind 成员必须是 DBKIND_NAME   。 在 pIndexID 为 Null 时，适用于 SQL Server 的 OLE DB 驱动程序不支持删除表上所有索引的 OLE DB 功能  。 如果 pIndexID 为 Null，则返回 E_INVALIDARG  。  
  
## <a name="see-also"></a>另请参阅  
 [表和索引](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md)   
 [DROP INDEX (Transact-SQL)](../../../t-sql/statements/drop-index-transact-sql.md)  
  
  
