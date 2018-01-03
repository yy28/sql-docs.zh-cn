---
title: "删除 SQL Server 索引 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-tables-indexes
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- removing indexes
- deleting indexes
- DropIndex function
- dropping indexes
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
ms.assetid: add3ba14-10b1-4723-b7c0-3e83689e9fdd
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6ea14c79c046a63d51dd5f9587d36150bd95f494
ms.sourcegitcommit: b603dcac7326bba387befe68544619e026e6a15e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="dropping-a-sql-server-index"></a>删除 SQL Server 索引
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序公开**IIndexDefinition::DropIndex**函数。 这允许使用者能够删除从索引[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序公开一些[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]作为索引的 PRIMARY KEY 和 UNIQUE 约束。 表所有者，数据库所有者和某些管理角色成员可以修改[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表，删除约束。 默认情况下，只有表所有者才能删除现有索引。 因此， **DropIndex**成功还是失败取决于不仅应用程序用户的访问权限但还指示索引的类型。  
  
 使用者中 Unicode 字符串形式指定表名称*pwszName*的成员*uName*联合中*pTableID*参数。 *EKind*的成员*pTableID*必须 DBKIND_NAME。  
  
 使用者为 Unicode 字符字符串中指定的索引名称*pwszName*的成员*uName*联合中*pIndexID*参数。 *EKind*的成员*pIndexID*必须 DBKIND_NAME。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持在表上删除所有索引的 OLE DB 功能时*pIndexID*为 null。 如果*pIndexID*是 null，则返回 E_INVALIDARG。  
  
## <a name="see-also"></a>另请参阅  
 [表和索引](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)   
 [DROP INDEX (Transact-SQL)](../../t-sql/statements/drop-index-transact-sql.md)  
  
  
