---
title: 删除 SQL Server 索引 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- removing indexes
- deleting indexes
- DropIndex function
- dropping indexes
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
ms.assetid: add3ba14-10b1-4723-b7c0-3e83689e9fdd
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9be4e3607097c476f083c32eed9f13fecc0d3842
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704523"
---
# <a name="dropping-a-sql-server-index"></a>删除 SQL Server 索引
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序公开**IIndexDefinition：:D ropindex**函数。 这允许使用者从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中删除某一索引。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序将一些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 主键和 UNIQUE 约束公开为索引。 表所有者、数据库所有者或某些管理角色成员可以修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表，以及删除约束。 默认情况下，只有表所有者才能删除现有索引。 因此，DropIndex 成功或失败不仅取决于应用程序用户的访问权限，而且取决于指示的索引的类型****。  
  
 在 pTableID 参数的 uName 联合的 pwszName 成员中，使用者将表名指定为 Unicode 字符串******。 pTableID 的 eKind 成员必须是 DBKIND_NAME****。  
  
 在 pIndexID 参数的 uName 联合的 pwszName成员中，使用者将索引名指定为 Unicode 字符串******。 pIndexID 的 eKind 成员必须是 DBKIND_NAME****。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]当*pIndexID*为 null 时，Native Client OLE DB 提供程序不支持删除表上的所有索引的 OLE DB 功能。 如果 pIndexID 为 Null，则返回 E_INVALIDARG**。  
  
## <a name="see-also"></a>另请参阅  
 [表和索引](tables-and-indexes.md)   
 [ALTER TABLE (Transact-SQL)](/sql/t-sql/statements/alter-table-transact-sql)   
 [DROP INDEX (Transact-SQL)](/sql/t-sql/statements/drop-index-transact-sql)  
  
  
