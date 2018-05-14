---
title: ALTER DATABASE（Azure SQL 数据仓库）| Microsoft Docs
ms.custom: ''
ms.date: 02/15/2018
ms.prod: ''
ms.prod_service: sql-data-warehouse
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: da712a46-5f8a-4888-9d33-773e828ba845
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 2e89ba1dde52c1b5cb919ff34181d7ca723b6c61
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2018
---
# <a name="alter-database-azure-sql-data-warehouse"></a>ALTER DATABASE（Azure SQL 数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

为数据库修改名称、最大大小或服务对象。  
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
ALTER DATABASE database_name  

  MODIFY NAME = new_database_name  
| MODIFY ( <edition_option> [, ... n] )  
  
<edition_option> ::=   
      MAXSIZE = { 
            250 | 500 | 750 | 1024 | 5120 | 10240 | 20480 
          | 30720 | 40960 | 51200 | 61440 | 71680 | 81920 
          | 92160 | 102400 | 153600 | 204800 | 245760 
      } GB  
      | SERVICE_OBJECTIVE = { 
            'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500' 
          | 'DW600' | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000' 
          | 'DW3000' | 'DW6000' | 'DW1000c' | 'DW1500c' | 'DW2000c' 
          | 'DW2500c' | 'DW3000c' | 'DW5000c' | 'DW6000c' | 'DW7500c' 
          | 'DW10000c' | 'DW15000c' | 'DW30000c'
      }  
```  
  
## <a name="arguments"></a>参数  
*database_name*  
指定要修改的数据库的名称。  

MODIFY NAME = new_database_name  
使用指定的名称 new_database_name 重命名数据库。  
  
MAXSIZE  
默认为 245,760 GB (240 TB)。  

适用于：“已针对弹性进行优化”性能层

允许的最大数据库大小。 数据库大小不能超出 MAXSIZE。 

适用于：“已针对计算进行优化”性能层

数据库中允许的最大行存储数据大小。 存储在行存储表中的数据、列存储索引的增量存储或非聚集索引（聚集在列存储索引上）都不可超过 MAXSIZE。  压缩到列存储格式的数据没有大小限制，不受 MAXSIZE 约束。 
  
SERVICE_OBJECTIVE  
指定性能级别。 有关 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] 的服务目标的详细信息，请参阅[性能层](https://azure.microsoft.com/documentation/articles/performance-tiers/)。  
  
## <a name="permissions"></a>权限  
需要以下权限：  
  
-   服务器级别主体登录名（由预配进程创建），或者  
  
-   `dbmanager` 数据库角色的成员。  
  
数据库的所有者不能更改数据库，除非该所有者是 `dbmanager` 角色的成员。  
  
## <a name="general-remarks"></a>一般备注  
当前数据库必须不同于你正在更改的数据库，因此连接到 master 数据库之后必须运行 ALTER。  
  
SQL 数据仓库设置为 COMPATIBILITY_LEVEL 130，且不得更改。 有关详细信息，请参阅[在 Azure SQL 数据库中通过兼容性级别 130 优化查询性能](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/)。
  
若要减小数据库的大小，请使用 [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
要运行 ALTER DATABASE，数据库必须处于联机且非暂停状态。  
  
必须在自动提交模式（默认事务管理模式）下运行 ALTER DATABASE 语句。 此操作在连接设置中进行设置。  
  
ALTER DATABASE 不能是用户定义的事务的一部分。

不可更改数据库排序规则。  
  
## <a name="examples"></a>示例  
在运行这些示例之前，请确保所更改的数据库不是当前数据库。 当前数据库必须不同于你正在更改的数据库，因此连接到 master 数据库之后必须运行 ALTER。  

### <a name="a-change-the-name-of-the-database"></a>A. 更改数据库的名称  

```  
ALTER DATABASE AdventureWorks2012  
MODIFY NAME = Northwind;  
```  
  
### <a name="b-change-max-size-for-the-database"></a>B. 更改数据库的最大大小  
  
```  
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB );  
```  
  
### <a name="c-change-the-performance-level"></a>C. 更改性能级别  
  
```  
ALTER DATABASE dw1 MODIFY ( SERVICE_OBJECTIVE= 'DW1200' );  
```  
  
### <a name="d-change-the-max-size-and-the-performance-level"></a>D. 更改最大大小和性能级别  
  
```  
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB, SERVICE_OBJECTIVE= 'DW1200' );  
```  
  
## <a name="see-also"></a>另请参阅  
[CREATE DATABASE（Azure SQL 数据仓库）](../../t-sql/statements/create-database-azure-sql-data-warehouse.md)
[参考主题的 SQL 数据仓库列表](https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-overview-reference/)  
  
