---
title: "将列添加到 SQL Server 表 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-tables-indexes
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- AddColumn function
- SQL Server Native Client OLE DB provider, columns
- adding columns
ms.assetid: 22bae18a-bc9d-4617-8660-ed8b17a468d4
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 48f1471efa0c2edd80dc867eb93571ec4b8deb67
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="adding-a-column-to-a-sql-server-table"></a>向 SQL Server 表添加列
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序公开**ITableDefinition::AddColumn**函数。 这允许使用者添加到列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。  
  
 当你将列添加到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序使用者约束，如下所示：  
  
-   如果 DBPROP_COL_AUTOINCREMENT 为 VARIANT_TRUE，则 DBPROP_COL_NULLABLE 必须为 VARIANT_FALSE。  
  
-   如果通过使用已定义该列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**时间戳**数据类型，DBPROP_COL_NULLABLE 必须为 VARIANT_FALSE。  
  
-   对于任何其他列定义，DBPROP_COL_NULLABLE 都必须为 VARIANT_TRUE。  
  
 使用者中 Unicode 字符串形式指定表名称*pwszName*的成员*uName*联合中*pTableID*参数。 *EKind*的成员*pTableID*必须 DBKIND_NAME。  
  
 新的列名称指定为中的 Unicode 字符字符串*pwszName*的成员*uName*联合中*dbcid* DBCOLUMNDESC 参数的成员*pColumnDesc*。 *EKind*成员必须是 DBKIND_NAME。  
  
## <a name="see-also"></a>另请参阅  
 [表和索引](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
