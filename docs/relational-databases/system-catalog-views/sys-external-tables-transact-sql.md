---
title: sys.external_tables (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: fac4720c-b679-4ab2-864b-ff7810a9b559
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fd6b9c144df14f9480ff825726fc918deb86f6cf
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52516286"
---
# <a name="sysexternaltables-transact-sql"></a>sys.external_tables (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  包含当前数据库中每个外部表的行。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|\<继承列 >||此视图所继承的列的列表，请参阅[sys.objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。||  
|max_column_id_used|**int**|为此表使用过的最大列 ID。||  
|uses_ansi_nulls|**bit**|在创建表时，将 SET ANSI_NULLS 数据库选项设置为 ON。||  
|data_source_id|**int**|外部数据源的对象 ID。||  
|file_format_id|**int**|对于通过 HADOOP 外部数据源的外部表，这是外部文件格式的对象 ID。||  
|位置|**nvarchar(4000)**|对于通过 HADOOP 外部数据源的外部表，这是 HDFS 中的外部数据的路径。||  
|reject_type|**tinyint**|对于通过 HADOOP 外部数据源的外部表，这是查询外部数据时被拒绝的行计数的方法。|值-已拒绝的行数。<br /><br /> 百分比-已拒绝的行的百分比。|  
|reject_value|**float**|对于通过 HADOOP 外部数据源的外部表：<br /><br /> 有关*reject_type =* 值，这是行拒绝使查询失败前允许的数量。<br /><br /> 有关*reject_type* = 百分比，这是行拒绝使查询失败前允许的百分比。||  
|reject_sample_value|**int**|有关*reject_type* = 百分比，这是要加载，成功或失败之前计算已拒绝的行的百分比, 的行数。|如果 reject_type = VALUE。|  
|distribution_type|**int**|对于 SHARD_MAP_MANAGER 外部数据源对外部表，这是对基础表的行的数据分布。|0-分片<br /><br /> 1-复制<br /><br /> 2-轮循机制|  
|distribution_desc|**nvarchar(120)**|对于 SHARD_MAP_MANAGER 外部数据源对外部表，这是显示为字符串的分布类型。||  
|sharding_column_id|**int**|对于对 SHARD_MAP_MANAGER 外部数据源和分片分布的外部表，这是列的包含分片密钥值的列 ID。||  
|remote_schema_name|**sysname**|对于 SHARD_MAP_MANAGER 外部数据源对外部表，这是基础表 （如果不同于其中定义外部表的架构） 在远程数据库的位置的架构。||  
|remote_object_name|**sysname**|对于 SHARD_MAP_MANAGER 外部数据源对外部表，这是远程数据库 （如果从外部表的名称不同） 上的基础表的名称。||  
  
## <a name="permissions"></a>权限  
 目录视图中仅显示用户拥有的安全对象的元数据，或用户对其拥有某些权限的安全对象的元数据。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [sys.external_file_formats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)   
 [sys.external_data_sources &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [CREATE EXTERNAL TABLE (Transact-SQL)](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  
