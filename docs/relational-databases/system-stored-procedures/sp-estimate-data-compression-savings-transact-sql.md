---
title: sp_estimate_data_compression_savings (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_estimate_data_compression_savings_TSQL
- sp_estimate_data_compression_savings
dev_langs:
- TSQL
helpviewer_keywords:
- compression [SQL Server], estimating
- sp_estimate_data_compression_savings
ms.assetid: 6f6c7150-e788-45e0-9d08-d6c2f4a33729
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d93c3626e7177df5920cd2e8888ba75a2416fdfe
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="spestimatedatacompressionsavings-transact-sql"></a>sp_estimate_data_compression_savings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回所请求对象的当前大小并估算对象在所请求的压缩状态下的大小。 可对所有表或部分表评估压缩。 这包括堆、聚集索引、非聚集索引、索引视图以及表和索引分区。 可使用行压缩或页压缩来压缩这些对象。 如果表、索引或分区已经过压缩，则可使用该过程来估计在重新压缩的情况下该表、索引或分区的大小。  
  
> [!NOTE]  
>  压缩和**sp_estimate_data_compression_savings**中的每个版本均不提供[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 若要对使用请求的压缩设置的对象进行大小估算，该存储过程将对源对象进行采样并且将此数据加载到在 tempdb 中创建的等效表和索引中。 然后，将按照所请求的设置压缩在 tempdb 中创建的表和索引，并计算出估计的压缩节省量。  
  
 若要更改的表、 索引或分区，使用压缩状态[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)或[ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)语句。 有关压缩的常规信息，请参阅[数据压缩](../../relational-databases/data-compression/data-compression.md)。  
  
> [!NOTE]  
>  如果现有的数据含有碎片，则可以在不使用压缩的情况下通过重新生成索引来减小数据的大小。 对于索引，在索引重新生成的过程中将应用填充因子。 这可能会增加索引的大小。  

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_estimate_data_compression_savings   
     [ @schema_name = ] 'schema_name'    
   , [ @object_name = ] 'object_name'   
   , [@index_id = ] index_id   
   , [@partition_number = ] partition_number   
   , [@data_compression = ] 'data_compression'   
[;]  
```  
  
## <a name="arguments"></a>参数  
 [ @schema_name=] '*schema_name*  
 包含表或索引视图的数据库架构的名称。 *schema_name*是**sysname**。 如果*schema_name*为 NULL，则使用当前用户的默认架构。  
  
 [ @object_name=] '*object_name*  
 索引所属的表或索引视图的名称。 object_name 为 sysname。  
  
 [ @index_id=] '*index_id*  
 索引的 ID。 *index_id*是**int**，和可以是以下值之一： 索引，NULL，或者 0 的 ID 号*object_id*是堆。 若要返回基表或视图的所有索引的信息，请指定 NULL。 如果指定 NULL，则必须指定为 NULL *partition_number*。  
  
 [ @partition_number=] '*partition_number*  
 对象中的分区号。 *partition_number*是**int**，和可以是以下值之一： 索引或堆、 NULL 或 1 个用于未分区的索引或堆的分区号。  
  
 若要指定分区，你还可以指定[$partition](../../t-sql/functions/partition-transact-sql.md)函数。 若要返回所属对象的所有分区的信息，请指定 NULL。  
  
 [ @data_compression=] '*data_compression*  
 要评估的压缩的类型。 *data_compression*可以是以下值之一： NONE、 行或页。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 将返回以下结果集，以提供表、索引或分区的当前大小和估计大小。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|object_name|**sysname**|表或索引视图的名称。|  
|schema_name|**sysname**|表或索引视图的架构。|  
|index_id|**int**|索引的索引 ID：<br /><br /> 0 = 堆<br /><br /> 1 = 聚集索引<br /><br /> > 1 = 非聚集索引|  
|partition_number|**int**|分区号。 对于未分区的表或索引，返回 1。|  
|size_with_current_compression_setting (KB)|**bigint**|当前存在的所请求的表、索引或分区的大小。|  
|size_with_requested_compression_setting (KB)|**bigint**|使用请求的压缩设置及现有填充因子（如果适用）且假定不存在碎片时的表、索引或分区的估计大小。|  
|sample_size_with_current_compression_setting (KB)|**bigint**|使用当前压缩设置时的示例大小。 这包括任何碎片。|  
|sample_size_with_requested_compression_setting (KB)|**bigint**|使用请求的压缩设置及现有填充因子（如果适用）创建的且没有碎片的样本的大小。|  
  
## <a name="remarks"></a>注释  
 可使用 sp_estimate_data_compression_savings 估算对表或分区启用行压缩或页压缩时可能带来的节省量。 例如，如果行的平均大小可以减少 40%，则可能可以将对象大小减少 40%。 您可能无法节省空间，因为这取决于填充因子和行大小。 例如，如果某行长度为 8000 字节并且您将该行的大小减少 40%，则数据页上仍只能容纳一行。 因此不会节省空间。  
  
 如果运行 sp_estimate_data_compression_savings 的结果指示表的大小将增长，则表示表中的许多行使用的几乎是数据类型的完全精度，因而为满足压缩格式的需要而增加的少量开销大于该压缩所带来的节省量。 在这种极个别的情况下，请不要启用压缩。  
  
 如果对表启用压缩，请使用 use sp_estimate_data_compression_savings 估算在未压缩该表的情况下该行的平均大小。  
  
 在此操作期间将获取该表的 (IS) 锁。 如果不能获取 (IS) 锁，则该过程将被阻止。 该表将在已提交读隔离级别下进行扫描。  
  
 如果请求的压缩设置与当前的压缩设置相同，则该存储过程将返回在没有数据碎片且使用现有填充因子时的估计大小。  
  
 如果索引或分区 ID 不存在，将不返回任何结果。  
  
## <a name="permissions"></a>权限  
 要求对该表具有 SELECT 权限。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 该过程不适用于列存储表，因此不接受数据压缩参数 COLUMNSTORE 和 COLUMNSTORE_ARCHIVE。  
  
## <a name="examples"></a>示例  
 下面的示例估计 `Production.WorkOrderRouting` 表在使用 `ROW` 压缩进行压缩后的大小。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_estimate_data_compression_savings 'Production', 'WorkOrderRouting', NULL, NULL, 'ROW' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)   
 [sys.partitions (Transact-SQL)](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [数据库引擎存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Unicode 压缩的实现](../../relational-databases/data-compression/unicode-compression-implementation.md)  
  
  
