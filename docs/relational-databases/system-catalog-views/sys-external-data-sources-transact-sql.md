---
title: sys.external_data_sources (TRANSACT-SQL) |Microsoft Docs
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
dev_langs:
- TSQL
ms.assetid: 1016db6e-9950-4ae2-a004-bd4171e27359
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 0ac216e2d50f2cc10f836c706ba8c07bc29c206b
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39549497"
---
# <a name="sysexternaldatasources-transact-sql"></a>sys.external_data_sources (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  每个外部数据源的当前数据库中存在对应的一行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]， [!INCLUDE[ssSDS](../../includes/sssds-md.md)]，和[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。  
  
 每个外部数据源的服务器上存在对应的一行[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|data_source_id|**int**|外部数据源的对象 ID。||  
|NAME|**sysname**|外部数据源的名称。||  
|位置|**nvarchar(4000)**|连接字符串，其中包括协议、 IP 地址和端口的外部数据源。||  
|type_desc|**nvarchar(255)**|数据源类型显示为字符串。|HADOOP，RDBMS，SHARD_MAP_MANAGER RemoteDataArchiveTypeExtDataSource|  
|type|**tinyint**|数据源类型显示为数字。|0-HADOOP<br /><br /> 1 - RDBMS<br /><br /> 2-SHARD_MAP_MANAGER<br /><br /> 3 - RemoteDataArchiveTypeExtDataSource|  
|resource_manager_location|**nvarchar(4000)**|键入 HADOOP、 IP 和端口 Hadoop 资源管理器的位置。 这用于提交 Hadoop 数据源上的作业。<br /><br /> 对于其他类型的外部数据源为 NULL。||  
|credential_id|**int**|数据库的对象 ID 范围用于连接到外部数据源的凭据。||  
|database_name|**sysname**|对于类型 RDBMS 中，远程数据库的名称。 对于类型，SHARD_MAP_MANAGER，分片映射管理器数据库的名称。 对于其他类型的外部数据源为 NULL。||  
|shard_map_name|**sysname**|对于类型 SHARD_MAP_MANAGER，分片映射的名称。 对于其他类型的外部数据源为 NULL。||  
  
## <a name="permissions"></a>Permissions  
 目录视图中仅显示用户拥有的安全对象的元数据，或用户对其拥有某些权限的安全对象的元数据。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [sys.external_file_formats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)   
 [sys.external_tables &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  
