---
title: "DBCC PDW_SHOWEXECUTIONPLAN (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/16/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|database-console-commands
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
caps.latest.revision: 12
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 461ee87f41692172b31125e36553c0eab0b09772
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-pdwshowexecutionplan-transact-sql"></a>DBCC PDW_SHOWEXECUTIONPLAN (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

显示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]运行对特定的查询的执行计划[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]计算节点或控制节点。 用于查询运行的计算节点和控制节点时排除查询性能问题。
  
一旦查询性能问题理解为 SMP[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在计算节点上运行的查询有几种方法来提高性能。 可能的方法，以提高查询性能，在计算节点上的包括创建多列统计信息、 创建非聚集索引，或使用查询提示。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定 &#40;Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
SQL Server 的语法：

```sql
DBCC PDW_SHOWEXECUTIONPLAN ( distribution_id, spid )  
[;]  
```  
语法 Azure 并行数据仓库：
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( pdw_node_id, spid )  
[;]  
```  
  
## <a name="arguments"></a>参数  
 *distribution_id*  
 正在运行的查询计划的分发的标识符。 这是一个整数，不能为 NULL。 使用在面向[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。  
  
 *pdw_node_id*  
 正在运行的查询计划的节点标识符。 这是一个整数，不能为 NULL。 以设备为目标时使用。  
  
 *spid*  
 标识符[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在运行的查询计划的会话。 这是一个整数，不能为 NULL。  
  
## <a name="permissions"></a>Permissions  
 在需要的 CONTROL 权限[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。  
  
需要在设备上的 VIEW SERVER STATE 权限。
  
## <a name="examples-includesssdwincludessssdw-mdmd"></a>示例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]  
  
### <a name="a-dbcc-pdwshowexecutionplan-basic-syntax"></a>A. DBCC PDW_SHOWEXECUTIONPLAN 基本语法  
 在上运行时[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]实例时，修改上述查询还选择 distribution_id。  
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status], [distribution_id]  
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
order by request_id, [dms_step_index];  
```  
  
这将返回每个主动运行分发的 spid。 如果你是想有关哪些分发 1 已在会话 375 中运行，你将运行以下命令。
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 1, 375 );  
```  

## <a name="examples-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="b-dbcc-pdwshowexecutionplan-basic-syntax"></a>B. DBCC PDW_SHOWEXECUTIONPLAN 基本语法  
 为运行时间太长的查询是运行 DMS 查询计划操作或 SQL 查询计划操作。  
  
如果查询正在运行 DMS 查询计划操作，你可以使用以下查询来检索的节点 Id 和步骤不完整的会话 Id 的列表。
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status]   
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
AND pdw_node_id = 201001   
order by request_id, [dms_step_index], [distribution_id];  
```  
  
根据前面的查询的结果，使用作为参数 DBCC PDW_SHOWEXEUCTIONPLAN sql_spid 和 pdw_node_id。 例如，以下命令显示为 pdw_node_id 201001 和 sql_spid 375 的执行计划。
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 201001, 375 );  
```  

## <a name="see-also"></a>另请参阅
[DBCC PDW_SHOWPARTITIONSTATS &#40;Transact SQL &#41;](dbcc-pdw-showpartitionstats-transact-sql.md)  
[DBCC PDW_SHOWSPACEUSED &#40;Transact SQL &#41;](dbcc-pdw-showspaceused-transact-sql.md)

