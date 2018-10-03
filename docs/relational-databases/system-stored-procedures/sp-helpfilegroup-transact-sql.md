---
title: sp_helpfilegroup (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpfilegroup_TSQL
- sp_helpfilegroup
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpfilegroup
ms.assetid: 619716b5-95dc-4538-82ae-4b90b9da8ebc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1d6e7c28e628254fd33269ab4ee200fee0067870
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47741045"
---
# <a name="sphelpfilegroup-transact-sql"></a>sp_helpfilegroup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回与当前数据库相关联的文件组的名称及属性。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpfilegroup [ [ @filegroupname = ] 'name' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@filegroupname =** ] **'***name***'**  
 当前数据库中任意文件组的逻辑名称。 *名称*是**sysname**，默认值为 NULL。 如果*名称*未指定，则列出当前数据库中的所有文件组，并只为第一个结果集显示在结果集部分中显示。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**groupname**|**sysname**|文件组的名称。|  
|**groupid**|**smallint**|数字文件组标识符。|  
|**filecount**|**int**|文件组中的文件数目。|  
  
 如果*名称*是指定，则返回一个行文件组中每个文件。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**file_in_group**|**sysname**|文件组中文件的逻辑名称。|  
|**fileid**|**smallint**|数字文件标识符。|  
|**filename**|**nchar(260)**|文件的物理名称，包括目录路径。|  
|size|**nvarchar(15)**|文件大小 (KB)。|  
|**最大大小**|**nvarchar(15)**|文件的最大大小。<br /><br /> 这是文件可增长到的最大大小。 此字段中的 UNLIMITED 值表示文件可以一直增长到磁盘变满为止。|  
|**增长**|**nvarchar(15)**|文件的增量。 表示每次需要新的空间时给文件增加的空间大小。<br /><br /> 0 = 文件的大小是固定的，不会增长。|  
  
## <a name="permissions"></a>Permissions  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-returning-all-filegroups-in-a-database"></a>A. 返回数据库中的所有文件组  
 下面的示例返回有关 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 示例数据库中文件组的信息。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_helpfilegroup;  
GO  
```  
  
### <a name="b-returning-all-files-in-a-filegroup"></a>B. 返回文件组中的所有文件  
 下面的示例返回有关 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 示例数据库的 `PRIMARY` 文件组中所有文件的信息。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_helpfilegroup 'PRIMARY';  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_helpfile (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [sys.database_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [sys.filegroups (Transact-SQL)](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [数据库文件和文件组](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
