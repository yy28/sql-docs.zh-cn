---
title: 将列添加到 SQL Server 表 |Microsoft 文档
description: 将列添加到使用 SQL Server 的 OLE DB 驱动程序的 SQL Server 表
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-tables-indexes
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- AddColumn function
- OLE DB Driver for SQL Server, columns
- adding columns
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 2f49f014e29401d0f99bd5f9bd59551c94255399
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="adding-a-column-to-a-sql-server-table"></a>向 SQL Server 表添加列
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL Server 的 OLE DB 驱动程序公开**ITableDefinition::AddColumn**函数。 这允许使用者添加到列[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]表。  
  
 当你将列添加到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]表，OLE DB 驱动程序的 SQL Server 使用者约束，如下所示：  
  
-   如果 DBPROP_COL_AUTOINCREMENT 为 VARIANT_TRUE，则 DBPROP_COL_NULLABLE 必须为 VARIANT_FALSE。  
  
-   如果通过使用已定义该列[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**时间戳**数据类型，DBPROP_COL_NULLABLE 必须为 VARIANT_FALSE。  
  
-   对于任何其他列定义，DBPROP_COL_NULLABLE 都必须为 VARIANT_TRUE。  
  
 使用者中 Unicode 字符串形式指定表名称*pwszName*的成员*uName*联合中*pTableID*参数。 *EKind*的成员*pTableID*必须 DBKIND_NAME。  
  
 新的列名称指定为中的 Unicode 字符字符串*pwszName*的成员*uName*联合中*dbcid* DBCOLUMNDESC 参数的成员*pColumnDesc*。 *EKind*成员必须是 DBKIND_NAME。  
  
## <a name="see-also"></a>另请参阅  
 [表和索引](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md)  
  
  
