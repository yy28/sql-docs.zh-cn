---
title: 删除 SQL Server 索引 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- removing indexes
- deleting indexes
- DropIndex function
- dropping indexes
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
ms.assetid: add3ba14-10b1-4723-b7c0-3e83689e9fdd
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 148565f2866e571ba783c58d1ff10413510ef6db
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37422226"
---
# <a name="dropping-a-sql-server-index"></a>删除 SQL Server 索引
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口公开**iindexdefinition:: Dropindex**函数。 这允许使用者从索引中删除[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序提供了一些[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]PRIMARY KEY 和 UNIQUE 约束作为索引。 表所有者、 数据库所有者和某些管理角色成员可以修改[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表，删除约束。 默认情况下，只有表所有者才能删除现有索引。 因此， **DropIndex**成功还是失败取决于应用程序用户的访问权限，而且还对索引所指示的类型。  
  
 使用者指定为 Unicode 字符串中的表名*pwszName*的成员*uName*联合*pTableID*参数。 *EKind*的成员*pTableID*必须为 DBKIND_NAME。  
  
 使用者指定为 Unicode 字符串中的索引名称*pwszName*的成员*uName*联合*pIndexID*参数。 *EKind*的成员*pIndexID*必须为 DBKIND_NAME。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序不支持删除表中的所有索引的 OLE DB 功能时*pIndexID*为 null。 如果*pIndexID*是 null，则返回 E_INVALIDARG。  
  
## <a name="see-also"></a>请参阅  
 [表和索引](tables-and-indexes.md)   
 [ALTER TABLE (Transact-SQL)](/sql/t-sql/statements/alter-table-transact-sql)   
 [DROP INDEX (Transact-SQL)](/sql/t-sql/statements/drop-index-transact-sql)  
  
  
