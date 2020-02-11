---
title: sys. dm_pdw_nodes_database_encryption_keys （Transact-sql）
ms.custom: seo-dt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: e7fd02b2-5d7e-4816-a0af-b58ae2ac3f7a
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c319259d8997db2ff39d90b408056d03eb008782
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401642"
---
# <a name="sysdm_pdw_nodes_database_encryption_keys-transact-sql"></a>sys. dm_pdw_nodes_database_encryption_keys （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  返回与数据库加密状态以及相关联数据库加密密钥有关的信息。 **sys. dm_pdw_nodes_database_encryption_keys**提供每个节点的此信息。 有关数据库加密的详细信息，请参阅[透明数据加密（SQL Server PDW）](../../analytics-platform-system/transparent-data-encryption.md)。  
  
|列名|数据类型|说明|  
|-----------------|---------------|-----------------|  
|database_id|**int**|每个节点上的物理数据库的 ID。|  
|encryption_state|**int**|指示此节点上的数据库是否已加密或未加密。<br /><br /> 0 = 不存在数据库加密密钥，未加密<br /><br /> 1 = 未加密<br /><br /> 2 = 正在进行加密<br /><br /> 3 = 已加密<br /><br /> 4 = 正在更改密钥<br /><br /> 5 = 正在进行解密<br /><br /> 6 = 正在进行保护更改（正在更改加密数据库加密密钥的证书。）|  
|create_date|**datetime**|显示加密密钥的创建日期。|  
|regenerate_date|**datetime**|显示重新生成加密密钥的日期。|  
|modify_date|**datetime**|显示加密密钥的修改日期。|  
|set_date|**datetime**|显示加密密钥应用于数据库的日期。|  
|opened_date|**datetime**|显示上次打开数据库密钥的时间。|  
|key_algorithm|**varchar （？）**|显示用于密钥的算法。|  
|key_length|**int**|显示密钥的长度。|  
|encryptor_thumbprint|**varbin**|显示加密程序的指纹。|  
|percent_complete|**实际上**|数据库加密状态更改的完成百分比。 如果未发生状态更改，则为 0。|  
|node_id|**int**|与节点关联的唯一数字 id。|  
  
## <a name="permissions"></a>权限  
 要求对服务器拥有 VIEW SERVER STATE 权限。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下面的示例联接`sys.dm_pdw_nodes_database_encryption_keys`到其他系统表，以指示 TDE 保护数据库的每个节点的加密状态。  
  
```  
SELECT D.database_id AS DBIDinMaster, D.name AS UserDatabaseName,   
PD.pdw_node_id AS NodeID, DM.physical_name AS PhysDBName,   
keys.encryption_state  
FROM sys.dm_pdw_nodes_database_encryption_keys AS keys  
JOIN sys.pdw_nodes_pdw_physical_databases AS PD  
    ON keys.database_id = PD.database_id AND keys.pdw_node_id = PD.pdw_node_id  
JOIN sys.pdw_database_mappings AS DM  
    ON DM.physical_name = PD.physical_name  
JOIN sys.databases AS D  
    ON D.database_id = DM.database_id  
ORDER BY D.database_id, PD.pdw_node_ID;  
```  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [&#40;Transact-sql&#41;创建数据库加密密钥](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [ALTER DATABASE ENCRYPTION KEY &#40;Transact-sql&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY &#40;Transact-sql&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)  
  
  

