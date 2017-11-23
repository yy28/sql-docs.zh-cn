---
title: "sys.pdw_nodes_partitions (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: b4216752-4813-4b2c-b259-7d8ffc6cc190
caps.latest.revision: "11"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: eb9462ad5ab281d6178ccf33270e759b569825b1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwnodespartitions-transact-sql"></a>sys.pdw_nodes_partitions (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  包含每个分区的所有表和索引中的大多数类型的行[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]数据库。 所有表和索引都包含至少一个分区，无论它们进行显式分区。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|partition_id|`bigint`|分区 id。 是一个数据库中唯一的。|  
|object_id|`int`|此分区所属的对象 id。 每个表或视图都至少包含一个分区。|  
|index_id|`int`|此分区所属的对象中的索引的 id。|  
|partition_number|`int`|拥有索引或堆中的基于 1 的分区号。 有关[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，此列的值为 1。|  
|hobt_id|`bigint`|包含此分区的行的数据堆或 B 树的 ID。|  
|rows|`bigint`|此分区中的大约行数。 |  
|data_compression|`int`|指示每个分区的压缩状态：<br /><br /> 0 = NONE<br /><br /> 1 = ROW<br /><br /> 2 = PAGE<br /><br /> 3 = COLUMNSTORE|  
|data_compression_desc|`nvarchar(60)`|指示每个分区的压缩状态。 可能的值为 NONE、ROW 和 PAGE。|  
|pdw_node_id|`int`|唯一标识符[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]节点。|  
  
## <a name="permissions"></a>Permissions  
 需要 CONTROL SERVER 权限。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  

### <a name="example-a-display-rows-in-each-partition-within-each-distribution"></a>在每个分布内的每个分区中的示例 a： 显示行 

适用于： [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]
 
若要在每个分布内的每个分区中显示的行数，请使用[DBCC PDW_SHOWPARTITIONSTATS (SQL Server PDW)](../../t-sql/database-console-commands/dbcc-pdw-showpartitionstats-transact-sql.md) 。

### <a name="example-b-uses-system-views-to-view-rows-in-each-partition-of-each-distribution-of-a-table"></a>示例 b： 使用系统视图以查看每个分布表的每个分区中的行

适用于：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]
 
此查询返回的行数中的每个分布表的每个分区`myTable`。  
 
```  
SELECT o.name, pnp.index_id, pnp.partition_id, pnp.rows,   
    pnp.data_compression_desc, pnp.pdw_node_id  
FROM sys.pdw_nodes_partitions AS pnp  
JOIN sys.pdw_nodes_tables AS NTables  
    ON pnp.object_id = NTables.object_id  
AND pnp.pdw_node_id = NTables.pdw_node_id  
JOIN sys.pdw_table_mappings AS TMap  
    ON NTables.name = TMap.physical_name 
    AND substring(TMap.physical_name,40, 10) = pnp.distribution_id 
JOIN sys.objects AS o  
    ON TMap.object_id = o.object_id  
WHERE o.name = 'myTable'  
ORDER BY o.name, pnp.index_id, pnp.partition_id;  
```    
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  

