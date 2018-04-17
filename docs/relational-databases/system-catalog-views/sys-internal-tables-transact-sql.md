---
title: sys.internal_tables (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.internal_tables
- internal_tables
- sys.internal_tables_TSQL
- internal_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- internal tables
- sys.internal_tables catalog view
ms.assetid: a5821c70-f150-4676-8476-3a31f7403dca
caps.latest.revision: 52
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9f0f30bc972bf0af35d582b908da6e163917b965
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysinternaltables-transact-sql"></a>sys.internal_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为每个作为内部表的对象返回一行。 内部表由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自动生成以支持各种功能。 例如，创建主 XML 索引时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将自动创建一个内部表以保存拆分的 XML 文档数据。 内部表将显示在**sys**的每个数据库的架构，并且具有唯一的、 由系统生成的名称，例如，指示其函数， **xml_index_nodes_2021582240_32001**或**queue_messages_1977058079**  
  
 内部表不包括用户可访问的数据，并且其架构是固定的，不可改变。 不能在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中引用内部表名称。 例如，不能执行如 SELECT 语句\*FROM  *\<sys.internal_table_name >*。 但是，可以查询目录视图以查看内部表的元数据。  
  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**\<列继承自 sys.objects >**||该视图继承的列的列表，请参阅[sys.objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。|  
|**internal_type**|**tinyint**|内部表的类型：<br /><br /> 201 = **queue_messages**<br /><br /> 202 = **xml_index_nodes**<br /><br /> 203 = **fulltext_catalog_freelist**<br /><br /> 205 = **query_notification**<br /><br /> 206 = **service_broker_map**<br /><br /> 207 = **extended_indexes** （如空间索引）<br /><br /> 208 = **filestream_tombstone**<br /><br /> 209 = **change_tracking**<br /><br /> 210 = **tracked_committed_transactions**|  
|**internal_type_desc**|**nvarchar(60)**|内部表的类型说明：<br /><br /> QUEUE_MESSAGES<br /><br /> XML_INDEX_NODES<br /><br /> FULLTEXT_CATALOG_FREELIST<br /><br /> FULLTEXT_CATALOG_MAP<br /><br /> QUERY_NOTIFICATION<br /><br /> SERVICE_BROKER_MAP<br /><br /> EXTENDED_INDEXES<br /><br /> FILESTREAM_TOMBSTONE<br /><br /> CHANGE_TRACKING<br /><br /> TRACKED_COMMITTED_TRANSACTIONS|  
|**parent_id**|**int**|父项的 ID，无论该父项的是否在架构范围内。 否则，其值为 0（如果没有父项）。<br /><br /> **queue_messages** = **object_id**的队列<br /><br /> **xml_index_nodes** = **object_id**的 xml 索引<br /><br /> **fulltext_catalog_freelist** = **fulltext_catalog_id**的全文目录<br /><br /> **fulltext_index_map** = **object_id**的全文索引<br /><br /> **query_notification**，或**service_broker_map** = 0<br /><br /> **extended_indexes** = **object_id**的扩展索引，例如空间索引<br /><br /> **object_id**哪些表启用跟踪的表 = **change_tracking**|  
|**parent_minor_id**|**int**|父项的次要 ID。<br /><br /> **xml_index_nodes** = **index_id**的 XML 索引<br /><br /> **extended_indexes** = **index_id**的扩展索引，例如空间索引<br /><br /> 0 = **queue_messages**， **fulltext_catalog_freelist**， **fulltext_index_map**， **query_notification**， **service_broker_map**，或**change_tracking**|  
|**lob_data_space_id**|**int**|对于该表，非零值是存放大型对象 (LOB) 数据的数据空间（文件组或分区方案）的 ID。|  
|**filestream_data_space_id**|**int**|保留供将来使用。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="remarks"></a>注释  
 内部表与父实体位于同一文件组。 可以使用下面示例 F 中所示的目录查询返回内部表中用于行内数据、行外数据和大型对象 (LOB) 数据的页数。  
  
 你可以使用[sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)系统过程以返回内部表空间使用情况数据。 **sp_spaceused**用以下方法报告内部表空间：  
  
-   当指定队列名称时，将引用与队列关联的基础内部表并报告其存储空间使用情况。  
  
-   中包含的 XML 索引、 空间索引和全文索引的内部表使用的页**index_size**列。 在指定表或索引的视图名称，则在列会包括 XML 索引、 空间索引，并为该对象的全文索引的页**保留**和**index_size**。  
  
## <a name="examples"></a>示例  
 下列示例说明如何使用目录视图查询内部表元数据。  
  
### <a name="a-show-internal-tables-that-inherit-columns-from-the-sysobjects-catalog-view"></a>A. 显示继承 sys.objects 目录视图中的列的内部表  
  
```  
SELECT * FROM sys.objects WHERE type = 'IT';  
```  
  
### <a name="b-return-all-internal-table-metadata-including-that-which-is-inherited-from-sysobjects"></a>B. 返回所有内部表元数据（包括从 sys.objects 继承的元数据）  
  
```  
SELECT * FROM sys.internal_tables;  
```  
  
### <a name="c-return-internal-table-columns-and-column-data-types"></a>C. 返回内部表列和列数据类型  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    ,itab.name AS internal_table_name  
    ,typ.name AS column_data_type   
    ,col.*  
FROM sys.internal_tables AS itab  
JOIN sys.columns AS col ON itab.object_id = col.object_id  
JOIN sys.types AS typ ON typ.user_type_id = col.user_type_id  
ORDER BY itab.name, col.column_id;  
```  
  
### <a name="d-return-internal-table-indexes"></a>D. 返回内部表索引  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    , itab.name AS internal_table_name  
    , idx.*  
FROM sys.internal_tables AS itab  
JOIN sys.indexes AS idx ON itab.object_id = idx.object_id  
ORDER BY itab.name, idx.index_id;  
```  
  
### <a name="e-return-internal-table-statistics"></a>E. 返回内部表统计信息  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    ,itab.name AS internal_table_name  
    , s.*  
FROM sys.internal_tables AS itab  
JOIN sys.stats AS s ON itab.object_id = s.object_id  
ORDER BY itab.name, s.stats_id;  
```  
  
### <a name="f-return-internal-table-partition-and-allocation-unit-information"></a>F. 返回内部表分区和分配单元信息  
  
```  
SELECT SCHEMA_NAME(itab.schema_id) AS schema_name  
    ,itab.name AS internal_table_name  
    ,idx.name AS heap_or_index_name  
    ,p.*  
    ,au.*  
FROM sys.internal_tables AS itab  
JOIN sys.indexes AS idx  
--     JOIN to the heap or the clustered index  
    ON itab.object_id = idx.object_id AND idx.index_id IN (0,1)  
JOIN   sys.partitions AS p   
    ON p.object_id = idx.object_id AND p.index_id = idx.index_id  
JOIN   sys.allocation_units AS au  
--     IN_ROW_DATA (type 1) and ROW_OVERFLOW_DATA (type 3) => JOIN to partition's Hobt  
--     else LOB_DATA (type 2) => JOIN to the partition ID itself.  
ON au.container_id =    
    CASE au.type   
        WHEN 2 THEN p.partition_id   
        ELSE p.hobt_id   
    END  
ORDER BY itab.name, idx.index_id;  
```  
  
### <a name="g-return-internal-table-metadata-for-xml-indexes"></a>G. 返回 XML 索引的内部表元数据  
  
```  
SELECT t.name AS parent_table  
    ,t.object_id AS parent_table_id  
    ,it.name AS internal_table_name  
    ,it.object_id AS internal_table_id  
    ,xi.name AS primary_XML_index_name  
    ,xi.index_id as primary_XML_index_id  
FROM sys.internal_tables AS it  
JOIN sys.tables AS t   
    ON it.parent_id = t.object_id  
JOIN sys.xml_indexes AS xi   
    ON it.parent_id = xi.object_id  
    AND it.parent_minor_id  = xi.index_id  
WHERE it.internal_type_desc = 'XML_INDEX_NODES';  
GO  
```  
  
### <a name="h-return-internal-table-metadata-for-service-broker-queues"></a>H. 返回 Service Broker 队列的内部表元数据  
  
```  
SELECT q.name AS queue_name  
    ,q.object_id AS queue_id  
    ,it.name AS internal_table_name  
    ,it.object_id AS internal_table_id  
FROM sys.internal_tables AS it  
JOIN sys.service_queues  AS  q ON it.parent_id = q.object_id  
WHERE it.internal_type_desc = 'QUEUE_MESSAGES';  
GO  
```  
  
## <a name="i-return-internal-table-metadata-for-all-service-broker-services"></a>I. 返回所有 Service Broker 服务的内部表元数据  
  
```  
SELECT *   
FROM tempdb.sys.internal_tables   
WHERE internal_type_desc = 'SERVICE_BROKER_MAP';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [对象目录视图&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
