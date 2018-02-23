---
title: "CREATE DATABASE（Azure SQL 数据仓库）| Microsoft Docs"
ms.custom: 
ms.date: 02/14/20178
ms.prod: 
ms.prod_service: sql-data-warehouse
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
author: barbkess
ms.author: barbkess
manager: craigg
ms.openlocfilehash: 3a802dc74793ef79ca35b177b4416d9464a8c34f
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="create-database-azure-sql-data-warehouse"></a>CREATE DATABASE（Azure SQL 数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

创建新数据库。  
  
## <a name="syntax"></a>语法  
  
```  
CREATE DATABASE database_name [ COLLATE collation_name ]  
(  
    [ MAXSIZE = { 
          250 | 500 | 750 | 1024 | 5120 | 10240 | 20480 | 30720 
        | 40960 | 51200 | 61440 | 71680 | 81920 | 92160 | 102400 
        | 153600 | 204800 | 245760 
      } GB ,
    ]  
    EDITION = 'datawarehouse',  
    SERVICE_OBJECTIVE = { 
         'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500' | 'DW600' 
        | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000' | 'DW3000' | 'DW6000' 
        | 'DW1000c' | 'DW1500c' | 'DW2000c' | 'DW2500c' | 'DW3000c' | 'DW5000c' 
        | 'DW6000c' | 'DW7500c' | 'DW10000c' | 'DW15000c' | 'DW30000c'
    }  
)  
[;]  
```  
  
## <a name="arguments"></a>参数  
*database_name*  
新数据库的名称。 此名称在 SQL Server 上必须是唯一的，它可托管 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 数据库和 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 数据库，且符合标识符的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 规则。 有关详细信息，请参阅[标识符](http://go.microsoft.com/fwlink/p/?LinkId=180386)。  
  
*collation_name*  
指定数据库的默认排序规则。 排序规则名称既可以是 Windows 排序规则名称，也可以是 SQL 排序规则名称。 如果未指定，则会为数据库分配默认排序规则（即 SQL_Latin1_General_CP1_CI_AS）。  
  
有关 Windows 和 SQL 排序规则名称的详细信息，请参阅 [COLLATE (Transact-SQL)](http://msdn.microsoft.com/library/ms184391.aspx)。  
  
*EDITION*  
指定数据库的服务层。 对于 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，使用 'datawarehouse'。  
  
*MAXSIZE*  
默认为 245,760 GB (240 TB)。  

适用于：“已针对弹性进行优化”性能层

允许的最大数据库大小。 数据库大小不能超出 MAXSIZE。 

适用于：“已针对计算进行优化”性能层

数据库中允许的最大行存储数据大小。 存储在行存储表中的数据、列存储索引的增量存储或非聚集索引（聚集在列存储索引上）都不可超过 MAXSIZE。  压缩到列存储格式的数据没有大小限制，不受 MAXSIZE 约束。
  
SERVICE_OBJECTIVE  
指定性能级别。 有关 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 的服务目标的详细信息，请参阅[性能层](https://azure.microsoft.com/documentation/articles/performance-tiers/)。  
  
## <a name="general-remarks"></a>一般备注  
使用 [DATABASEPROPERTYEX (Transact-SQL)](../../t-sql/functions/databasepropertyex-transact-sql.md) 查看数据库属性。  
  
使用 [ALTER DATABASE（Azure SQL 数据仓库）](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md)在以后更改最大大小或服务目标值。   

SQL 数据仓库设置为 COMPATIBILITY_LEVEL 130，且不得更改。 有关详细信息，请参阅 [Improved Query Performance with Compatibility Level 130 in Azure SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/)（在 Azure SQL 数据库中通过兼容性级别 130 优化查询性能）。
  
## <a name="permissions"></a>权限  
所需的权限：  
  
-   服务器级别主体登录名（由预配进程创建），或者  
  
-   `dbmanager` 数据库角色的成员。  
  
## <a name="error-handling"></a>错误处理  
如果数据库的大小达到 MAXSIZE，你将收到错误代码 40544。 如果发生这种情况，你不能插入或更新数据或创建新的对象（如表、存储过程、视图和函数）。 不过，仍可以读取和删除数据、截断表、删除表和索引以及重新生成索引。 然后，您可以将 MAXSIZE 更新为比当前数据库大小更大的值，或者删除一些数据以释放存储空间。 在您可以插入新数据之前，可能有长达十五分钟的延迟。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
您必须连接到 master 数据库才能创建新的数据库。  
  
`CREATE DATABASE` 语句必须是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批处理中的唯一语句。

创建数据库后，无法更改数据库排序规则。   
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]  
  
### <a name="a-simple-example"></a>A. 简单示例  
创建数据仓库数据库的简单示例。 这将创建最小最大大小为 10240 GB、默认排序规则为 SQL_Latin1_General_CP1_CI_AS 且 最小计算功率为 DW100 的数据库。  
  
```  
CREATE DATABASE TestDW  
(EDITION = 'datawarehouse', SERVICE_OBJECTIVE='DW100');  
```  
  
### <a name="b-create-a-data-warehouse-database-with-all-the-options"></a>B. 创建具有所有选项的数据仓库数据库  
创建使用所有选项的 10 TB 数据仓库的示例。  
  
```  
CREATE DATABASE TestDW COLLATE Latin1_General_100_CI_AS_KS_WS  
(MAXSIZE = 10240 GB, EDITION = 'datawarehouse', SERVICE_OBJECTIVE = 'DW1000');  
```  
  
## <a name="see-also"></a>另请参阅  
[ALTER DATABASE（Azure SQL 数据仓库）](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md)
[CREATE TABLE（Azure SQL 数据仓库）](../../t-sql/statements/create-table-azure-sql-data-warehouse.md) 
[DROP DATABASE (Transact-SQL)](../../t-sql/statements/drop-database-transact-sql.md) 
  

