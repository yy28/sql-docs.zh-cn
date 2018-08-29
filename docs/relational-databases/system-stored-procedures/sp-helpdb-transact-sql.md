---
title: sp_helpdb (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helpdb
- sp_helpdb_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpdb
ms.assetid: 4c3e3302-6cf1-4b2b-8682-004049b578c3
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 09dc7e451e5122600b0ea32222f6fa913c2716f8
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43027701"
---
# <a name="sphelpdb-transact-sql"></a>sp_helpdb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  报告有关指定数据库或所有数据库的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpdb [ [ @dbname= ] 'name' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@dbname=** ] **'***name***'**  
 要报告其信息的数据库的名称。 *名称*是**sysname**，无默认值。 如果*名称*未指定，则**sp_helpdb**中的所有数据库上的报表**sys.databases**目录视图。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|数据库名称。|  
|**db_size**|**nvarchar(13)**|数据库总计大小。|  
|**所有者**|**sysname**|数据库所有者，例如**sa**。|  
|**dbid**|**smallint**|数据库 ID。|  
|**创建**|**nvarchar(11)**|数据库创建的日期。|  
|**status**|**nvarchar(600)**|以逗号分隔的值列表，这些值是当前在数据库上设置的数据库选项的值。<br /><br /> 只有启用布尔值选项时，才将这些选项列出。 非布尔选项及其对应值的形式列出*option_name*=*值*。<br /><br /> 有关详细信息，请参阅 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)。|  
|**compatibility_level**|**tinyint**|数据库兼容级别：60、65、70、80 或 90。|  
  
 如果*名称*没有显示指定的数据库的文件分配的其他结果集的指定。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**nchar(128)**|逻辑文件名称。|  
|**fileid**|**smallint**|文件 ID。|  
|**filename**|**nchar(260)**|操作系统文件名（物理文件名称）。|  
|**filegroup**|**nvarchar(128)**|文件所属的文件组。<br /><br /> NULL = 文件为日志文件。 它决不是文件组的一部分。|  
|size|**nvarchar(18)**|文件大小 (MB)。|  
|**最大大小**|**nvarchar(18)**|文件大小可达到的最大值。 此字段中的 UNLIMITED 值表示文件可以一直增长到磁盘变满为止。|  
|**增长**|**nvarchar(18)**|文件的增量。 这表示添加到每个时间的新空间所需的文件的空间量。|  
|**使用情况**|**varchar(9)**|文件用法。 对于数据文件，值是**仅限数据**并为日志文件的值是**仅记录**。|  
  
## <a name="remarks"></a>Remarks  
 **状态**结果集中列的选项已设置为 ON 的数据库中的报表。 不报告所有数据库选项**状态**列。 若要查看当前数据库选项设置的完整列表，请使用**sys.databases**目录视图。  
  
## <a name="permissions"></a>Permissions  
 当指定单个数据库时中的成员身份**公共**数据库中的角色是必需的。 当不指定任何数据库时中的成员身份**公共**中的角色**master**数据库是必需的。  
  
 如果不能访问数据库， **sp_helpdb**会显示错误消息 15622 和尽可能有关数据库的信息。  
  
## <a name="examples"></a>示例  
  
### <a name="a-returning-information-about-a-single-database"></a>A. 返回有关单个数据库的信息  
 以下示例显示有关 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库的信息。  
  
```sql  
EXEC sp_helpdb N'AdventureWorks2012';  
```  
  
### <a name="b-returning-information-about-all-databases"></a>B. 返回有关所有数据库的信息  
 以下示例显示有关运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的服务器上所有数据库的信息。  
  
```sql  
EXEC sp_helpdb;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.filegroups (Transact-SQL)](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.master_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
