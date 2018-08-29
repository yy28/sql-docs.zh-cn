---
title: sys.sysdatabases (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysdatabases_TSQL
- sys.sysdatabases_TSQL
- sys.sysdatabases
- sysdatabases
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysdatabases compatibility view
- sysdatabases system table
ms.assetid: 60a93880-62f1-4eda-a886-f046706ba90c
caps.latest.revision: 35
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4942e0fb4161f64b47a074e9de18ccfecb40c648
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43066315"
---
# <a name="syssysdatabases-transact-sql"></a>sys.sysdatabases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  个实例中的每个数据库占一行[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 当[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]首次安装**sysdatabases**包含的条目**主**，**模型**， **msdb**，和**tempdb**数据库。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|数据库名称|  
|**dbid**|**smallint**|数据库 ID|  
|**sid**|**varbinary(85)**|数据库创建者的系统 ID|  
|**模式**|**smallint**|用于创建数据库时在内部锁定该数据库。|  
|**status**|**int**|状态位，可以通过设置其中一些[ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)所述：<br /><br /> 1 = **autoclose** (ALTER DATABASE)<br /><br /> 4 =**选择到 / bulkcopy** (ALTER DATABASE，使用 SET RECOVERY)<br /><br /> 8 = **trunc.log 上 chkpt** (ALTER DATABASE，使用 SET RECOVERY)<br /><br /> 16 =**残缺页检测**(ALTER DATABASE)<br /><br /> 32 =**加载**<br /><br /> 64 =**恢复前的准备**<br /><br /> 128 =**恢复**<br /><br /> 256 =**不恢复**<br /><br /> 512 =**脱机**(ALTER DATABASE)<br /><br /> 1024 =**只读**(ALTER DATABASE)<br /><br /> 2048 =**仅供 dbo 使用**(ALTER DATABASE，使用 SET RESTRICTED_USER)<br /><br /> 4096 =**单个用户**(ALTER DATABASE)<br /><br /> 32768 =**紧急模式**<br /><br /> 65536 =**校验和**(ALTER DATABASE)<br /><br /> 4194304 = **autoshrink** (ALTER DATABASE)<br /><br /> 1073741824 =**完全关闭**<br /><br /> 可以同时打开多个位。|  
|**status2**|**int**|16384 = **ANSI null 默认值**(ALTER DATABASE)<br /><br /> 65536 =**串联 null 时得到 null** (ALTER DATABASE)<br /><br /> 131072 =**递归触发器**(ALTER DATABASE)<br /><br /> 1048576 =**默认为局部游标**(ALTER DATABASE)<br /><br /> 8388608 =**带引号的标识符**(ALTER DATABASE)<br /><br /> 33554432 =**提交时关闭游标**(ALTER DATABASE)<br /><br /> 67108864 = **ANSI nulls** (ALTER DATABASE)<br /><br /> 268435456 = **ANSI 警告**(ALTER DATABASE)<br /><br /> 536870912 =**启用了全文**(通过设置**sp_fulltext_database**)|  
|**crdate**|**datetime**|创建日期|  
|**保留**|**datetime**|保留供将来使用。|  
|**category**|**int**|包含用于复制的信息位图：<br /><br /> 1 = 为快照或事务复制而发布。<br /><br /> 2 = 订阅快照或事务发布。<br /><br /> 4 = 为合并复制而发布。<br /><br /> 8 = 订阅合并发布。<br /><br /> 16 = 发布数据库。|  
|**cmptlevel**|**tinyint**|数据库的兼容性级别。 有关详细信息，请参阅 [ALTER DATABASE 兼容级别 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。|  
|**filename**|nvarchar(260)|数据库主文件的操作系统路径和名称。<br /><br /> **文件名**可见**dbcreator**， **sysadmin**，使用 CREATE ANY DATABASE 权限或具有以下权限之一的被授权者数据库所有者： ALTER ANY DATABASE创建任何数据库，查看任何定义。 若要返回的路径和文件名称，请查询[sys.sysfiles](../../relational-databases/system-compatibility-views/sys-sysfiles-transact-sql.md)兼容性视图中，或[sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)视图。|  
|**version**|**smallint**|用于创建数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代码的内部版本号。 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="see-also"></a>请参阅  
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [系统表映射到系统视图&#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [兼容性视图 (Transact SQL)](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
