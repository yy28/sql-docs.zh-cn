---
title: SQL 数据仓库和并行数据仓库目录视图 |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.service: sql-data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ef6f58e2-0162-4bb2-951a-a786da7453e4
aauthor: julieMSFT
ms.author: jrasnick
manager: jroth
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: ef736003be3c07fb1e48520fbaf2186181735427
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822341"
---
# <a name="sql-data-warehouse-and-parallel-data-warehouse-catalog-views"></a>SQL 数据仓库和并行数据仓库目录视图

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

 本主题列出了[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]目录视图。  
  
 所有[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]并[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]目录视图以开头**sys.pdw**。  
  
## <a name="includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd-catalog-views"></a>[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]目录视图  
 下列目录视图对两者都适用[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]:  
  
 [sys.pdw_column_distribution_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-column-distribution-properties-transact-sql.md)  
  
 [sys.pdw_distributions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)  
  
 [sys.pdw_index_mappings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md)  
  
 [sys.pdw_loader_backup_run_details (Transact-SQL)](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
 [sys.pdw_loader_backup_runs (Transact-SQL)](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
 [sys.pdw_nodes_column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)  
  
 [sys.pdw_nodes_column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)  
  
 [sys.pdw_nodes_column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-segments-transact-sql.md)  
  
 [sys.pdw_nodes_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-columns-transact-sql.md)  
  
 [sys.pdw_nodes_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-indexes-transact-sql.md)  
  
 [sys.pdw_nodes_partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-partitions-transact-sql.md)  
  
 [sys.pdw_nodes_pdw_physical_databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-pdw-physical-databases-transact-sql.md)  
  
 [sys.pdw_nodes_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-tables-transact-sql.md) 

 [sys.pdw_replicated_table_cache_state (Transact-SQL)](sys-pdw-replicated-table-cache-state-transact-sql.md) 
  
 [sys.pdw_table_distribution_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-table-distribution-properties-transact-sql.md)  
  
 [sys.pdw_table_mappings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-table-mappings-transact-sql.md) 

[sys.workload_management_workload_classifier_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifier-details-transact-sql.md) (Preview)

[sys.workload_management_workload_classifiers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifiers-transact-sql.md) (Preview)

> [!Note]
> 可以在 SQL 数据仓库 Gen2 上预览工作负荷分类。 工作负荷管理分类和重要性预览适用于发布日期为 2019 年 4 月 9 日或更晚的内部版本。  用户应避免使用早于此日期的内部版本进行工作负荷管理测试。  若要确定内部版本是否支持工作负荷管理，请在连接到 SQL 数据仓库实例时运行 select @@version。
 
## <a name="includesspdwincludessspdw-mdmd-catalog-views"></a>[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 目录视图  
 以下目录视图将应用于[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]仅：

 [sys.pdw_database_mappings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)  
  
 [sys.pdw_diag_event_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-diag-event-properties-transact-sql.md)  
  
 [sys.pdw_diag_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-diag-events-transact-sql.md)  
  
 [sys.pdw_diag_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-diag-sessions-transact-sql.md)  
  
 [sys.pdw_health_alerts &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)  
  
 [sys.pdw_health_component_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-component-groups-transact-sql.md)  
  
 [sys.pdw_health_component_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-component-properties-transact-sql.md)  
  
 [sys.pdw_health_component_status_mappings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-component-status-mappings-transact-sql.md)  
  
 [sys.pdw_health_components &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)  
  
 [sys.pdw_loader_run_stages (Transact-SQL)](../../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)  
  
## <a name="see-also"></a>请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
