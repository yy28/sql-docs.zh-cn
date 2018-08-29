---
title: 向 SQL Server 表添加列 |Microsoft Docs
description: 将列添加到使用 SQL Server 的 OLE DB 驱动程序的 SQL Server 表
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
- columns [OLE DB]
- AddColumn function
- OLE DB Driver for SQL Server, columns
- adding columns
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 65ac05fb361e3308304bf8457c036d68cc610501
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43020881"
---
# <a name="adding-a-column-to-a-sql-server-table"></a>向 SQL Server 表添加列
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server 的 OLE DB 驱动程序公开**itabledefinition:: Addcolumn**函数。 利用此函数，使用者便可向 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 表中添加列。  
  
 当您添加到列[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]表，OLE DB 驱动程序的 SQL Server 使用者约束，如下所示：  
  
-   如果 DBPROP_COL_AUTOINCREMENT 为 VARIANT_TRUE，则 DBPROP_COL_NULLABLE 必须为 VARIANT_FALSE。  
  
-   如果相应列是使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] timestamp 数据类型定义的，则 DBPROP_COL_NULLABLE 必须为 VARIANT_FALSE。  
  
-   对于任何其他列定义，DBPROP_COL_NULLABLE 都必须为 VARIANT_TRUE。  
  
 在 pTableID 参数的 uName 联合的 pwszName 成员中，使用者将表名指定为 Unicode 字符串。 pTableID 的 eKind 成员必须是 DBKIND_NAME。  
  
 在 uName 联合（位于 DBCOLUMNDESC 参数 pColumnDesc 的 dbcid 成员中）的 pwszName 成员中，将新列的名称指定为 Unicode 字符串。 eKind 成员必须为 DBKIND_NAME。  
  
## <a name="see-also"></a>另请参阅  
 [表和索引](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md)  
  
  
