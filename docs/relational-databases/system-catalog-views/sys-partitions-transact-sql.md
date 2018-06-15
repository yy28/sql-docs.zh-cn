---
title: sys.partitions (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- partitions
- partitions_TSQL
- sys.partitions_TSQL
- sys.partitions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.partitions catalog view
ms.assetid: 1c19e1b1-c925-4dad-a652-581692f4ab5e
caps.latest.revision: 60
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4902bca55295c2e6e870e2f3488cc178c0f771fa
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33181183"
---
# <a name="syspartitions-transact-sql"></a>sys.partitions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  数据库中的所有表和大部分类型的索引的每个分区各对应一行。 在此视图中不包含全文索引、 空间和 XML 等特殊索引类型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的所有表和索引都至少包含一个分区，无论它们是否已进行显式分区均为如此。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|指示分区 ID。 是一个数据库中唯一的。|  
|object_id|**int**|指示此分区所属的对象的 ID。 每个表或视图都至少包含一个分区。|  
|index_id|**int**|指示此分区所属的对象内的索引的 ID。<br /><br /> 0 = 堆<br />1 = 聚集的索引<br />2 或更高 = 非聚集索引|  
|partition_number|**int**|所属索引或堆中的从 1 开始的分区号。 对于未分区的表和索引，此列的值为 1。|  
|hobt_id|**bigint**|指示包含此分区的行的数据堆或 B 树的 ID。|  
|rows|**bigint**|指示此分区中的大约行数。|  
|filestream_filegroup_id|**int**|**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 指示在此分区上存储的 FILESTREAM 文件组的 ID。|  
|data_compression|**tinyint**|指示每个分区的压缩状态：<br /><br /> 0 = NONE <br />1 = ROW <br />2 = PAGE <br />3 = COLUMNSTORE:**适用于**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />4 = COLUMNSTORE_ARCHIVE:**适用于**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /><br /> **注意：** 全文索引将压缩的任何版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|data_compression_desc|**nvarchar(60)**|指示每个分区的压缩状态。 行存储表的可能值为 NONE、ROW 和 PAGE。 列存储表的可能值为 COLUMNSTORE 和 COLUMNSTORE_ARCHIVE。|  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询 SQL Server 系统目录常见问题解答](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
