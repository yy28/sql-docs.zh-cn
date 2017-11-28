---
title: "sys.sysdatabases (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysdatabases_TSQL
- sys.sysdatabases_TSQL
- sys.sysdatabases
- sysdatabases
dev_langs: TSQL
helpviewer_keywords:
- sys.sysdatabases compatibility view
- sysdatabases system table
ms.assetid: 60a93880-62f1-4eda-a886-f046706ba90c
caps.latest.revision: "35"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 988f6c7ba4a2494215bbc5c69ce1a77b7bb6f15e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="syssysdatabases-transact-sql"></a>sys.sysdatabases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  实例中每个数据库中对应一行[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 当[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]首次安装**sysdatabases**包含的条目**master**，**模型**， **msdb**，和**tempdb**数据库。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|数据库名称|  
|**dbid**|**int**|数据库 ID|  
|**sid**|**varbinary(85)**|数据库创建者的系统 ID|  
|**模式**|**int**|用于创建数据库时在内部锁定该数据库。|  
|**status**|**int**|状态位，其中一些可以通过使用设置[ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)所述：<br /><br /> 1 = **autoclose** (ALTER DATABASE)<br /><br /> 4 =**选择到 / bulkcopy** (ALTER DATABASE 使用设置恢复)<br /><br /> 8 = **trunc。 登录 chkpt** (ALTER DATABASE 使用设置恢复)<br /><br /> 16 =**残缺页检测**(ALTER DATABASE)<br /><br /> 32 =**加载**<br /><br /> 64 =**恢复前的准备**<br /><br /> 128 =**恢复**<br /><br /> 256 =**未恢复**<br /><br /> 512 =**脱机**(ALTER DATABASE)<br /><br /> 1024 =**只读**(ALTER DATABASE)<br /><br /> 2048 =**仅供 dbo 使用**(ALTER DATABASE 使用设置 RESTRICTED_USER)<br /><br /> 4096 =**单个用户**(ALTER DATABASE)<br /><br /> 32768 =**紧急模式**<br /><br /> 65536 =**校验和**(ALTER DATABASE)<br /><br /> 4194304 =**自动收缩**(ALTER DATABASE)<br /><br /> 1073741824 =**完全关闭**<br /><br /> 可以同时打开多个位。|  
|**status2**|**int**|16384 = **ANSI null 默认值**(ALTER DATABASE)<br /><br /> 65536 =**串联 null 时得到 null** (ALTER DATABASE)<br /><br /> 131072 =**递归触发器**(ALTER DATABASE)<br /><br /> 1048576 =**默认为局部游标**(ALTER DATABASE)<br /><br /> 8388608 =**带引号的标识符**(ALTER DATABASE)<br /><br /> 33554432 =**提交时关闭游标**(ALTER DATABASE)<br /><br /> 67108864 = **ANSI nulls** (ALTER DATABASE)<br /><br /> 268435456 = **ANSI 警告**(ALTER DATABASE)<br /><br /> 536870912 =**完整文本启用**(通过设置**sp_fulltext_database**)|  
|**crdate**|**datetime**|创建日期|  
|**保留**|**datetime**|保留供将来使用。|  
|**类别**|**int**|包含用于复制的信息位图：<br /><br /> 1 = 为快照或事务复制而发布。<br /><br /> 2 = 订阅快照或事务发布。<br /><br /> 4 = 为合并复制而发布。<br /><br /> 8 = 订阅合并发布。<br /><br /> 16 = 发布数据库。|  
|**cmptlevel**|**tinyint**|数据库的兼容性级别。 有关详细信息，请参阅 [ALTER DATABASE 兼容级别 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。|  
|**文件名**|**nvarchar(260)**|数据库主文件的操作系统路径和名称。<br /><br /> **filename**对可见**dbcreator**， **sysadmin**，数据库所有者，拥有 CREATE ANY DATABASE 权限或具有以下权限的任何一个的被授权者： ALTER ANY数据库、 创建任意数据库、 查看任意定义。 若要返回的路径和文件名称，请查询[sys.sysfiles](../../relational-databases/system-compatibility-views/sys-sysfiles-transact-sql.md)兼容性视图或[sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)视图。|  
|**version**|**int**|用于创建数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代码的内部版本号。 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="see-also"></a>另请参阅  
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [将系统表映射到系统视图 &#40;Transact SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [兼容性视图 (Transact SQL)](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
