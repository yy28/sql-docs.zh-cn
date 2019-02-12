---
title: DBCC PDW_SHOWEXECUTIONPLAN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.technology: data-warehouse
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: uc-msft
ms.author: umajay
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 88738f857ab83b4a2f7927f75a2795a4f0eb1169
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034248"
---
# <a name="dbcc-pdwshowexecutionplan-transact-sql"></a>DBCC PDW_SHOWEXECUTIONPLAN (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

显示在特定 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 或 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 计算节点或控制节点上运行的查询的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 执行计划。 在计算节点和控制节点上运行查询时，使用它来解决查询性能问题。
  
了解在计算节点上运行的 SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查询的查询性能问题后，可通过几种方法来提高性能。 可提高计算节点上查询性能的方法包括创建多列统计信息、创建非聚集索引或使用查询提示。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [Transact-SQL 语法约定 (Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
Azure SQL 数据仓库的语法：

```sql
DBCC PDW_SHOWEXECUTIONPLAN ( distribution_id, spid )  
[;]  
```  
Azure 并行数据仓库语法：
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( pdw_node_id, spid )  
[;]  
```  
  
## <a name="arguments"></a>参数  
 distribution_id  
 正在运行查询计划的分发的标识符。 这必须为整数，并且不能为 NULL。 以 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 为目标时使用。  
  
 pdw_node_id  
 正在运行查询计划的节点的标识符。 这必须为整数，并且不能为 NULL。 以设备为目标时使用。  
  
 spid  
 正在运行查询计划的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会话的标识符。 这必须为整数，并且不能为 NULL。  
  
## <a name="permissions"></a>Permissions  
 需要对 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 的 CONTROL 权限。  
  
需要设备上的 VIEW SERVER STATE 权限。
  
## <a name="examples-includesssdwincludessssdw-mdmd"></a>示例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]  
  
### <a name="a-dbcc-pdwshowexecutionplan-basic-syntax"></a>A. DBCC PDW_SHOWEXECUTIONPLAN 基本语法  
 在 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 实例上运行时，修改上述查询以同时选择 distribution_id。  
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status], [distribution_id]  
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
order by request_id, [dms_step_index];  
```  
  
这将返回每个主动运行分发的 spid。 如果对会话 375 中正在运行的分发 1 感到好奇，可运行以下命令。
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 1, 375 );  
```  

## <a name="examples-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="b-dbcc-pdwshowexecutionplan-basic-syntax"></a>B. DBCC PDW_SHOWEXECUTIONPLAN 基本语法  
 运行时间太长的查询运行的是 DMS 查询计划操作或 SQL 查询计划操作。  
  
如果查询运行的是 DMS 查询计划操作，对于未完成的步骤，可以使用以下查询来检索节点 ID 和 会话 ID 的列表。
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status]   
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
AND pdw_node_id = 201001   
order by request_id, [dms_step_index], [distribution_id];  
```  
  
基于上述查询的结果，使用 sql_spid 和 pdw_node_id 作为 DBCC PDW_SHOWEXECUTIONPLAN 的参数。 例如，以下命令会显示 pdw_node_id 201001 和 sql_spid 375 的执行计划。
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 201001, 375 );  
```  

## <a name="see-also"></a>另请参阅
[DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL)](dbcc-pdw-showpartitionstats-transact-sql.md)  
[DBCC PDW_SHOWSPACEUSED (Transact-SQL)](dbcc-pdw-showspaceused-transact-sql.md)
