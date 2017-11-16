---
title: "监视系统版本控制的内存优化临时表 | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 03/28/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7a06785d-dbcb-44de-b95c-26b131471bee
caps.latest.revision: "11"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0469d41e4bab668d3f5d83d67489f79c0a0bad91
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="monitoring-memory-optimized-system-versioned-temporal-tables"></a>监视系统版本控制型内存优化临时表
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  每个系统版本控制型内存优化表都可以使用现有视图来跟踪详细的和摘要性的内存占用情况。  
  
 详细的内存占用情况（按每个主要的系统版本控制型内部历史记录临时表进行拆分）：  
  
```  
--Details of memory consumption   
WITH InMemoryTemporalTables   
AS   
(   
   SELECT SCHEMA_NAME ( T1.schema_id ) AS TemporalTableSchema  
      , T1.object_id AS TemporalTableObjectId  
      , IT.object_id AS InternalTableObjectId  
      , OBJECT_NAME ( IT.parent_object_id ) AS TemporalTableName  
      , IT.Name AS InternalHistoryStagingName   
   FROM sys.internal_tables IT    
   JOIN sys.tables T1 ON IT.parent_object_id = T1.object_id   
   WHERE T1.is_memory_optimized  = 1 AND T1.temporal_type = 2    
)   
  
SELECT   
     TemporalTableSchema  
   , T.TemporalTableName  
   , T.InternalHistoryStagingName,    
     CASE   
        WHEN C.object_id = T.TemporalTableObjectId   
        THEN 'Temporal Table Consumption'   
         ELSE 'Internal Table Consumption'   
         END ConsumedBy  
     , C.*   
   FROM sys.dm_db_xtp_memory_consumers C   
   JOIN InMemoryTemporalTables T   
      ON C.object_id = T.TemporalTableObjectId OR C.object_id = T.InternalTableObjectId   
   WHERE T.TemporalTableSchema = 'dbo' AND  T.TemporalTableName = 'FXCurrencyPairs' ;  
  
```  
  
 内存占用情况摘要（系统版本控制型内存优化表的总计）：  
  
```  
--Summary of memory consumption   
WITH InMemoryTemporalTables   
AS   
(   
   SELECT SCHEMA_NAME ( T1.schema_id ) AS TemporalTableSchema  
     , T1.object_id AS TemporalTableObjectId  
     , IT.object_id AS InternalTableObjectId  
     , OBJECT_NAME ( IT.parent_object_id ) AS TemporalTableName  
     , IT.Name AS InternalHistoryStagingName   
   FROM sys.internal_tables IT    
   JOIN sys.tables T1 ON IT.parent_object_id = T1.object_id   
   WHERE T1.is_memory_optimized  = 1 AND T1.temporal_type = 2    
)   
, DetailedConsumption   
AS   
(   
   SELECT TemporalTableSchema  
      , T.TemporalTableName  
      , T.InternalHistoryStagingName  
      , CASE   
           WHEN C.object_id = T.TemporalTableObjectId   
           THEN 'Temporal Table Consumption'   
           ELSE 'Internal Table Consumption'   
           END ConsumedBy  
      , C.*   
    FROM sys.dm_db_xtp_memory_consumers C   
   JOIN InMemoryTemporalTables T   
      ON C.object_id = T.TemporalTableObjectId OR C.object_id = T.InternalTableObjectId   
)   
  
SELECT TemporalTableSchema  
     TemporalTableName  
   , sum ( allocated_bytes ) AS allocated_bytes  
   , sum ( used_bytes ) AS used_bytes   
FROM DetailedConsumption   
WHERE TemporalTableSchema = 'dbo' AND  TemporalTableName = 'FXCurrencyPairs'   
GROUP BY TemporalTableSchema, TemporalTableName ;  
  
```  
  
## <a name="did-this-article-help-you-were-listening"></a>本文是否对你有帮助？ 我们洗耳恭听  
 你正在查找哪些信息，是否已经找到？ 我们不断听取你的反馈来改进内容。 请将你的评论提交到 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Monitoring%20Memory-Optimized%20System-Versioned%20Temporal%20Tables%20page)  
  
## <a name="see-also"></a>另请参阅  
 [系统版本控制临时表与内存优化表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [创建系统版本控制的内存优化临时表](../../relational-databases/tables/creating-a-memory-optimized-system-versioned-temporal-table.md)   
 [使用带有系统版本的内存优化临时表](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)   
 [内存优化系统版本控制临时表的性能注意事项](../../relational-databases/tables/memory-optimized-system-versioned-temporal-tables-performance.md)   
 [临时表](../../relational-databases/tables/temporal-tables.md)   
 [临时表系统一致性检查](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [管理版本由系统控制的临时表中历史数据的保留期](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [临时表元数据视图和函数](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
