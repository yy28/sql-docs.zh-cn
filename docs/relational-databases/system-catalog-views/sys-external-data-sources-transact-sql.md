---
title: sys.external_data_sources (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 1016db6e-9950-4ae2-a004-bd4171e27359
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0f082cc4246236133fe7439514d0cc2b64d3c7e8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysexternaldatasources-transact-sql"></a>sys.external_data_sources (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  包含在当前数据库中为每个外部数据源的行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]， [!INCLUDE[ssSDS](../../includes/sssds-md.md)]，和[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。  
  
 包含每个外部数据源的服务器上的行[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|data_source_id|**int**|外部数据源的对象 ID。||  
|name|**sysname**|外部数据源的名称。||  
|位置|**nvarchar(4000)**|连接字符串，其中包括协议、 IP 地址和外部数据源的端口。||  
|type_desc|**nvarchar(255)**|数据源类型显示为字符串。|HADOOP、 RDBMS，于包含 SHARD_MAP_MANAGER RemoteDataArchiveTypeExtDataSource|  
|type|**tinyint**|数据源类型显示为数字。|0-HADOOP<br /><br /> 1 - RDBMS<br /><br /> 2-于包含 SHARD_MAP_MANAGER<br /><br /> 3 - RemoteDataArchiveTypeExtDataSource|  
|resource_manager_location|**nvarchar(4000)**|有关键入 HADOOP、 IP 和端口的 Hadoop 资源管理器的位置。 这用于提交 Hadoop 数据源上的作业。<br /><br /> 其他类型的外部数据源为 NULL。||  
|credential_id|**int**|数据库的对象 ID 范围的凭据用于连接到外部数据源。||  
|database_name|**sysname**|对于类型 RDBMS，远程数据库的名称。 对于类型，于包含 SHARD_MAP_MANAGER，分片映射管理器数据库的名称。 其他类型的外部数据源为 NULL。||  
|shard_map_name|**sysname**|对于类型于包含 SHARD_MAP_MANAGER，分片映射的名称。 其他类型的外部数据源为 NULL。||  
  
## <a name="permissions"></a>权限  
 目录视图中仅显示用户拥有的安全对象的元数据，或用户对其拥有某些权限的安全对象的元数据。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [sys.external_file_formats &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)   
 [sys.external_tables &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  
