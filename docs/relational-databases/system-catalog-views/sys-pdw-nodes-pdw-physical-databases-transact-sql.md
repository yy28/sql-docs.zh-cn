---
title: "sys.pdw_nodes_pdw_physical_databases (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/09/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 70e0939d-4d97-4ae0-ba16-934e0a80e718
caps.latest.revision: "9"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f54cc6c6d5de9559ed53e5762ecc471ea303f559
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwnodespdwphysicaldatabases-transact-sql"></a>sys.pdw_nodes_pdw_physical_databases (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  包含计算节点上每个物理数据库的行。 若要获取有关数据库的详细的信息的聚合的物理数据库信息。 若要将信息进行合并，联接`sys.pdw_nodes_pdw_physical_databases`到`sys.pdw_database_mappings`和`sys.databases`表。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|数据库的对象 ID。 请注意，此值不相同中 database_id [sys.databases &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)视图。|  
|physical_name|**sysname**|Shell/计算节点上数据库的物理名称。 此值是在 physical_name 列中的值与相同[sys.pdw_database_mappings &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)视图。|  
|pdw_node_id|**int**|与节点关联的唯一数字 id。|  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-returning"></a>A. 返回  
 以下查询返回的名称和每个数据库的 ID 中 master 和相应的数据库名称在每个计算节点上。  
  
```  
SELECT D.database_id AS DBID_in_master, D.name AS UserDatabaseName,   
PD.pdw_node_id AS NodeID, DM.physical_name AS PhysDBName   
FROM sys.databases AS D  
JOIN sys.pdw_database_mappings AS DM  
    ON D.database_id = DM.database_id  
JOIN sys.pdw_nodes_pdw_physical_databases AS PD  
    ON DM.physical_name = PD.physical_name  
ORDER BY D.database_id, PD.pdw_node_ID;  
```  
  
### <a name="b-using-syspdwnodespdwphysicaldatabases-to-gather-detailed-object-information"></a>B. 使用 sys.pdw_nodes_pdw_physical_databases 收集详细的对象信息  
 以下查询显示有关索引的信息，其中包括有关数据库的有用信息的对象属于数据库中的对象。  
  
```  
SELECT D.name AS UserDatabaseName, D.database_id AS DBIDinMaster,  
DM.physical_name AS PhysDBName, PD.pdw_node_id AS NodeID,   
IU.object_id, IU.index_id, IU.user_seeks, IU.user_scans, IU.user_lookups, IU.user_updates  
FROM sys.databases AS D  
JOIN sys.pdw_database_mappings AS DM  
    ON D.database_id = DM.database_id  
JOIN sys.pdw_nodes_pdw_physical_databases AS PD  
    ON DM.physical_name = PD.physical_name  
JOIN sys.dm_pdw_nodes_db_index_usage_stats AS IU  
    ON PD.database_id = IU.database_id  
ORDER BY D.database_id, IU.object_id, IU.index_id, PD.pdw_node_ID;  
```  
  
### <a name="c-using-syspdwnodespdwphysicaldatabases-to-determine-the-encryption-state"></a>C. 使用 sys.pdw_nodes_pdw_physical_databases 确定的加密状态  
 下面的查询提供 AdventureWorksPDW2012 数据库加密状态。  
  
```  
WITH dek_encryption_state AS   
(  
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id, encryption_state  
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek  
        INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map  
            ON dek.database_id = node_db_map.database_id AND dek.pdw_node_id = node_db_map.pdw_node_id  
        LEFT JOIN sys.pdw_database_mappings AS db_map  
            ON node_db_map .physical_name = db_map.physical_name  
        INNER JOIN sys.dm_pdw_nodes AS nodes  
            ON nodes.pdw_node_id = dek.pdw_node_id  
    WHERE dek.encryptor_thumbprint <> 0x  
)  
SELECT TOP 1 encryption_state  
       FROM  dek_encryption_state  
       WHERE dek_encryption_state.database_id = DB_ID('AdventureWorksPDW2012 ')  
       ORDER BY (CASE encryption_state WHEN 3 THEN -1 ELSE encryption_state END) DESC;  
```  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.pdw_database_mappings &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)  
  
  

