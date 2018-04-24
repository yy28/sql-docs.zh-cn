---
title: ALTER DATABASE（并行数据仓库）| Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5751656b-7aae-4152-a314-4c631bea4fc4
caps.latest.revision: 10
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0dd532ce7001c52d9fef2f3fd030fd6cf53e8a77
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="alter-database-parallel-data-warehouse"></a>ALTER DATABASE（并行数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  修改[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]中复制表、分布式表和事务日志的最大数据库大小选项。 使用此语句可在数据库大小增长或收缩时管理数据库的磁盘空间分配。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [Transact-SQL 语法约定 (Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Parallel Data Warehouse  
ALTER DATABASE database_name    
    SET ( <set_database_options>   | <db_encryption_option> )  
[;]  
  
<set_database_options> ::=   
{  
    AUTOGROW = { ON | OFF }  
    | REPLICATED_SIZE = size [GB]  
    | DISTRIBUTED_SIZE = size [GB]  
    | LOG_SIZE = size [GB]  
}  
  
<db_encryption_option> ::=  
    ENCRYPTION { ON | OFF }  
```  
  
## <a name="arguments"></a>参数  
 *database_name*  
 要修改的数据库的名称。 要在设备上显示数据库列表，请使用 [sys.databases (Transact SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)。  
  
 AUTOGROW = { ON | OFF }  
 更新 AUTOGROW 选项。 当 AUTOGROW 为 ON 时，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 根据需要自动为复制表、分布式表和事务日志增大分配空间，以适应存储需求的增长。 当 AUTOGROW 为 OFF 时，如果复制表、分布式表或事务日志超出最大大小设置，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 会返回一个错误。  
  
 REPLICATED_SIZE = size [GB]  
 指定每个计算节点的新最大 GB 数，以便存储要更改的数据库中的所有复制表。 如果正在计划设备存储空间，需要用 REPLICATED_SIZE 乘以设备中的计算节点数。  
  
 DISTRIBUTED_SIZE = size [GB]  
 指定每个数据库的新的最大 GB 数，以便存储要更改的数据库中的所有分布式表。 该大小分布到设备的所有计算节点中。  
  
 LOG_SIZE = size [GB]  
 指定每个数据库的新的最大 GB 数，以便存储要更改的数据库中的所有事务日志。 该大小分布到设备的所有计算节点中。  
  
 ENCRYPTION { ON | OFF }  
 将数据库设置为加密的 (ON) 或未加密的 (OFF)。 只能在 [sp_pdw_database_encryption](http://msdn.microsoft.com/5011bb7b-1793-4b2b-bd9c-d4a8c8626b6e) 已设置为 **1** 时为 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 配置加密。 必须先创建数据库加密密钥，然后才能配置透明数据加密。 有关数据库加密的详细信息，请参阅[透明数据加密 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md)。  
  
## <a name="permissions"></a>权限  
 需要具有针对数据库的 ALTER 权限。  
  
## <a name="general-remarks"></a>一般备注  
 REPLICATED_SIZE、DISTRIBUTED_SIZE 和 LOG_SIZE 的值可以大于、等于或小于数据库的当前值。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 增长和收缩操作是近似的。 所得到的实际大小可能因大小参数而异。  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 不会将 ALTER DATABASE 语句作为原子操作执行。 如果在执行期间中止该语句，将保持已发生的更改。  
  
## <a name="locking-behavior"></a>锁定行为  
 在 DATABASE 对象上采用共享锁。 无法更改另个用户正在读取或写入的数据库。 这包括已在数据库上发出 [USE](http://msdn.microsoft.com/158ec56b-b822-410f-a7c4-1a196d4f0e15) 语句的会话。  
  
## <a name="performance"></a>“性能”  
 收缩数据库可能需要大量时间和系统资源，具体取决于数据库中的实际数据大小和磁盘上的碎片量。 例如，收缩数据库可能需要几个小时或更长时间。  
  
## <a name="determining-encryption-progress"></a>确定加密进度  
 可使用以下查询来确定数据库透明数据加密进度的百分比：  
  
```  
WITH  
database_dek AS (  
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id,  
        dek.encryption_state, dek.percent_complete,  
        dek.key_algorithm, dek.key_length, dek.encryptor_thumbprint,  
        type  
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek  
    INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map  
        ON dek.database_id = node_db_map.database_id   
        AND dek.pdw_node_id = node_db_map.pdw_node_id  
    LEFT JOIN sys.pdw_database_mappings AS db_map  
        ON node_db_map .physical_name = db_map.physical_name  
    INNER JOIN sys.dm_pdw_nodes nodes  
        ON nodes.pdw_node_id = dek.pdw_node_id  
    WHERE dek.encryptor_thumbprint <> 0x  
),  
dek_percent_complete AS (  
    SELECT database_dek.database_id, AVG(database_dek.percent_complete) AS percent_complete  
    FROM database_dek  
    WHERE type = 'COMPUTE'  
    GROUP BY database_dek.database_id  
)  
SELECT DB_NAME( database_dek.database_id ) AS name,  
    database_dek.database_id,  
    ISNULL(  
       (SELECT TOP 1 dek_encryption_state.encryption_state  
        FROM database_dek AS dek_encryption_state  
        WHERE dek_encryption_state.database_id = database_dek.database_id  
        ORDER BY (CASE encryption_state  
            WHEN 3 THEN -1  
            ELSE encryption_state  
            END) DESC), 0)  
        AS encryption_state,  
dek_percent_complete.percent_complete,  
database_dek.key_algorithm, database_dek.key_length, database_dek.encryptor_thumbprint  
FROM database_dek  
INNER JOIN dek_percent_complete   
    ON dek_percent_complete.database_id = database_dek.database_id  
WHERE type = 'CONTROL';  
```  
  
 有关演示实现 TDE 的所有步骤的完整示例，请参阅[透明数据加密 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md)。  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-altering-the-autogrow-setting"></a>A. 更改 AUTOGROW 设置  
 将数据库 `CustomerSales` 的 AUTOGROW 设置为 ON。  
  
```  
ALTER DATABASE CustomerSales  
    SET ( AUTOGROW = ON );  
```  
  
### <a name="b-altering-the-maximum-storage-for-replicated-tables"></a>B. 更改复制表的最大存储  
 下面的示例将数据库 `CustomerSales` 的复制表存储限制设置为 1 GB。 这是每个计算节点的存储限制。  
  
```  
ALTER DATABASE CustomerSales  
    SET ( REPLICATED_SIZE = 1 GB );  
```  
  
### <a name="c-altering-the-maximum-storage-for-distributed-tables"></a>C. 更改分布式表的最大存储  
 下面的示例将数据库 `CustomerSales` 的分布式表存储限制设置为 1000 GB (1 TB)。 这是设备上所有计算节点的组合存储限制，而不是每个计算节点的存储限制。  
  
```  
ALTER DATABASE CustomerSales  
    SET ( DISTRIBUTED_SIZE = 1000 GB );  
```  
  
### <a name="d-altering-the-maximum-storage-for-the-transaction-log"></a>D. 更改事务日志的最大存储  
 下面的示例更新数据库 `CustomerSales`使设备的最大 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事务日志大小为 10 GB。  
  
```  
ALTER DATABASE CustomerSales  
    SET ( LOG_SIZE = 10 GB );  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE DATABASE（并行数据仓库）](../../t-sql/statements/create-database-parallel-data-warehouse.md)   
 [DROP DATABASE (Transact SQL)](../../t-sql/statements/drop-database-transact-sql.md)  
  
  
