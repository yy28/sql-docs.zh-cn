---
title: "ALTER DATABASE （并行数据仓库） |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5751656b-7aae-4152-a314-4c631bea4fc4
caps.latest.revision: 10
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 74b47bec1033728d47e5fe577af29c6d43e9af65
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="alter-database-parallel-data-warehouse"></a>ALTER DATABASE （并行数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  修改复制的表、 分布式的表和中的事务日志的最大数据库大小选项[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。 使用此语句可以管理数据库的磁盘空间分配，因为它的增长或收缩的大小。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定 &#40;Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 要修改的数据库的名称。 若要在设备上显示的数据库列表，请使用[sys.databases &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
 自动增长 = {ON |关闭}  
 更新的自动增长选项。 当自动增长为 ON，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]会自动增加为复制的表、 分布式的表和事务日志分配的空间，根据需要以适应存储需求的增长。 自动增长时 OFF，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]会返回一个错误，如果所复制表，分布式表，或事务日志文件超出最大大小设置。  
  
 REPLICATED_SIZE =*大小*[GB]  
 指定每个在更改数据库中存储的所有复制的表的计算节点的新的最大千兆字节。 如果你打算设备存储空间，你将需要 REPLICATED_SIZE 乘以设备中的计算节点数。  
  
 DISTRIBUTED_SIZE =*大小*[GB]  
 指定每个数据库的更改数据库中存储的所有分布式表的新的最大千兆字节。 大小分布在所有设备的计算节点。  
  
 LOG_SIZE =*大小*[GB]  
 指定每个数据库的更改数据库中存储的所有事务日志的新的最大千兆字节。 大小分布在所有设备的计算节点。  
  
 加密 {ON |关闭}  
 将数据库设置为加密的 (ON) 或未加密的 (OFF)。 加密只能为配置[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]时[sp_pdw_database_encryption](http://msdn.microsoft.com/5011bb7b-1793-4b2b-bd9c-d4a8c8626b6e)已设置为**1**。 必须创建数据库加密密钥，然后才能配置透明数据加密。 有关数据库加密的详细信息，请参阅[透明数据加密 &#40;TDE &#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  
  
## <a name="permissions"></a>Permissions  
 需要数据库拥有 ALTER 权限。  
  
## <a name="general-remarks"></a>一般备注  
 REPLICATED_SIZE、 DISTRIBUTED_SIZE 和 LOG_SIZE 值可以是晚于、 等于或小于数据库的当前值。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 增长和收缩操作都是近似值。 所得到的实际大小可能会因大小参数。  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]不执行 ALTER DATABASE 语句以原子操作。 如果在执行期间中止该语句时，将保持已发生更改。  
  
## <a name="locking-behavior"></a>锁定行为  
 数据库对象上采用共享的锁。 无法更改正在由另一个用户使用的读取或写入数据库。 这包括已颁发的会话[使用](http://msdn.microsoft.com/158ec56b-b822-410f-a7c4-1a196d4f0e15)对数据库的语句。  
  
## <a name="performance"></a>性能  
 收缩数据库可能需要大量的时间和系统资源，具体取决于数据库中的实际数据大小和磁盘上的碎片量。 例如，收缩数据库可能需要几小时或更。  
  
## <a name="determining-encryption-progress"></a>确定加密进度  
 使用以下查询来确定数据库，以百分比形式的透明数据加密的进度：  
  
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
  
 有关演示中实现 TDE 的所有步骤的完整示例，请参阅[透明数据加密 &#40;TDE &#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-altering-the-autogrow-setting"></a>A. 更改自动增长设置  
 针对数据库自动增长设置为 ON `CustomerSales`。  
  
```  
ALTER DATABASE CustomerSales  
    SET ( AUTOGROW = ON );  
```  
  
### <a name="b-altering-the-maximum-storage-for-replicated-tables"></a>B. 更改复制的表的最大存储  
 下面的示例设置为 1 GB 的数据库的复制的表存储限制`CustomerSales`。 这是每个计算节点的存储限制。  
  
```  
ALTER DATABASE CustomerSales  
    SET ( REPLICATED_SIZE = 1 GB );  
```  
  
### <a name="c-altering-the-maximum-storage-for-distributed-tables"></a>C. 更改分布式表的最大存储  
 下面的示例设置分布式的表存储限制为 1000 GB (一个 terabyte) 数据库`CustomerSales`。 这不是存储限制，每个计算节点的计算节点上，所有设备的组合的存储限制。  
  
```  
ALTER DATABASE CustomerSales  
    SET ( DISTRIBUTED_SIZE = 1000 GB );  
```  
  
### <a name="d-altering-the-maximum-storage-for-the-transaction-log"></a>D. 更改事务日志的最大存储  
 下面的示例更新数据库`CustomerSales`以最多有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]装置事务日志大小的 10 GB。  
  
```  
ALTER DATABASE CustomerSales  
    SET ( LOG_SIZE = 10 GB );  
```  
  
## <a name="see-also"></a>另请参阅  
 [创建数据库 &#40;并行数据仓库 &#41;](../../t-sql/statements/create-database-parallel-data-warehouse.md)   
 [DROP DATABASE (Transact SQL)](../../t-sql/statements/drop-database-transact-sql.md)  
  
  
