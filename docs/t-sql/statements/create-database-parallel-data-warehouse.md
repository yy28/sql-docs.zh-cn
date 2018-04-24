---
title: CREATE DATABASE（并行数据仓库）| Microsoft Docs
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
ms.assetid: 40cacde4-ac72-45f7-9564-d76e2b4a741a
caps.latest.revision: 13
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 41ed767a4acd2dbe4b202e94ed054da46810e14a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="create-database-parallel-data-warehouse"></a>CREATE DATABASE（并行数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  在 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 设备上创建新的数据库。 使用该语句创建与设备数据库相关联的所有文件，并为数据库表和事务日志设置最大大小和自动增长选项。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [Transact-SQL 语法约定 (Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
CREATE DATABASE database_name   
WITH (   
    [ AUTOGROW = ON | OFF , ]   
    REPLICATED_SIZE = replicated_size [ GB ] ,  
    DISTRIBUTED_SIZE = distributed_size [ GB ] ,  
    LOG_SIZE = log_size [ GB ] )  
[;]  
```  
  
## <a name="arguments"></a>参数  
 *database_name*  
 新数据库的名称。 有关允许的数据库名称的详细信息，请参阅 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] 中的“对象命名规则”和“保留的数据库名称”。  
  
 AUTOGROW = ON | OFF  
 指定此数据库的 replicated_size、distributed_size 和 log_size 参数是否将根据需要自动增加到超出其指定大小。 默认值为 OFF。  
  
 如果 AUTOGROW 为 ON，则 replicated_size、distributed_size 和 log_size 将根据所需（不是在初始指定大小的块中），随需要比已分配存储更多存储的每次数据插入、更新或其他操作增加。  
  
 如果 AUTOGROW 为 OFF，则大小不会自动增加。 当尝试执行需要将 replicated_size、distributed_size 或 log_size 增加到超过其指定值的操作时，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 将返回错误。  
  
 对于所有大小，AUTOGROW 要么都设置为 ON，要么都为 OFF。 例如，不可能对于 log_size 将 AUTOGROW 设置为 ON，对于 replicated_size，却不这样设置。  
  
 replicated_size [ GB ]  
 一个正数。 为分配到复制表和每个 Compute 节点上的相应数据的总空间设置大小（整数或十进制 GB）。 有关 replicated_size 的最小和最大要求的信息，请参阅 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] 中的“最小值和最大值”。  
  
 如果 AUTOGROW 为 ON，复制表允许增加到超出限制。  
  
 如果 AUTOGROW 为 OFF，那么当用户尝试创建新的复制表、将数据插入到现有复制表或以增加的大小可能会超过 replicated_size 的方式更新现有复制表时，将返回错误。  
  
 distributed_size [ GB ]  
 一个正数。 整个设备上分配给分布式表（以及相应数据）的总空间大小（整数或十进制 GB）。 有关 distributed_size 的最小和最大要求的信息，请参阅 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] 中的“最小值和最大值”。  
  
 如果 AUTOGROW 为 ON，分布式表将可以增加到超出限制。  
  
 如果 AUTOGROW 为 OFF，那么当用户尝试创建新的分布式表、将数据插入到现有分布式表或以增加的大小可能会超过 replicated_size 的方式更新现有分布式表时，将返回错误。  
  
 log_size [ GB ]  
 一个正数。 整个设备上的事务日志的大小（整数或十进制 GB）。  
  
 有关 log_size 的最小和最大要求的信息，请参阅 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] 中的“最小值和最大值”。  
  
 如果 AUTOGROW 为 ON，日志文件将可以增加到超出限制。 使用 [DBCC SHRINKLOG（Azure SQL 数据仓库）](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)语句将日志文件大小减少至初始大小。  
  
 如果 AUTOGROW 为 OFF，那么对于在单个计算节点上增加的日志大小可能会超过 log_size 的任何操作，将向用户返回错误。  
  
## <a name="permissions"></a>权限  
 需要 master 数据库中的 CREATE ANY DATABASE 权限，或者 sysadmin 固定服务器角色的成员身份。  
  
 以下示例向数据库用户 Fay 提供创建数据库的权限。  
  
```  
USE master;  
GO  
GRANT CREATE ANY DATABASE TO [Fay];  
GO  
```  
  
## <a name="general-remarks"></a>一般备注  
 数据库创建时的数据库兼容性级别为 120，这是 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 的兼容级别。 这可确保数据库将能够使用 PDW 所使用的所有 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 功能。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 不允许在显式事务中使用 CREATE DATABASE 语句。 有关详细信息，请参阅[语句](../../t-sql/statements/statements.md)。  
  
 有关数据库的最小和最大约束的信息，请参阅 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] 中的“最小值和最大值”。  
  
 在创建数据库时，每个 Compute 节点上必须有足够的可用空间来分配以下大小的总和：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的表的大小为 replicated_table_size。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的表的大小为（distributed_table_size/Compute 节点数量）。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日志的大小为（log_size/Compute 节点数量）。  
  
## <a name="locking"></a>锁定  
 在 DATABASE 对象上采用共享锁。  
  
## <a name="metadata"></a>元数据  
 成功执行此操作后，[sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 和 [sys.objects (Transact-SQL)](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) 元数据视图中将会显示该数据库的条目。  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-basic-database-creation-examples"></a>A. 基本数据库创建示例  
 以下示例创建数据库 `mytest`，对于复制表，每个 Compute 节点分配 100 GB 存储，对于分布式表，每个设备分配 500 GB 存储，对于事务日志，每个设备分配 100 GB 存储。 在此示例中，AUTOGROW 默认为关。  
  
```  
CREATE DATABASE mytest  
   WITH   
   (REPLICATED_SIZE = 100 GB,  
   DISTRIBUTED_SIZE = 500 GB,  
   LOG_SIZE = 100 GB );  
```  
  
 以下示例使用和以上相同的参数创建数据库 `mytest`，但 AUTOGROW 为关闭。 这允许数据库增加到超过参数的指定大小。  
  
```  
CREATE DATABASE mytest  
   WITH   
   (AUTOGROW = ON,  
   REPLICATED_SIZE = 100 GB,  
   DISTRIBUTED_SIZE = 500 GB,  
   LOG_SIZE = 100 GB);  
```  
  
### <a name="b-creating-a-database-with-partial-gigabyte-sizes"></a>B. 创建部分 GB 级大小数据库  
 以下示例创建数据库 `mytest`，（AUTOGROW 为 关）对于复制表，每个计算节点分配 1.5 GB 存储，对于分布式表，每个设备分配 5.25 GB 存储，对于事务日志，每个设备分配 10 GB 存储。  
  
```  
CREATE DATABASE mytest  
   WITH   
   (REPLICATED_SIZE = 1.5 GB,  
   DISTRIBUTED_SIZE = 5.25 GB,  
   LOG_SIZE = 10 GB);  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER DATABASE（并行数据仓库）](../../t-sql/statements/alter-database-parallel-data-warehouse.md)   
 [DROP DATABASE (Transact SQL)](../../t-sql/statements/drop-database-transact-sql.md)  
  
  
