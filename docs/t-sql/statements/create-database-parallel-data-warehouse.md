---
title: "创建数据库 （并行数据仓库） |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 40cacde4-ac72-45f7-9564-d76e2b4a741a
caps.latest.revision: "13"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4e9ff76a4d260604a93f59baa3b61f5c37b4952f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="create-database-parallel-data-warehouse"></a>创建数据库 （并行数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  创建一个新数据库上[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]设备。 若要创建与设备数据库相关联的所有文件，并设置最大大小和数据库表和事务日志的自动增长选项，请使用此语句。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定 &#40;Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 新数据库的名称。 有关允许的数据库名称的详细信息，请参阅"对象命名规则"和"保留的数据库名称"中[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 自动增长 = ON |**OFF**  
 指定是否*replicated_size*， *distributed_size*，和*log_size*根据需要超出其指定为此数据库的参数将自动增长大小。 默认值是**OFF**。  
  
 如果自动增长为 ON， *replicated_size*， *distributed_size*，和*log_size*将增长 （不在指定的初始大小的块） 所需的每个数据插入，已分配更新或需要的存储比其他操作。  
  
 如果自动增长已关闭，不会自动增长大小。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]尝试的操作需要时将返回错误*replicated_size*， *distributed_size*，或*log_size*增大到超过其指定的值。  
  
 自动增长是所有大小的 ON 或 OFF 所有大小的。 例如，不能设置为自动增长 ON 为*log_size*，但未设置为*replicated_size*。  
  
 *replicated_size* [ GB ]  
 一个正数。 设置分配给复制的表和相应的数据的总空间大小 （以整数或小千兆字节为单位）*每个计算节点上*。 最小值和最大值*replicated_size*要求，请参阅中的"最小和最大值" [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 如果自动增长为 ON 时，将允许复制的表增长超过此限制。  
  
 如果自动增长为 OFF，将的插入到现有的复制数据的表，或更新现有用户尝试创建新复制的表，如果复制表会增加超出大小的方式返回错误*replicated_size*.  
  
 *distributed_size* [ GB ]  
 一个正数。 大小，以整数或小千兆字节，为分配给分布式的表 （和相应的数据） 的总空间*跨设备*。 最小值和最大值*distributed_size*要求，请参阅中的"最小和最大值" [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 如果自动增长为 ON 时，将允许分布式的表增长超过此限制。  
  
 如果用户尝试创建一个新的分布式的表，将数据插入到现有的分布式表，或更新现有分布式的表会增加超出大小的方式，如果自动增长为 OFF，将返回错误*distributed_size*.  
  
 *log_size* [ GB ]  
 一个正数。 事务日志大小 （以整数或小千兆字节为单位）*跨设备*。  
  
 最小值和最大值*log_size*要求，请参阅中的"最小和最大值" [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 如果自动增长为 ON 时，允许日志文件增长超过此限制。 使用[DBCC SHRINKLOG （Azure SQL 数据仓库）](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)语句将日志文件的大小减小到其原始大小。  
  
 如果自动增长为 OFF，将向用户提供的任何操作都将增加超出单个计算节点上的日志大小返回错误*log_size*。  
  
## <a name="permissions"></a>权限  
 需要**CREATE ANY DATABASE** master 数据库中或中的成员身份中的权限**sysadmin**固定的服务器角色。  
  
 以下示例向数据库用户 Fay 提供创建数据库的权限。  
  
```  
USE master;  
GO  
GRANT CREATE ANY DATABASE TO [Fay];  
GO  
```  
  
## <a name="general-remarks"></a>一般备注  
 数据库来创建数据库兼容性级别 120，这是兼容性级别[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]。 这可确保数据库将能够使用的所有[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]PDW 使用的功能。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 CREATE DATABASE 语句不允许在显式事务。 有关详细信息，请参阅[语句](../../t-sql/statements/statements.md)。  
  
 在数据库上的最小和最大约束的信息，请参阅"最小和最大值"中[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 在创建的数据库时，必须有足够的可用空间*每个计算节点上*分配以下大小的总和：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库与表的大小*replicated_table_size*。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库与表的大小 (*distributed_table_size* / 的计算节点数)。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]日志的大小 (*log_size* / 的计算节点数)。  
  
## <a name="locking"></a>锁定  
 数据库对象上采用共享的锁。  
  
## <a name="metadata"></a>元数据  
 此操作成功，一个条目为此数据库将出现在之后[sys.databases &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)和[sys.objects &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)元数据视图。  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-basic-database-creation-examples"></a>A. 基本数据库创建示例  
 下面的示例创建数据库`mytest`使用 100 GB 的每个计算节点复制的表、 500 GB 每个分布式表的应用装置和设备的事务日志每 100 GB 的存储分配。 在此示例中，自动增长默认处于关闭状态。  
  
```  
CREATE DATABASE mytest  
   WITH   
   (REPLICATED_SIZE = 100 GB,  
   DISTRIBUTED_SIZE = 500 GB,  
   LOG_SIZE = 100 GB );  
```  
  
 下面的示例创建数据库`mytest`使用与上面相同的参数，除非该自动增长已开启。 这允许 database 放大到超过指定的大小参数。  
  
```  
CREATE DATABASE mytest  
   WITH   
   (AUTOGROW = ON,  
   REPLICATED_SIZE = 100 GB,  
   DISTRIBUTED_SIZE = 500 GB,  
   LOG_SIZE = 100 GB);  
```  
  
### <a name="b-creating-a-database-with-partial-gigabyte-sizes"></a>B. 创建数据库具有部分千兆字节大小  
 下面的示例创建数据库`mytest`、 关闭自动增长，每个复制的表的计算节点的 1.5 GB、 每个分布式表的应用装置 5.25 GB 和每个事务日志的设备的 10 GB 的存储分配。  
  
```  
CREATE DATABASE mytest  
   WITH   
   (REPLICATED_SIZE = 1.5 GB,  
   DISTRIBUTED_SIZE = 5.25 GB,  
   LOG_SIZE = 10 GB);  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER DATABASE &#40;并行数据仓库 &#41;](../../t-sql/statements/alter-database-parallel-data-warehouse.md)   
 [DROP DATABASE (Transact SQL)](../../t-sql/statements/drop-database-transact-sql.md)  
  
  
